---
ms.assetid: 03c82f43-ae2d-4038-b286-ae3858aed35a
title: 配置 AD FS 以发送密码过期声明
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a0c04f42cbe29b1ea36d09f1f148fb28280d7fec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859890"
---
# <a name="configure-ad-fs-to-send-password-expiry-claims"></a>配置 AD FS 以发送密码过期声明


可以配置 Active Directory 联合身份验证服务（AD FS），将密码过期声明发送到受 ADFS 保护的信赖方信任（应用程序）。 如何使用这些声明取决于应用程序。 例如，使用 Office 365 作为你的信赖方时，会将更新实施到 Exchange 和 Outlook，以通知联合身份验证用户其密码即将过期。

若要配置 AD FS 以便向信赖方信任发送密码过期声明，你必须将以下声明规则添加到此信赖方信任：

```
@RuleName = "Issue Password Expiry Claims"
c1:[Type == "https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime"]
 => issue(store = "_PasswordExpiryStore", types = ("https://schemas.microsoft.com/ws/2012/01/passwordexpirationtime", "https://schemas.microsoft.com/ws/2012/01/passwordexpirationdays", "https://schemas.microsoft.com/ws/2012/01/passwordchangeurl"), query = "{0};", param = c1.Value);
```

> [!NOTE]
> 密码到期声明仅可用于用户名和密码，以及 Microsoft Passport for Work 身份验证类型。  如果用户使用 Windows 集成身份验证进行身份验证，并且未配置 Passport，则声明将不可用，用户将看不到密码过期通知。

> [!NOTE]
> 存在14天的窗口，因此仅当密码在14天内到期时才会填充已发送的声明。

## <a name="see-also"></a>另请参阅
[AD FS 操作](../../ad-fs/AD-FS-2016-Operations.md)
