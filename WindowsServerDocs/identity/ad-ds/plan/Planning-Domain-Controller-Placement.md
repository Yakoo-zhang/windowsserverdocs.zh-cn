---
ms.assetid: 692bd2af-deee-44cf-9af9-f364677e267f
title: 规划域控制器放置
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 784e26a1762e8950b8f658ea32968a0d170df13d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822180"
---
# <a name="planning-domain-controller-placement"></a>规划域控制器放置

>适用于：Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

收集了将用于设计站点拓扑的所有网络信息后，请规划要在何处放置域控制器，包括林根域控制器、区域域控制器、操作主机角色持有者和全局编录服务器。  
  
在 Windows Server 2008 中，还可以利用只读域控制器（Rodc）。 RODC 是一种新类型的域控制器，它承载 Active Directory 数据库的只读分区。 除帐户密码之外，RODC 保存了可写域控制器所保留的所有 Active Directory 对象和属性。 但是，不能对存储在 RODC 上的数据库进行更改。 更改必须在可写域控制器上进行，然后复制回 RODC。  
  
RODC 主要用于在远程或分支机构环境中部署，这通常是相对较少的用户、物理安全性差、中心站点的网络带宽相对较差的人员，以及具有有限信息技术（IT）知识的人员。 部署 Rodc 会提高安全性并更有效地访问网络资源。 有关 RODC 功能的详细信息，请参阅 AD DS：只读域控制器（[https://go.microsoft.com/fwlink/?LinkID=106616](https://go.microsoft.com/fwlink/?LinkID=106616)）。 有关如何部署 RODC 的详细信息，请参阅只读域控制器的循序渐进指南（[https://go.microsoft.com/fwlink/?LinkID=92728](https://go.microsoft.com/fwlink/?LinkID=92728)）。  
  
> [!NOTE]  
> 本指南不说明如何确定每个站点中每个域的正确数量的域控制器和域控制器硬件要求。  
  
## <a name="in-this-section"></a>本部分内容  
  
-   [规划目录林根级域控制器放置](../../ad-ds/plan/Planning-Forest-Root-Domain-Controller-Placement.md)  
  
-   [规划区域域控制器放置](../../ad-ds/plan/Planning-Regional-Domain-Controller-Placement.md)  
  
-   [规划全局编录服务器放置](../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md)  
  
-   [规划操作主机角色放置](../../ad-ds/plan/Planning-Operations-Master-Role-Placement.md)  
  


