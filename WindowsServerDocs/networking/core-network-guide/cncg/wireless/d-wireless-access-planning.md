---
title: 无线访问部署计划
description: 本主题介绍 Windows Server 2016 网络指南"部署密码基于 802.1 X 身份验证无线的访问"部分
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 8c632d02-2270-4a82-8fc4-74ea3747f079
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a1aa7d9fa66c480988ec7e3a97447157bd3eab9c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="wireless-access-deployment-planning"></a>无线访问部署计划

>适用于：Windows Server（半年通道），Windows Server 2016

部署无线接入之前，你必须计划以下各项：

- 安装的无线接入点 \(APs\) 网络上

- 无线客户端配置和访问

以下部分提供了有关这些规划步骤的详细信息。

## <a name="planning-wireless-ap-installations"></a>规划无线接入点安装
设计无线网络的访问权限解决方案时，你必须执行以下操作：

1. 确定哪些标准必须支持你的无线接入点
2. 确定你希望提供无线服务了解覆盖区域
3. 确定你想要查找无线接入点

此外，你必须计划的无线接入点的 IP 地址方案和无线客户端。 请参阅部分**计划的无线接入点的在 NPS 配置**下方的相关信息。

### <a name="verify-wireless-ap-support-for-standards"></a>验证针对标准的无线接入点支持
对于一致性目的，轻松部署和接入点管理建议你部署的同一品牌和型号的无线接入点。

你将其部署的无线接入点必须支持：

- **IEEE 802.1 X**

- **RADIUS 身份验证**

- **无线身份验证和密码。** 下面按顺序列出的到的大多数至少首选：

    1.  与 AES WPA2\ 企业版

    2.  与 TKIP WPA2\ 企业版

    3.  与 AES WPA\ 企业版

    4.  与 TKIP WPA\ 企业版

>[!NOTE]
>若要部署 WPA2，必须使用无线网络适配器和同样支持 WPA2 的无线接入点。 否则，请使用 WPA\ 企业。

此外，该网络提供增强的安全性，无线接入点必须支持以下安全选项：

- **DHCP 筛选。** 无线接入点必须筛选 IP 端口以防止传输 DHCP 广播邮件在这些情况下，在其中无线客户端配置为 DHCP 服务器上。 无线接入点，必须阻止从 UDP 端口 68 IP 数据包发送到该网络的客户端。

- **DNS 筛选。** 必须筛选 IP 端口以防止客户端作为 DNS 服务器执行无线接入点。 无线接入点必须阻止客户端发送 IP 数据包 TCP 或 UDP 从端口延长 53 到该网络。

- **客户端隔离**如果你的无线接入点提供客户端隔离功能，你应启用防止可能地址分辨率协议 \(ARP\) 欺骗的手段该功能。

### <a name="identify-areas-of-coverage-for-wireless-users"></a>标识为无线用户覆盖率的区域
使用每个楼层有关每个构建建筑的绘图找出你希望提供无线覆盖率的区域。 例如，识别出相应办公室、会议房间、大厅、咖啡店或 courtyards。

上绘图，表示任何干扰无线信号，如医疗设备、无线的视频摄像机、在 2.4 GHz 行业、科学型和医疗 \(ISM\) 范围 2.5，通过运行的无绳电话的设备，并且 Bluetooth\ 启用的设备。

在绘图，标记方面的可能会影响无线信号; 建筑一座构建中使用的金属物体可能会影响中无线信号。 例如，以下常见对象可能会影响与信号传播：电梯家供暖和 air\ 调节管道，具体支持 girders。

请参考你的接入点制造商以了解可能会导致的无线接入点射频衰减的来源。 大多数 Ap 提供测试可用于检查信号强度、错误率和数据吞吐量的软件。

### <a name="determine-where-to-install-wireless-aps"></a>确定安装无线接入点的位置
在建筑的绘图，找到你的无线接入点关闭足够在一起，他们不会干扰彼此与众不同提供充裕无线但远足够的覆盖范围。

之间接入点的必要距离取决于接入点的类型和接入点天线，阻止构建方面无线信号，并且其他来源的干扰。 你可以标记无线接入点的位置，以便每个无线接入点不超过 300 英尺从任何旁边的无线接入点。 请参阅有关接入点规格的无线接入点制造商提供的文档和位置的指南。

暂时安装在你的体系结构绘图上指定的位置的无线接入点。 然后，使用的是笔记本电脑配备 802.11 的无线适配器和通常提供该站点调查软件无线适配器，确定在每个覆盖范围内的信号强度。

