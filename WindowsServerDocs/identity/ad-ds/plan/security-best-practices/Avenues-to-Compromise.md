---
ms.assetid: d7a4d2e1-217d-4ffc-93f0-817149bd9e7f
title: "危害的途径"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 149a3e4bb2ce4558e40425e42ecfdeec2c5dfcb7
ms.sourcegitcommit: 78d8839ccafa9530784cb9e38c3127ed2c215423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2018
---
# <a name="avenues-to-compromise"></a>危害的途径

>适用于：Windows Server 2016，Windows Server 2012 R2、Windows Server 2012

*法律编号七： 最安全网络是一个管理完善。* - [10 变的法律的安全管理](https://technet.microsoft.com/library/cc722488.aspx)  
  
在遇到灾难危害的事件的组织中，评估通常展现出的组织有深入其 IT 基础结构，这可能大幅不同从其"述"状态的实际状态受到限制。 这些差异引入公开危害，通常以小的风险，直到危害所处的位置到该处攻击者有效"拥有"环境点的发现的环境中的漏洞。  
  
这些组织的广告 DS 配置、 公共基础结构 (Pki)、 服务器、 工作站、 应用程序的详细的评估访问 acl)，和其他技术显示错误配置和，如果修正，可能已阻止初始危害的漏洞。  
  
分析 IT 文档、 进程，并过程识别引入了利用攻击者最终获得完全破坏 Active Directory 森林所用的权限的管理实践中的缺陷漏洞。 完全受到威胁的森林是权限的一攻击者会危及不仅个别系统、 应用程序或用户帐户，但提升他们的访问权限，可以获取级别，它们可以修改或销毁森林中的所有方面。 当 Active Directory 安装已受到威胁到程序度数，攻击者可做出更改，使其保持在整个环境中，或者更糟糕，销毁目录和系统它管理的帐户存在。  
  
虽然数量遵循的说明中通常利用的漏洞的不是对 Active Directory 攻击，它们允许攻击者建立一席之地可用于运行特权提升 （也称为特权提升） 攻击和最终目标，并且危及广告 DS 的环境中。  
  
此部分中的本文重点介绍描述攻击者通常使用访问的基础结构，并且最终启动特权提升攻击机制。 请参阅以下各部分：  
  
-   [减少 Active Directory 攻击 Surface](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)详细安全的 Active Directory 配置的建议。  
  
-   [监视 Active Directory 的迹象危害](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)建议，以帮助检测危害  
  
-   [危害规划](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)高级的方法有助于对从的基础结构攻击准备 IT 和业务风景  
  
> [!NOTE]  
> 尽管本文重点属于广告 DS 域的 Active Directory 和 Windows 系统，攻击者很少重点单独 Active Directory 和窗口。 具有的操作系统、 目录、 应用和数据存储库维护混合环境，很常见查找非 Windows 系统也受到威胁。 这是如果系统提供的"桥"Windows 和非 Windows 环境之间如由 Windows 和 UNIX 或 Linux 客户端，提供了多个操作系统，身份验证服务的目录或同步的数据，跨不同类型目录的元目录访问文件服务器，尤其如此。  
>   
> 广告 DS 为目标，因为它提供了向 Windows 系统，但其他客户端的集中式访问和配置管理功能。 目录或提供身份验证和配置管理服务的应用程序可，并将定向确定攻击者。 尽管本文重点关注可以减少的可能性危及 Active Directory 安装，包括非 Windows 计算机的每一个组织的安全的保护功能目录、 应用程序或数据存储库维护还应准备针对这些系统的攻击。  
  
## <a name="initial-breach-targets"></a>初始违反目标  
没有人有意版本公开危害的组织的 IT 基础结构。 当首次构造 Active Directory 森林时，通常是原生态和当前。 在年传递和获取新的操作系统和应用程序时，它们会将其添加到森林。 识别 Active Directory 提供的可管理性权益，如越来越多的内容添加到的目录，更多人与广告 DS 集成其计算机或应用程序和升级的域的支持 Windows 操作系统的最新版本中提供的新功能。 但是，还时发生随着时间的推移是，即使在新的基础结构是要添加的基础结构的其他部分可能不会以及它们最初保留、 系统和应用程序正在正常运行，因此未受到注意后组织开始忘记了他们不消除了他们传统的基础结构。 根据我们在评估受到威胁的基础结构的看到较旧，更大，并更复杂环境，更有可能已有的常用利用的漏洞的大量实例。  
  
