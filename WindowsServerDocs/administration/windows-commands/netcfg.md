---
title: netcfg
description: 适用于 * * * * 的 Windows 命令主题
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2daaab7-12db-4e36-b70c-db8906d084f7 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4895928ffdd5d923d370f82e699d69f42c0f81a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838930"
---
# <a name="netcfg"></a>netcfg

>适用于：Windows Server（半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

安装 Windows 预安装环境（WinPE），这是用于部署工作站的 Windows 轻型版本。
## <a name="syntax"></a>语法
```
netcfg [/v] [/e] [/winpe] [/l ] /c /i
```
#### <a name="parameters"></a>参数
|参数|说明|
|-------|--------|
|/v|**在详细（详细）** 模式下运行|
|/e|在安装和卸载过程中使用服务**环境**变量|
|/winpe|为 Windows 预安装环境（WinPE）安装 TCP/IP、NetBIOS 和 Microsoft 客户端|
|/l|提供 INF**位置**|
|/c|提供要安装的组件的**类**;协议、服务或客户端|
|/i|提供组件**ID**|
|/s|提供要**显示**的组件的类型。<p>\ta = 适配器，n = net 组件|
|/b|显示**绑定路径**，后跟包含路径名称的字符串。|
|/?|在命令提示符下显示**帮助**。|

## <a name="examples"></a><a name=BKMK_Examples></a>示例

使用 c:\oemdir\example.inf 安装协议*示例*：
```
netcfg /l c:\oemdir\example.inf /c p /i example
```
若要安装*MS_Server*服务：
```
netcfg /c s /i MS_Server
```
为 Windows 预安装环境安装 TCP/IP、NetBIOS 和 Microsoft 客户端
```
netcfg /v /winpe
```
若要显示是否安装了组件*MS_IPX* ：
```
netcfg /q MS_IPX
```
卸载组件*MS_IPX*：
```
netcfg /u MS_IPX
```
显示所有已安装的 net 组件：
```
netcfg /s n
```
显示包含*MS_TCPIP*的绑定路径：
```
netcfg /b ms_tcpip
```
## <a name="additional-references"></a>其他参考
-   - [命令行语法项](command-line-syntax-key.md)