在了解覆盖区域了信号强度较低，以改进覆盖区域的信号强度，请安装额外的无线接入点提供必要覆盖率、调动或删除源的信号干扰接入点的位置。  

更新你的体系结构绘图指示最终所有的无线接入点的位置。 有准确的接入点放置地图有助于诊断操作期间稍后或你想要升级或更换接入点。

### <a name="plan-wireless-ap-and-nps-radius-client-configuration"></a>套餐的无线接入点和 NPS RADIUS 客户端配置
你可以使用 NPS 配置单独或组中的无线接入点。

如果你正在部署较大的无线网络，其中包括许多接入点，很更加容易配置 Ap 组中。 若要在 NPS RADIUS 客户端组作为添加接入点，必须具有这些属性配置接入点。

- 无线接入点配置了从同一 IP 地址范围的 IP 地址。

- 所有都使用相同的共享机密配置无线接入点。

### <a name="plan-the-use-of-peap-fast-reconnect"></a>计划 PEAP Fast 重新连接的使用
在 802.1 X 基础结构，无线接入点配置为 RADIUS RADIUS 服务器的客户端。 部署时 PEAP fast 重新连接时，两个或多个访问点之间漫游无线客户端不需要进行身份验证的每个新关联。

重新连接 PEAP 快速因为身份验证请求最初执行身份验证和授权的客户端连接请求 NPS 服务器转发从新的访问点，减少了之间客户端和验证器身份验证的响应时间。

因为 PEAP 客户端和都使用以前的 NPS 服务器缓存传输层安全性 \(TLS\) 连接属性 \（它的集锦名为 TLS handle\）、NPS 服务器快速确定客户端授权重新连接。

>[!IMPORTANT]
>为 fast 重新连接才能正常工作，必须为 RADIUS 服务器客户的相同 NPS 配置接入点。

如果原始 NPS 服务器不变为可用，或进入配置为 RADIUS 客户端到不同的 RADIUS 服务器接入点的客户端，身份验证的全屏必须发生客户端和新 authenticator 之间。

### <a name="wireless-ap-configuration"></a>无线接入点配置
下面总结了通常配置 802.1X\ 上的项目的支持的无线接入点：

> [!NOTE]
> 项目名称因品牌和型号，并且可能不同于下面的列表。 请参阅 configuration\ 特定的详细信息无线接入点的文档。

- **服务设置标识符 \(SSID\)**。 这是无线网络的名称 \ (例如，ExampleWlan\) 和公布到无线客户端的名称。 为了减少混乱，选择要向你推荐的 SSID 应不匹配通过任何接收你的无线网络范围内的无线网络广播 SSID。

    在多个的无线接入点为相同的无线网络的一部分在其中的部署的情况下，为每个无线接入点配置相同 SSID。 在多个的无线接入点为相同的无线网络的一部分在其中的部署的情况下，为每个无线接入点配置相同 SSID。  

    在你需要部署满足特定的企业需要不同无线网络的情况下，您无线接入点的上一个网络应广播比 SSID 你其他 network\(s\) 不同 SSID。 例如，如果你为你的员工和来宾需要单独的无线网络，你可以配置的企业网络你无线接入点具有 SSID 设置为广播**ExampleWLAN**。 为你的访客网络，然后，你可能设置每个无线接入点 SSID 广播**GuestWLAN**。 这样你的员工和来宾可以连接到不必要的有条不紊地预期网络。  

    > [!TIP]  
    > 一些无线接入点都有广播多个 SSID 的可以容纳 multi\ 网络部署的能力。 无线接入点的程序可以使用多个 SSID 广播参加可以减少部署和运营维护成本。  

- **无线身份验证和加密**。

    无线身份验证是与无线接入点关联无线客户端时使用安全验证。  

    无线加密是用于无线身份验证来保护之间无线接入点和无线客户端发送通信安全加密密钥。  

- **无线接入点的 IP 地址 \(static\)**。 在每个无线接入点，将配置唯一的静态 IP 地址。 如果子网 DHCP 服务器由提供服务，请确保，以便不会尝试到另一台计算机或设备发布的同一 IP 地址 DHCP 服务器的所有 AP IP 地址都位于 DHCP 排除项范围内。 在"来创建和激活新 DHCP 范围"的过程中记录排除范围[Core 网络指南](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide)。 如果你打算配置为由组中 NPS RADIUS 客户端的接入点，每个组中的点击必须从同一 IP 地址范围 IP 地址。