攻击者的动机，无论大多数信息的安全漏洞一次启动的一个或两个系统损害。 这些初始事件或入口点到网络中，通常利用的漏洞可能已修复，但并非。 [2012年数据违反调查报告 (DBIR)](http://www.verizonbusiness.com/resources/reports/rp_data-breach-investigations-report-2012_en_xg.pdf)，这是产生 Verizon 风险团队中的许多国家安全机关和其他公司合作的一年研究，指出 96%的攻击已"不高度很困难，"和"的违规 97%了避免通过简单或中间控件。" 这些发现可能会经常利用的漏洞遵循直接后果。  
  
### <a name="gaps-in-antivirus-and-antimalware-deployments"></a>在防病毒和恶意软件部署间距  
*法律编号八： 过期的恶意软件的扫描程序在所有才略微比没有扫描仪更好。* - [十变法律规定，，安全 （2.0 版本）](https://technet.microsoft.com/security/hh278941.aspx)  
  
分析的组织的防病毒和恶意软件部署通常显示在其中环境大多数工作站配置已启用的防病毒和恶意软件和当前。 例外情况是通常工作站为企业环境或员工的设备上的防病毒和恶意软件的软件可能很难部署、 配置和更新不频繁连接。  
  
服务器人口，但是，倾向于小于持续保护许多受到威胁的环境中。 报告中[2012年数据违反调查](http://www.verizonbusiness.com/resources/reports/rp_data-breach-investigations-report-2012_en_xg.pdf)、 的所有数据 %到 94%损害涉及到的服务器，这表示 18%增加以前年和的攻击 69%合并恶意软件。 在服务器人口不比比皆是防病毒和恶意软件安装是一致配置、 过时、 错误配置的或即使禁用。 在某些情况下，防病毒和恶意软件禁用通过管理人员，但在其他情况下，攻击者禁用该软件危及其他漏洞通过服务器后。 禁用防病毒和恶意软件时，攻击者然后植物在服务器上的恶意软件和重点关注服务器总体传播泄露。  
  
很重要不仅以确保你的系统都设有当前、 全面的恶意软件保护，但也监视系统禁用或删除防病毒和恶意软件并手动禁用后自动重启保护。 虽然防护和检测到的所有的感染，可以保证没有防病毒和恶意软件，正确配置，并且部署防病毒和恶意软件实现可以减少的可能性感染。  
  
### <a name="incomplete-patching"></a>不完整的修补程序  
*法律第三步： 如果您不赶上安全修补程序，你的网络不会将你的个性长时间。* - [10 变的法律的安全管理](https://technet.microsoft.com/library/cc722488.aspx)  
  
Microsoft 会发布安全公告每月的第二个星期二尽管极少数情况下的安全更新发布的每月的安全更新 （如下所示也称为"带"更新） 之间当漏洞确定会造成紧急的风险来客户系统。 还是一家小型企业配置其 Windows 的计算机使用 Windows 更新管理系统和应用程序的修补大型组织用于管理软件系统中心配置管理器 (SCCM) 如部署根据详细、 分层套餐的修补程序，许多客户修补相对及时程序其 Windows 基础结构。  
  
但是，一些基础结构包括只能 Windows 的计算机和 Microsoft 应用程序，并且在受到威胁的环境，很常见查找组织的修补程序管理策略包含缺陷。 这些环境中的 Windows 系统一致应用修补程序。 如果根本，偶尔，修补非 Windows 操作系统。 商业现成 (COTS) 应用程序包含的漏洞为其修补程序存在，但尚未应用。 网络设备通常配置具有出厂默认凭据和没有固件更新后他们安装年。 应用程序，但通常保持及其供应商通过不再受支持的操作系统运行的，尽管它们可以不再进行修补针对漏洞。 每个这些修补程序的系统表示攻击者其他潜在的入口点。  
  
消费 IT 该员工中引入的其他难题拥有使用设备访问附属公司的数据，并的组织可能有一些到任何控制修补并配置员工的个人设备。 企业级的硬件通常附带面向企业配置选项和管理功能，但在单独的自定义和设备选择较少选择。 侧重于员工的硬件提供更广泛各种制造商、 供应商、 硬件安全功能、 软件的安全功能、 管理功能和配置选项，并许多企业功能完全可能不存在。  
  
#### <a name="patch-and-vulnerability-management-software"></a>修补程序和漏洞管理软件  
如果 Windows 系统和 Microsoft 应用程序有效的修补程序管理系统，已得到解决未安装修补程序的安全漏洞创建攻击 surface 的一部分。 但是，除非非 Windows 系统、 非 Microsoft 应用程序、 网络基础结构和员工的设备也会保持最新的修补程序和其他修补程序，仍然易受攻击的基础结构。 在某些情况下，应用程序供应商可能会提供自动更新功能。在其他应用，可能需要设计定期检索和应用的修补程序和其他修复方法。
  
### <a name="outdated-applications-and-operating-systems"></a>过期的应用和操作系统  
*"无法预计六个岁的操作系统保护你防御的六个月久攻击。"* -信息安全专业版的 10 年的体验固定企业版安装  
  
尽管"获取当前、 保持最新"听起来营销短语、 过期的操作系统和应用程序创建的风险，在许多组织 IT 基础结构。 操作系统，发布 2003年可能仍受供应商和随附地址漏洞的更新，但该操作系统不可能包含在较新版本的操作系统中添加了安全功能。 过期的系统甚至可以要求弱化的某些广告 DS 安全配置，以支持这些计算机的小功能。  
  
不能 retooled 编写的应用程序已使用传统的身份验证的协议通过供应商可支持应用程序不会再通常支持较强的身份验证机制。 但是，组织 Active Directory 域，仍然可以配置 LAN Manager 哈希或可逆加密的密码，以支持此类应用程序存储。 编写之前更高版本操作系统引入的应用程序可能无法正常或根本当前在操作系统上，需要组织维护旧和较早的系统，并且在某些情况下，完全不受支持的硬件和软件。  
  
即使在组织已更新到 Windows Server 2012、 Windows Server 2008 R2 或 Windows Server 2008 其域控制器的情况下，它是典型发现该成员的重要部分服务器人口运行 （这是不会再在主要支持） 的 Windows Server 2003，甚至 Windows 2000 Server 或 Windows NT 服务器 4.0 （这不完全受支持）。 组织维护老化系统的时间越长，此功能集之间的差异的发展越多，并越有可能成为生产系统将不受支持。 此外的时间越长维护 Active Directory 森林，越多，我们观察传统系统和应用程序错过了升级的套餐中。 这可能表示一台运行一个应用程序可能会引入域或树林漏洞，因为 Active Directory 配置为支持它的传统协议和机制身份验证。  
  
若要消除旧版系统和应用程序，应首先重点识别和对它们进行分类，然后确定是否升级或替换该应用程序或主机上。 虽然它可能很难找到更换非常专业的应用程序将简支持以及的升级路径，你可能能够充分利用称为"创意销毁"的概念替换旧版应用程序与新提供的应用程序所需功能。 [危害规划](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)"规划危害"在本文后面的更多深度中所述。  
  
### <a name="misconfiguration"></a>错误配置  
*法律数字四： 它不会执行多良好安装根本保护开头的计算机上的安全修复。* - [10 变的法律的安全管理](https://technet.microsoft.com/library/cc722488.aspx)  
  
即使是在系统通常保存当前和修补环境中，我们通常识别缺陷或操作系统，错误配置计算机和 Active Directory 上运行的应用程序。 一些错误配置公开仅在本地计算机在实施侵害时，，但一台计算机"拥有后，"攻击者通常重点关注进一步传播危害最终跨其他系统以及 Active Directory。 以下是一些常见的区域，在其中我们找出带来的风险的配置。  
  
#### <a name="in-active-directory"></a>Active Directory 中  
最常进行针对性投放攻击者 Active Directory 中的帐户那些成员的最高权限的组中，如域管理员 (DA)、 企业版管理员 (EA) 或内置管理员 （栏） 组 Active Directory 中的成员。 应帐户可能的最小号码减少的这些组成员资格，以便限制攻击的这些组。 甚至可以以消除"永久"会员在这些权限的组。也就是说，可以实现设置允许你只需要及其域和树林权限时，临时填充这些组。 当使用帐户高权限时，他们应指定、 安全如域控制器或安全管理主机的系统上使用。 中提供了详细的信息，以帮助实现所有这些配置[减少 Active Directory 攻击 Surface](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)。  
  
当我们评估的 Active Directory 中最高权限的组成员资格时，我们通常三个最特权组查找过多的会员。 在某些情况下，组织提供了多种，甚至数百 DA 组中的帐户。 在其他情况下，组织放在帐户直接内置管理员组，考虑该组"不太特权"比 DAs 组。 不存在。 我们通常在森林根域，尽管 EA 权限很少和暂时所需找到一些永久 EA 组成员。 在这三组中查找 IT 用户日常管理帐户也很常见，尽管这是一个有效地冗余配置。 中所述[减少 Active Directory 攻击 Surface](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)、 帐户是否的其中一个部分或全部，永久成员的帐户可用于影响，以及甚至会破坏广告 DS 环境和系统由该帐户。 安全配置并使用 Active Directory 中特权帐户的建议中提供了[减少 Active Directory 攻击 Surface](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)。  
  
#### <a name="on-domain-controllers"></a>域控制器上  
当我们评估的域控制器，我们通常查找查找他们配置，并且不不同成员服务器管理。 有时，域控制器运行相同的应用程序和不是因为，域控制器上需要在它们，但的应用标准生成的一部分安装在成员服务器上的实用工具。 这些应用程序可能会提供了域控制器上的最小功能，但通过要求打开端口、 创建高权限的服务帐户、 或授予访问系统应连接到域控制器用于任何目的以外身份验证和组策略应用程序的用户配置设置显著添加到其攻击 surface。 在某些侵害，攻击者已使用域控制器不仅访问域控制器，但修改或损坏广告 DS 数据库已经安装的工具。  
  
当我们提取域控制器上的 Internet Explorer 配置设置时，我们发现，用户已与具有很高的 Active Directory 中特权并已使用帐户访问来自域控制器的 Internet 连接和 intranet 的帐户登录。 在某些情况下，帐户以允许 Internet 下载的内容，域控制器上配置 Internet Explorer 设置，并免费软件已从 Internet 站点下载和上的域控制器安装。 Internet Explorer 增强的安全配置为用户和管理员已启用默认情况下，但我们通常观察前提是已禁用的管理员。 当高权限的帐户访问 Internet 和下载内容的任何计算机时，该计算机是危及严重。 计算机时域控制器，整个广告 DS 安装是危及。  
  
##### <a name="protecting-domain-controllers"></a>保护域控制器  
应视为基础结构的关键组件、 进一步保护和配置文件、 打印和应用程序服务器比严格域控制器。 域控制器不应运行不需要的域控制器函数到或无法保护受攻击的域控制器的任何软件。 域控制器不应能访问 Internet 时，并且应配置和由组策略对象 (Gpo) 实施安全设置。 中提供了详细的建议安全安装、 配置和管理域控制器[针对攻击保护域控制器](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)。  
  
#### <a name="within-the-operating-system"></a>在操作系统  
*法律第二： 如果攻击者可以更改你的计算机上的操作系统，它不是你的计算机不再。* - [十变法律规定，，安全 （2.0 版本）](https://technet.microsoft.com/security/hh278941.aspx)  
  
虽然有些组织创建基准配置为服务器不同类型的并安装后允许有限的自定义的操作系统，受到威胁的环境的分析通常揭示大量服务器特殊的方式部署和配置手动和独立。 执行相同的功能的两个服务器之间配置可能完全不同，均不得服务器已牢固配置的位置。 相反，可能会始终强制，但还始终错误配置的; 服务器配置基线创建给定类型的所有服务器上的同一漏洞的方式，即配置服务器。 错误配置包括做法如禁用显示器的安全功能、 授予过多的权利和帐户 （尤其是服务） 的权限时，使用相同的本地凭据跨系统，并允许安装的未经授权的应用程序和创建自己的安全漏洞的实用工具。  
  
##### <a name="disabling-security-features"></a>禁用显示器的安全功能  
组织有时会利用 WFAS 很困难配置，或需要工作密集型配置相信禁用 Windows 防火墙与高级安全 (WFAS)。 但是，开始与 Windows Server 2008、 服务器上安装了任何作用或功能时，默认情况下所需的功能正常工作的角色的最低特权配置 Windows 防火墙自动配置支持角色或功能。 通过禁用显示器的 WFAS （和不使用在其位置的另一台主机基于防火墙） 组织增加攻击的整个 Windows 环境。 周边防火墙提供了一些防御直接目标从 Internet 上的环境的攻击但提供没有防御如利用其他攻击方法攻击[驱动器通过下载](https://www.microsoft.com/security/sir/glossary/drive-by-download-sites.aspx)攻击或从其他来源的攻击威胁上的 intranet 系统。  
  
在服务器上的用户帐户控制 (UAC) 设置有时禁用，因为管理人员查找提示干扰。 尽管[Microsoft 支持文章 2526083](https://support.microsoft.com/kb/2526083)除非你正在运行的服务器核心安装 （其中 UAC 禁用设计），您应该仔细考虑和研究没有的服务器上禁用 UAC 描述 UAC 可能禁用 Windows 服务器的方案。  
  
在其他情况下，服务器设置配置为不太安全值，因为组织将过期的服务器配置设置应用到新的操作系统，如将应用到计算机，而无需更改基线以反映这些更改操作系统中的运行 Windows Server 2012、 Windows Server 2008 R2 或 Windows Server 2008、 Windows Server 2003 基准。 而不是为了实现旧服务器基线到新的操作系统，当部署新的操作系统，请查看安全更改和配置设置，以确保实现的设置都适用和适用于新的操作系统。  
  
##### <a name="granting-excessive-privilege"></a>授予过多的权限  
在我们有评估几乎每个环境过多特权授予 Windows 系统上的当地的和基于域帐户。 用户授予其工作站上的本地管理员权限成员服务器运行配置使用超出需要函数，权限的服务，服务器总体的本地管理员组包含多种或甚至本地数百和域帐户。 只有一个特权的帐户的计算机上的危害允许攻击者损害每个用户和服务，可向计算机中，以及传播到其他系统破坏的秋分并充分利用凭据登录的帐户。  
  
尽管 pass--哈希 (PTH) 和其他凭据盗窃攻击普遍今天，是因为使变得简单的免费工具，并且易于解压缩的时攻击其他特权帐户凭据有权管理员或系统级别的计算机。 即使没有允许窃取凭据登录会话中的工具，使用计算机的访问权限的攻击轻而易举安装捕获按键、 屏幕截图和剪贴板上的内容的击键记录器。 使用计算机的访问权限的攻击可以禁用反恶意软件，安装 rootkit、 修改受保护的文件或自动化攻击或会到服务器的计算机上安装恶意软件[驱动器通过下载](https://www.microsoft.com/security/sir/glossary/drive-by-download-sites.aspx)主机。  
  
用于扩展到一台计算机违反策略各不相同，但传播危害的关键高权限访问其他 systems 的购买。 通过任何系统减少帐户的访问权限的数量，减少不仅的计算机，但攻击搜集有价值的凭据，从计算机的可能性攻击 surface。  
  
##### <a name="standardizing-local-administrator-credentials"></a>标准化本地管理员凭据  
重命名 Windows 的计算机上的本地管理员帐户中是否有值，长已之间安全专家作为多的讨论。 有关本地管理员帐户实际上重要的是是否它们跨多台计算机配置的相同用户名和密码。  
  
如果为相同的值还配置了分配给该帐户的密码的本地管理员帐户名为为相同的值跨服务器，攻击者可解压缩上一台计算机的管理员或系统级别获得访问该帐户凭据。 攻击者没有最初危害的本地管理员帐户。他们只能需要危及是成员本地，或配置运行本地或具有管理员权限的服务帐户的用户帐户。 攻击者可提取管理员帐户凭据，然后重播这些网络登录到该网络上的其他计算机中的凭据。  
  
只要另一台计算机已使用的相同用户名和密码 （或密码希） 作为正在提供帐户凭据本地帐户，登录尝试成功和攻击者获得授权的访问到目标计算机。 内置的管理员帐户中的 Windows 当前版本中，已[默认禁用](https://technet.microsoft.com/library/cc753450.aspx)，但在旧操作系统，默认情况下启用了帐户。  
  
> [!NOTE]  
> 某些组织有意配置了这将提供在所有其他特权的帐户锁定系统的情况下"安全模式"在以下情况中启用的本地管理员帐户。 但是，即使没有其他帐户提供，可启用帐户或登录到具有管理员权限的系统已禁用的本地管理员帐户，系统可启动到安全模式和内置的本地管理员帐户可以重新启用，述[Microsoft 支持文章 814777](https://support.microsoft.com/kb/814777)。 此外，如果系统成功仍然适用 Gpo，GPO 可以进行修改以 （暂时） 重新启用管理员帐户，或受限制的组可以配置为基于域帐户添加到本地。 可以执行的修复和可以再次禁用的管理员帐户。 以防有效地使用内置的本地管理员帐户凭据横向危害，唯一的用户名和密码必须配置的本地管理员帐户。 若要部署通过 GPO 的本地管理员帐户的唯一的密码，请参阅[管理通过 GPO 内置管理员帐户的密码的解决方案](https://technet.microsoft.com/mt227395.aspx)technet 上。  
  
##### <a name="permitting-installation-of-unauthorized-applications"></a>允许安装未经授权的应用程序  
*法律的第一部分： 如果攻击者可诱骗你在计算机上运行他的程序，不只是你的计算机不再。* - [十变法律规定，，安全 （2.0 版本）](https://technet.microsoft.com/security/hh278941.aspx)  
  
是否组织跨服务器部署一致基准设置，应不允许的应用程序不属于服务器的定义角色进行安装。 通过允许安装不是软件服务器指定功能的一部分，服务器面临意外或恶意安装增加服务器攻击 surface、 引入了应用程序漏洞或导致系统不稳定的软件。  
  
#### <a name="applications"></a>应用程序  
如上文所述，应用程序经常安装和配置为使用的帐户被授予实际上需要更多高于应用程序的权限。 在某些情况下，应用程序的文档指定 service 帐户必须服务器的本地管理员组成员或必须配置本地系统上下文中运行。 这通常是不是因为该应用程序需要这些权利，但因为确定哪些的权利和权限应用程序的服务的帐户需要需要额外的时间和精力投资。 如果未安装最低权限才能正常的应用程序和其配置的功能所需的应用程序，系统可以充分利用应用权限，没有任何攻击操作系统本身的攻击。  
  
### <a name="lack-of-secure-application-development-practices"></a>缺少的安全的应用程序开发做法  
支持企业工作负载而存在的基础结构。 这些工作负载实现中自定义应用程序时，很重要以确保使用安全的最佳实践开发应用程序。 企业级事件的根本原因分析通常显示初始危害通过自定义受影响的应用程序-尤其是 Internet 面对。 可以通过危害的已知攻击如 SQL 插入 (SQLi) 来完成这些危害的大多数和跨网站脚本 (XSS) 攻击。  
  
SQL 插入是允许用户定义的反馈进而修改传递到数据库用于执行的 SQL 声明的应用程序漏洞。 可以通过应用程序、 （如查询字符串或 cookie），参数或其他方法的字段中提供此输入。 此插入结果是从根本上不同于哪些适用的开发人员提供给数据库 SQL 声明。 例如，需要在用户名/密码组合评估普通查询：  
  
`SELECT userID FROM users WHERE username = 'sUserName' AND password = 'sPassword'`  
  
当收到时数据库服务器时，它指示通过用户表查找，然后返回的任何用户 Id 记录其中用户名和密码相符 （大概通过的某些类型的窗体登录） 的用户提供的服务器。 自然开发人员在此情况下旨在帮助仅可由用户提供了正确的用户名和密码如果返回有效的记录。 如果任一不正确，数据库 server 将无法找到匹配记录和退还空的结果。  
  
攻击会出现一些意外如提供自己 SQL 有效的数据的位置时出现问题。 因为 SQL 解释上实时数据库服务器，就像开发人员必须将其放入自己会处理插入的代码。 例如，如果输入攻击者**管理员**的用户 id 和**xyz**或者**1 = 1**得到语句由数据库处理会密码，为：  
  
`SELECT userID FROM users WHERE username = 'administrator' AND password = 'xyz' OR 1=1`  
  
此查询处理数据库服务器时, 表中的所有行中将都返回查询 1 = 1 将始终评估为如此，从而因为它并不重要如果已知或提供正确的用户名和密码。 在大多数情况下结果是将作为第一个在用户的数据库; 用户登录的用户在大多数情况下，这将管理用户。  
  
只需登录，除了格式不正确 SQL 明细表诸如这可用于添加，请删除，或更改数据，或甚至从数据库放 （删除） 整个表。 最高的情况下 SQLi 结合过多的权限，可以运行操作系统命令以启用创建新的用户，若要下载攻击工具，或需要选择攻击者的任何其他操作。  
  
在脚本跨网站、 应用程序的输出中引入了漏洞。 攻击开头攻击提供格式不正确的数据，应用程序，但这种情况下格式不正确的数据 （如 JavaScript) 脚本将通过受害者的浏览器运行的代码的形式。 利用 XSS 漏洞可以他的攻击运行用户上下文中的任何函数目标应用程序启动浏览器。 通过诱使用户可单击的链接，连接到该应用程序，并运行攻击代码网络钓鱼电子邮件通常启动 XSS 攻击。  
  
在网上银行和商务方案攻击购物或传输利用用户的上下文中的资金的位置，通常受虐 XSS。 自定义基于 web 的标识管理应用程序有针对性攻击，如果它可以允许创建自己的身份、 修改权限，并导致系统性受损的攻击。  
  
尽管完整的脚本跨网站和 SQL 插入讨论了本文中的范围之外[打开 Web 应用程序安全项目 (OWASP)](https://www.owasp.org/index.php/Main_Page)发布齐名最高的 10 深入讨论漏洞和对策。  
  
无论为安全基础结构的投资，如果根本无法运行设计和书写的应用程序内的基础结构，部署环境进行易受攻击。 通常更完善受保护的基础结构不能提供有效的对策这些应用的攻击。 复合问题，设计根本无法运行的应用程序可能需要服务帐户被授予过多的函数为的应用程序的权限。  
  
Microsoft Security 开发生命周期 (SDL) 是一组工作来改进安全要求收集，并通过应用程序的生命周期扩展，直到它停止使用在早期的开始位置的结构过程控件。 此集成的有效的安全控件不只是关键的安全全景，非常重要，以确保应用程序的安全已成本，并计划有效。 评估应用程序的安全问题，它实际上是完成代码时需要组织仅之前，或在部署应用后，甚至使决策应用程序的安全。 可以选择将在生产，引起成本和延迟，应用部署之前地址应用程序缺陷组织或应用程序可以部署生产具有已知的安全漏洞，公开危害的组织中。  
  
某些组织放置在上面的问题，10000 美元的生产代码修复安全问题的完整成本和应用程序开发没有有效的 SDL 可以平均每 100000 的代码行多十严重问题。 在较大的应用，快升级成本。 相反，许多公司 SDL，最终代码审查阶段设置的小于 1 问题 100000 行代码的每一个基准和致力于即为零高风险生产中的应用程序中的问题。  
  
实现 SDL 通过收集要求在早期包括安全要求改进安全性和应用程序的设计提供威胁建模高风险的应用程序;需要有效培训和监控的开发人员;且一致的代码标准和做法清除，需要。 SDL 实际效果时减少开发、 部署、 维护和停止使用应用的费用是在应用程序的安全重大改进。 虽然设计详细的讨论和 SDL 实现本文档的范围之外，请参阅[Microsoft 安全开发生命周期](https://www.microsoft.com/security/sdl/default.aspx)详细的指导和信息。  
  

