---
title: 什么是 Windows Admin Center
description: 什么是 Windows Admin Center (Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d374704768d06aaeb7ee6bc9c984cc78d49cb4b0
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2018
ms.locfileid: "4080904"
---
# 什么是 Windows Admin Center？

>适用于：Windows Admin Center、Windows Admin Center 预览版

Windows Admin Center 是一个在本地部署的基于浏览器的管理工具集，让你能够管理 Windows Server，而无需依赖 Azure 或云。 利用 Windows Admin Center，你可以完全控制服务器基础结构的各个方面，对于在未连接到 Internet 的专用网络上进行管理特别有用。

Windows Admin Center 是“内部”管理工具（例如服务器管理器和 MMC）的现代演进版。 它是对 System Center 的补充-它不会替换。

![](../media/wac-complements.png)

## Windows Admin Center 如何工作？

Windows Admin Center 在 Web 浏览器上运行，通过安装在 Windows Server 2016 或 Windows 10 上的 **Windows Admin Center 网关**管理 Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows 10 等程序。 该网关通过使用远程 PowerShell 管理服务器，并通过 WinRM 管理 WMI。 此网关使用单个的轻型 .msi 程序包在 Windows Admin Center 中提供，你可以[下载](https://aka.ms/windowsadmincenter)它。

发布到 DNS 并提供对相应公司防火墙的访问权限后，Windows Admin Center 让你可以通过 Microsoft Edge 或 Google Chrome 从任何位置安全地连接和管理你的服务器。

![](../media/architecture.png)

## 了解 Windows Admin Center 如何改进管理环境

### **熟悉的功能**

Windows Admin Center 是像 Microsoft 管理控制台 (MMC) 这样的长期知名管理平台的演进版本，它针对系统当前的构建和管理方式从头构建。 Windows Admin Center 包含许多你目前用于管理 Windows Server 和客户端的熟悉工具。

### **易于安装和使用**

在 Windows 10 计算机上[安装](../deploy/install.md)，在数分钟内即可开始管理，或在充当网关的 Windows 2016 服务器上安装，让你的整个组织都可以从 Web 浏览器管理计算机。

### **补充现有的解决方案** 

Windows Admin Center 的工作原理与解决方案，如 System Center 和 Azure 管理和安全，将添加到其功能执行详细的单计算机管理任务。

### **从任何位置管理**

将 Windows Admin Center 网关服务器发布到公共 Internet，然后你便可以从任何位置连接并管理服务器，全部以安全的方式。

### **增强管理平台的安全性**

Windows Admin Center 进行了许多改进，让你的管理平台[更安全](../plan/user-access-options.md)。 基于角色的访问控制允许你微调哪些管理员有权访问哪些管理功能。 网关身份验证选项包括本地组、本地基于域的 Active Directory 和基于云的 Azure Active Directory。  此外，[还可了解](../use/logging.md)在你的环境中执行的管理操作。

### **Azure 集成**

Windows Admin Center 有很多点[与 Azure 服务的集成](../plan/azure-integration-options.md)，包括 Azure Active Directory 和 Azure 备份、 Azure Site Recovery，等等。

### **管理超融合群集**

Windows Admin Center 提供[管理超融合群集](../use/manage-hyper-converged.md)的最佳体验 - 包括虚拟化计算、存储和网络组件。

### **扩展性**

Windows Admin Center 在构建之初就考虑了可扩展性，它为 Microsoft 和第三方开发人员提供了除当前产品和服务外构建其他工具和解决方案的能力。 Microsoft 提供允许开发人员构建自己的 Windows Admin Center 工具的 [SDK](../extend/extensibility-overview.md) 。

> [!Tip]
> 已准备好安装 Windows Admin Center？ [立即下载](https://aka.ms/windowsadmincenter)