- **DNS 名称**。 可以与 DNS 名称配置某些无线接入点。 为每个无线接入点配置一个唯一的名称。 例如，如果你在 multi\ 故事构建有部署的无线接入点，你可能命名前三个的无线接入点上的第三个楼层 AP3\ 01、AP3\ 02 和 AP3\ 03 部署。

- **无线接入点子网掩码**。 配置掩码，若要指定 IP 的哪个部分地址是网络 ID 和 IP 地址的部分是主机。

- **点击 DHCP 服务**。 如果你的无线接入点都有 built\ 中 DHCP 服务，请将其禁用。

- **RADIUS 共享的密钥**。 使用唯一 RADIUS 幽静分享的每个无线接入点，除非你打算配置中组-在的情况下必须将配置为所有组中的接入点的共享机密 NPS RADIUS 客户端。 共享的机密应该至少 22 字符多长时间，同时大写与随机序列、小写字母、数字和标点符号。 若要确保随机，可以使用随机字符生成程序创建你共享的机密信息。 建议你录制共享的机密的每个无线接入点，并将其存储在安全位置，如 office 安全。 RADIUS 客户端配置中 NPS 主机时，您将创建虚拟每次接入点的版本。 你在每个 NPS 中的虚拟接入点配置共享的幽静必须匹配实际、物理接入点上的共享的机密。

- **RADIUS 服务器 IP 地址**。 键入你想要用于验证和授权连接到此接入点的请求 NPS 服务器的 IP 地址。

- **UDP port\(s\)**。 默认情况下，NPS RADIUS 身份验证消息和 UDP 端口 1813 年和 RADIUS 会计消息的 1646 年使用 1812 年和 1645 UDP 端口。 请勿更改默认 RADIUS UDP 端口设置建议。

- **Vsa**。 一些无线接入点需要 vendor\ 特定于属性 \(VSAs\) 提供完全的无线接入点的功能。

- **DHCP 筛选**。 将阻止无线将 IP 数据包从 UDP 端口 68 发送到该网络的客户端的无线接入点的配置。 查看你的无线接入点配置 DHCP 筛选的文档。

- **DNS 筛选**。 将阻止无线将 IP 数据包从 TCP 或 UDP 端口延长 53 发送到该网络的客户端的无线接入点的配置。 查看你的无线接入点配置 DNS 筛选的文档。

## <a name="planning-wireless-client-configuration-and-access"></a>计划无线客户端配置和访问

在规划的 802.1X\ 部署-经过身份验证的无线接入，必须考虑以下几个 client\ 特定因素：

- **计划支持多个标准**。

    确定是否无线计算机都使用相同版本的 Windows 或它们是否计算机运行的其他操作系统的组合。 它们是否不同，请确保你了解任何标准受支持的操作系统的差异。

    确定是否无线网络适配器上的所有无线客户端计算机的所有支持相同无线标准版，或是否需要支持不同标准。 例如，确定某些网络适配器的硬件驱动程序在而其他支持只有 WPA\ 企业版和 TKIP 支持 WPA2\ 企业版和 AES。

- **计划的客户端身份验证模式**。 身份验证模式定义 Windows 客户端如何处理域的凭据。 你可以选择从以下三个网络身份验证模式无线网络策略中。  

    1. **用户身份验证 re\**。 该模式是指身份验证始终执行通过安全凭据根据计算机的当前状态。 没有用户在登录到计算机，身份验证方法是使用计算机的凭据。 用户在登录到计算机，始终使用凭据用户执行身份验证。  

    2. **只有计算机**。 计算机模式是指身份验证仅已始终使用执行仅计算机凭据。  

    3.  **用户身份验证**。 用户身份验证模式是指身份验证时才会执行用户在登录到计算机时。 当有未登录该计算机的用户时，不会执行身份验证尝试。  

- **计划无线限制**。 确定是否想要为所有用户无线提供相同级别的访问你的无线网络，或者你是否希望限制访问你的无线用户的某些。 你可以将应用针对特定的无线用户组中 NPS 限制。  例如，你可以定义特定天和几个小时某些组获准无线网络的访问权限。  

- **计划添加新无线计算机方法**。 对于加入的域之前部署你的无线网络，如果计算机连接到有线网络，不受 802.1 X 的一段 wireless\ 支持的计算机，无线配置设置将自动应用后，您将配置无线网络 \ (IEEE 802.11\) 策略该域控制器上和无线客户端上刷新组策略。  

    对于未已加入域到的计算机，但是，你必须计划的方法以应用设置所需的 802.1X\-身份验证的访问权限。 例如，确定是否想要加入的域通过以下方法之一计算机。

    1.  将计算机连接到有线由 802.1 X，不受保护的网络的一段，然后加入域的计算机。

    2.  你的无线用户提供的步骤和他们需要在添加自己无线启动配置文件，这使他们加入域的计算机的设置。

    3.  指定 IT 人员加入域的无线客户端。

