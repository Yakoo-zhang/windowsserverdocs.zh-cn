---
ms.date: 09/27/2018
ms.topic: conceptual
contributor: maertendMSFT
author: maertendmsft
title: 适用于 Windows 的 OpenSSH 服务器配置
ms.product: windows-server
ms.openlocfilehash: defb8875ca73c0d08fb0fa0764ed3ddf9003e09c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852040"
---
# <a name="openssh-key-management"></a>OpenSSH 密钥管理

Windows 环境中的大多数身份验证都是使用用户名-密码对完成的。
这适用于共享公共域的系统。 当跨域工作时（例如在本地和云托管的系统之间），这会变得更加困难。

相比之下，Linux 环境通常使用公钥/私钥对来驱动身份验证。
OpenSSH 提供了工具来帮助支持此用途，具体如下：

* __ssh-keygen__，用于生成安全的密钥
* __ssh-agent__ 和 __ssh-add__，用于安全地存储私钥
* __scp__ 和 __sftp__，在首次使用服务器时安全地复制公钥文件

本文档概述了如何在 Windows 上使用这些工具开始使用 SSH 进行密钥身份验证。 如果你不熟悉 SSH 密钥管理，我们强烈建议你查看 [NIST 文档 IR 7966](http://nvlpubs.nist.gov/nistpubs/ir/2015/NIST.IR.7966.pdf)，标题为“使用安全外壳 (SSH) 的交互和自动化访问管理的安全性”。

## <a name="about-key-pairs"></a>关于密钥对

密钥对指的是由特定的身份验证协议使用的公钥和私钥文件。 

SSH 公钥身份验证使用不对称加密算法来生成两个密钥文件 – 一个为“私钥”文件，一个为“公钥”文件。 私钥文件等效于密码，在所有情况下都应当保护它们。 如果有人获取了你的私钥，则他们可以像你一样登录到你有权登录的任何 SSH 服务器。 公钥放置在 SSH 服务器上，并且可以共享，不会危害私钥的安全。

将密钥身份验证用于 SSH 服务器时，SSH 服务器和客户端会依据私钥来比较所提供的用户名的公钥。 如果无法依据客户端私钥验证公钥，则身份验证失败。 

可以通过在生成密钥对时要求提供密码来通过密钥对实现多重身份验证（参见下文的密钥生成）。 在身份验证期间，会提示用户输入密码，将使用该密码以及 SSH 客户端上的私钥来对用户进行身份验证。 

## <a name="host-key-generation"></a>主机密钥生成

公钥具有特定的 ACL 要求，在 Windows 上，这些要求等同于仅允许管理员和 System 进行访问。 为使此更加简单， 

* 已创建了 OpenSSHUtils PowerShell 模块来正确设置密钥 ACL，并且应当将该模块安装在服务器上
* 首次使用 sshd 时，将自动生成主机的密钥对。 如果 ssh-agent 正在运行，则密钥将自动添加到本地存储中。 

若要使用 SSH 服务器轻松进行密钥身份验证，请在权限提升的 PowerShell 提示符下运行以下命令：

```powershell

# Install the OpenSSHUtils module to the server. This will be valuable when deploying user keys.
Install-Module -Force OpenSSHUtils -Scope AllUsers

# Start the ssh-agent service to preserve the server keys
Start-Service ssh-agent

# Now start the sshd service
Start-Service sshd
```

由于没有与 sshd 服务关联的用户，因此主机密钥存储在 \ProgramData\ssh 下。


## <a name="user-key-generation"></a>用户密钥生成

若要使用基于密钥的身份验证，首先需要为客户端生成一些公钥/私钥对。 通过 PowerShell 或 cmd，使用 ssh-keygen 生成一些密钥文件。

```powershell
cd ~\.ssh\
ssh-keygen
```

这应当会显示如下某些内容（其中，“username”将替代为你的用户名）

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\username\.ssh\id_ed25519):
```

你可以按 Enter 来接受默认值，或指定要在其中生成密钥的路径。 此时，系统会提示你使用密码来加密你的私钥文件。
密码与密钥文件一起工作来提供双重身份验证。 在此示例中，我们将密码留空。 

```
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in C:\Users\username\.ssh\id_ed25519.
Your public key has been saved in C:\Users\username\.ssh\id_ed25519.pub.
The key fingerprint is: 
SHA256:OIzc1yE7joL2Bzy8!gS0j8eGK7bYaH1FmF3sDuMeSj8 username@server@LOCAL-HOSTNAME

The key's randomart image is:
+--[ED25519 256]--+
|        .        |
|         o       |
|    . + + .      |
|   o B * = .     |
|   o= B S .      |
|   .=B O o       |
|  + =+% o        |
| *oo.O.E         |
|+.o+=o. .        |
+----[SHA256]-----+
```

现在，你有了一个公钥/私钥 ED25519 密钥对（.pub 文件是公钥，其余的是私钥）：

```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/28/2018  11:09 AM           1679 id_ed25519
-a----        9/28/2018  11:09 AM            414 id_ed25519.pub
```

请记住，私钥文件等效于密码，应当采用与保护密码相同的方式来保护它。
为了实现此目的，请使用 ssh-agent 来将私钥安全地存储在与你的 Windows 登录关联的 Windows 安全上下文中。 为执行该操作，请以管理员身份启动 ssh-agent 服务并使用 ssh-add 来存储私钥。 

```powershell
# Make sure you're running as an Administrator
Start-Service ssh-agent

# This should return a status of Running
Get-Service ssh-agent

# Now load your key files into ssh-agent
ssh-add ~\.ssh\id_ed25519

```

完成这些步骤后，每当从此客户端进行身份验证需要使用私钥时，ssh-agent 都会自动检索本地私钥，并将其传递到你的 SSH 客户端。

> [!NOTE]
> 强烈建议你将私钥备份到一个安全位置，将其添加到 ssh-agent，然后将其从本地系统中删除。 
> 无法从代理中检索私钥。
> 如果你失去了对私钥的访问权限，则必须在你与之交互的所有系统上创建一个新的密钥对并更新公钥。

## <a name="deploying-the-public-key"></a>部署公钥

若要使用上面创建的用户密钥，需要将公钥放置在服务器上的一个文本文件中，该文件名为 *authorized_keys*，位于 users\username\.ssh\. 下 OpenSSH 工具包括了 scp 来帮助实现此目的，这是一个安全的文件传输实用工具。

将公钥 (~\.ssh\id_ed25519.pub) 的内容移动到服务器/主机上 ~\.ssh 中名为 authorized_keys 的文本文件中。

此示例使用了之前在上面的说明中在主机上安装的 OpenSSHUtils 模块中的 Repair-AuthorizedKeyPermissions 函数。

```powershell
# Make sure that the .ssh directory exists in your server's home folder
ssh user1@domain1@contoso.com mkdir C:\users\user1\.ssh\

# Use scp to copy the public key file generated previously to authorized_keys on your server
scp C:\Users\user1\.ssh\id_ed25519.pub user1@domain1@contoso.com:C:\Users\user1\.ssh\authorized_keys

# Appropriately ACL the authorized_keys file on your server  
ssh --% user1@domain1@contoso.com powershell -c $ConfirmPreference = 'None'; Repair-AuthorizedKeyPermission C:\Users\user1\.ssh\authorized_keys
```

这些步骤完成了对 Windows 上的 SSH 使用基于密钥的身份验证所需的配置。
完成此项后，用户可以从具有私钥的任何客户端连接到 sshd 主机。