### <a name="planning-support-for-multiple-standards"></a>计划对多个标准的支持

无线网络 \ (IEEE 802.11\) 策略扩展在组策略中的提供的各种配置选项，以支持的各种部署选项。

你可以部署配置与你想要支持，标准的无线接入点，然后配置无线网络中的多个无线配置文件 \ (IEEE 802.11\) 策略，每个配置文件的标准，你需要指定的一组。

例如，如果你的网络已无线支持 WPA2\ 企业版和 AES，支持 WPA\ 企业版和 AES 的其他计算机和支持仅 WPA\ 企业版和 TKIP 的其他计算机的计算机必须确定是否要：

- 配置单个配置文件支持的所有无线计算机使用弱加密方法，你的计算机的所有支持-在此情况下，WPA\ 企业和 TKIP。  
- 配置两配置文件来提供支持的每个无线计算机最佳可能的安全。 在这种情况，你会配置一个指定最强的加密的个人资料 \（WPA2\ 企业和 AES\）和一个使用较弱的 WPA\ 企业和 TKIP 加密的配置文件。 在此示例中，它至关重要您位置的使用 WPA2\ 企业和最高的偏好随意选择顺序 AES 配置文件。 不支持使用 WPA2\ 企业版和 AES 的计算机将自动跳到下一步中优先顺序配置文件，并处理指定 WPA\ 企业版和 TKIP 配置文件。

> [!IMPORTANT]
> 必须配置文件中，有序列表中放置的配置文件的更高版本的最安全标准，因为连接计算机使用他们是可使用的第一个配置文件。

### <a name="planning-restricted-access-to-the-wireless-network"></a>计划受限到无线网络的访问权限

在许多情况下，你可能想要无线的用户提供不同的无线网络的访问权限级别。 例如，你可能想要允许某些无限制的用户的访问，任何一小时每天在一周内。 其他用户，你可能只想要在 core 时间内，周一到周五，允许访问上周六和星期日拒绝访问。

本指南介绍了如何创建无线资源的常见访问的组中的地方所有无线用户访问环境。 你创建一个无线用户安全组 Active Directory 用户和计算机 snap\ 中，，然后进行要授予无线的访问权限的组成员的每位的用户。

配置 NPS 网络策略，指定无线用户安全组作为 NPS 处理确定授权时的对象。

但是，如果你部署针对不同的访问权限的级别要求支持您需要只执行以下：  

1. 创建多个无线用户安全组中的 Active Directory 用户和计算机创建其他无线安全组。 例如，你可以创建包含已完全访问权限，对于只能在常规的运行时间内访问的组和适应您的需求的其他条件其他组的用户的组。

2. 添加到你创建的相应的安全组的用户。

3. 配置为无线的其他安全每个组中，其他 NPS 网络策略和配置产生的条件和约束所需的每组策略。

### <a name="planning-methods-for-adding-new-wireless-computers"></a>添加新无线计算机计划的方法

加入域，然后登录到域的新无线计算机的首选的方法是通过使用有线的连接到 lan 之外，有权访问域控制器，并通过 802.1 X 身份验证以太网交换机不受保护的一段。

在某些情况下，但是，它可能不可行使用有线的连接将计算机加入域，，或为其第一个日志在尝试使用有线的连接，使用已加入域的计算机用户。

计算机加入域使用无线连接或支持用户在登录到域首次使用 domain\ 加入的计算机和的无线连接无线客户端必须第一次建立连接到无线网络通过以下方法之一中有权访问网络域控制器段上。

1. **IT 人员的成员加入域，无线计算机，然后配置单一登录启动无线配置文件。** 使用此方法，IT 管理员无线的计算机连接到有线的以太网网络，并将计算机然后加入域。 然后管理员分发给用户的计算机。 时，用户启动计算机时，它们手动指定用户登录过程域凭据用于同时建立连接到无线网络，然后登录到的域。  

2. **用户手动启动无线的配置文件的配置无线计算机，然后加入域。** 使用此方法，用户手动配置此无线计算机与引导无线基本根据从 IT 管理员的说明进行操作。 启动无线配置文件可用于建立无线连接，并且然后加入域的计算机。 加入域的计算机并后重启计算机，用户可以在登录到域无线连接通过其域帐户凭据。

若要部署无线的访问，请参阅[无线访问部署](e-wireless-access-deployment.md)。