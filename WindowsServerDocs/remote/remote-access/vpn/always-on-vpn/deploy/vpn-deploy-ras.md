---
title: 为始终启用 VPN 配置远程访问服务器
description: RRAS 旨在同时作为路由器和远程访问服务器执行;因此，它支持多种功能。
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.localizationpriority: medium
ms.author: v-tea
author: Teresa-MOTIV
ms.date: 08/30/2018
ms.reviewer: deverette
ms.openlocfilehash: 4cb5d5fc65eee997068ea3192081bf753fdd9083
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818980"
---
# <a name="step-3-configure-the-remote-access-server-for-always-on-vpn"></a>步骤 3。 为始终启用 VPN 配置远程访问服务器

>适用于： Windows Server （半年频道）、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**上一个：** 步骤2。配置服务器基础结构](vpn-deploy-server-infrastructure.md)
- [**上一个：** 步骤4。安装和配置网络策略服务器（NPS）](vpn-deploy-nps.md)

RRAS 旨在同时作为路由器和远程访问服务器执行，因为它支持多种功能。 对于此部署，只需一小部分这些功能：支持 IKEv2 VPN 连接和 LAN 路由。

IKEv2 是 Internet 工程任务团队请求注释7296中所述的 VPN 隧道协议。 IKEv2 的主要优点是它不必完全了基础网络连接中的中断。 例如，如果连接暂时丢失或用户将客户端计算机从一个网络移到另一个网络，则在重新建立网络连接后，IKEv2 会自动恢复 VPN 连接，而无需用户干预。

在禁用未使用的协议时，将 RRAS 服务器配置为支持 IKEv2 连接，这会降低服务器的安全空间。 此外，将服务器配置为从静态地址池将地址分配给 VPN 客户端。 可以册从池或 DHCP 服务器分配地址;但是，使用 DHCP 服务器会增加设计的复杂性，并提供最少的好处。

>[!IMPORTANT]
>重要的是：
>- 在物理服务器中安装两个以太网网络适配器。 如果要在虚拟机上安装 VPN 服务器，则必须创建两个外部虚拟交换机，每个物理网络适配器一个;然后为 VM 创建两个虚拟网络适配器，每个网络适配器连接到一个虚拟交换机。
>
>- 将服务器安装在外围网络和内部防火墙之间，将一个网络适配器连接到外部外围网络，并将一个网络适配器连接到内部外围网络。

>[!WARNING]
>在开始之前，请确保在 VPN 服务器上启用 IPv6。 否则，无法建立连接，并显示一条错误消息。

## <a name="install-remote-access-as-a-ras-gateway-vpn-server"></a>将远程访问作为 RAS 网关 VPN 服务器安装

在此过程中，你将远程访问角色安装为单租户 RAS 网关 VPN 服务器。 有关详细信息，请参阅[远程访问](../../../Remote-Access.md)。

### <a name="install-the-remote-access-role-by-using-windows-powershell"></a>使用 Windows PowerShell 安装远程访问角色

1. 以**管理员身份**打开 Windows PowerShell。

2. 输入并运行以下 cmdlet：

   ```powershell
   Install-WindowsFeature DirectAccess-VPN -IncludeManagementTools
   ```

   安装完成后，Windows PowerShell 中将显示以下消息。

   ```powershell
   | Success | Restart Needed | Exit Code |               Feature Result               |
   |---------|----------------|-----------|--------------------------------------------|
   |  True   |       No       |  Success  | {RAS Connection Manager Administration Kit |
   ```

### <a name="install-the-remote-access-role-by-using-server-manager"></a>使用服务器管理器安装远程访问角色

你可以使用以下过程通过服务器管理器安装远程访问角色。

1. 在 VPN 服务器上的服务器管理器中，选择 "**管理**"，然后选择 "**添加角色和功能**"。
   
   将打开“添加角色和功能向导”。

2. 在 "开始之前" 页上，选择 "**下一步**"。

3. 在 "选择安装类型" 页上，选择 "**基于角色或基于功能的安装**" 选项，然后选择 "**下一步**"。

4. 在 "选择目标服务器" 页上，选择 "**从服务器池中选择服务器**" 选项。

5. 在 "服务器池" 下，选择本地计算机，然后选择 "**下一步**"。

6. 在 "选择服务器角色" 页的 "**角色**" 中，选择 "**远程访问**"，然后选择 "**下一步**"

7. 在 "选择功能" 页上，选择 "**下一步**"。

8. 在 "远程访问" 页上，选择 "**下一步**"。

9.  在 "选择角色服务" 页上，在 "**角色服务**" 中选择 " **DirectAccess 和 VPN （RAS）** "。

   此时将打开 "**添加角色和功能向导**" 对话框。

11. 在 "添加角色和功能" 对话框中选择 "**添加功能**"，然后选择 "**下一步**"。

12. 在 "Web 服务器角色（IIS）" 页上，选择 "**下一步**"。

13. 在 "选择角色服务" 页上，选择 "**下一步**"。

14. 在 "确认安装选择" 页上，查看你的选择，然后选择 "**安装**"。

15. 安装完成后，选择 "**关闭**"。

## <a name="configure-remote-access-as-a-vpn-server"></a>将远程访问配置为 VPN 服务器

在本部分中，你可以配置远程访问 VPN，以允许 IKEv2 VPN 连接，拒绝来自其他 VPN 协议的连接，并分配静态 IP 地址池，以便颁发 IP 地址来连接授权的 VPN 客户端。

1. 在 VPN 服务器上的 "服务器管理器中，选择"**通知**"标志。

2. 在 "**任务**" 菜单中，选择 **"打开入门向导"**

   此时将打开 "配置远程访问" 向导。

   >[!NOTE]
   >配置远程访问向导可能会打开服务器管理器。 如果你认为该向导需要很长时间才能打开，请移动或最小化服务器管理器，以确定该向导是否位于该向导后面。 如果不是，请等待向导初始化。

3. 选择 "**仅部署 VPN**"。

    此时将打开 "路由和远程访问 Microsoft 管理控制台（MMC）"。

4. 右键单击 VPN 服务器，然后选择 "**配置并启用路由和远程访问**"。

   此时将打开 "路由和远程访问服务器安装向导"。

5. 在 "欢迎使用路由和远程访问服务器安装向导" 中，选择 "**下一步**"。

6. 在 "**配置**" 中选择 "**自定义配置**"，然后选择 "**下一步**"。

7. 在 "**自定义配置**" 中，选择**VPN 访问**，然后选择 "**下一步**"。

   "正在完成路由和远程访问服务器安装向导" 将打开。

8. 选择 "**完成**" 关闭向导，然后选择 **"确定"** 以关闭 "路由和远程访问" 对话框。

9. 选择 "**启动服务**" 以启动远程访问。

10. 在远程访问 MMC 中，右键单击 VPN 服务器，然后选择 "**属性**"。

11. 在 "属性" 中，选择 "**安全**" 选项卡并执行以下操作：

    a. 选择 "**身份验证提供程序**" 并选择 " **RADIUS 身份验证**"。

    b. 选择 "**配置**"。

       "RADIUS 身份验证" 对话框随即打开。

    c. 选择“添加”。

       此时将打开 "添加 RADIUS 服务器" 对话框。

    d. 在 "**服务器名称**" 中，输入组织/企业网络上 NPS 服务器的完全限定的域名（FQDN）。
    
       例如，如果 NPS 服务器的 NetBIOS 名称是 NPS1，而你的域名为 corp.contoso.com，则输入**NPS1.corp.contoso.com**。

    e. 在 "**共享密钥**" 中，选择 "**更改**"。

       此时将打开 "更改机密" 对话框。

    f. 在 "**新密码**" 中，输入文本字符串。

    g. 在 "**确认新密码**" 中，输入相同的文本字符串，然后选择 **"确定"** 。

    >[!IMPORTANT]
    >保存该文本字符串。 在组织/企业网络上配置 NPS 服务器时，会将此 VPN 服务器添加为 RADIUS 客户端。 在此配置过程中，你将使用此相同的共享机密，以便 NPS 和 VPN 服务器可以进行通信。

12. 在 "**添加 RADIUS 服务器**" 中，查看以下项的默认设置：

    - **超时**

    - **初始分数**

    - **Port**

13. 如有必要，请更改这些值以匹配环境的要求，然后选择 **"确定"** 。

    NAS 是提供对较大网络的某些级别的访问权限的设备。 使用 RADIUS 基础结构的 NAS 还是 RADIUS 客户端，它将连接请求和记帐消息发送到 RADIUS 服务器以便进行身份验证、授权和记帐。

14. 查看**记帐提供程序**的设置：

    |                    如果你想要 。                     |                                                     那么...                                                      |
    |-----------------------------------------------------------|----------------------------------------------------------------------------------------------------------------|
    | 远程访问在远程访问服务器上的活动 |                               请确保已选择 " **Windows 记帐**"。                               |
    |        用于为 VPN 执行记帐服务的 NPS         | 将**记帐提供程序**更改为**RADIUS 记帐**，然后将 NPS 配置为记帐提供程序。 |

15. 选择 " **IPv4** " 选项卡，并执行以下操作：

    a. 选择 "**静态地址池**"。

    b. 选择 "**添加**" 以配置 IP 地址池。

       静态地址池应包含来自内部外围网络的地址。 这些地址位于 VPN 服务器上的面向内部的网络连接上，而不是企业网络中。

    c. 在 "**起始 ip 地址**" 中，输入要分配给 VPN 客户端的范围中的起始 ip 地址。

    d. 在 "**结束 ip 地址**" 中，输入要分配给 VPN 客户端的范围中的结束 ip 地址，或在 "**地址数**" 中，输入要提供的地址号。 如果在此子网中使用 DHCP，请确保在 DHCP 服务器上配置相应的地址排除。

    e. 可有可无如果你使用的是 DHCP，则选择 "**适配器**"，然后在结果列表中选择连接到内部外围网络的以太网适配器。

16. 可有可无*如果要配置 vpn 连接的条件性访问*，请在 "**证书**" 下拉列表中的 " **SSL 证书绑定**" 下，选择 VPN 服务器身份验证。

17. 可有可无*如果要配置 VPN 连接的条件性访问*，请在 NPS MMC 中，展开 "**策略"\\"网络策略**"，然后执行以下操作： 

    a. 右键**连接到 Microsoft 路由和远程访问服务器**网络策略，然后选择 "**属性**"。

    b. 选择 "**授予访问权限"。如果连接请求与此策略选项匹配，则授予访问权限**。

    c. 在 "网络访问服务器类型" 下，从下拉菜单中选择 "**远程访问服务器（VPN 拨号）** "。

18. 在 "路由和远程访问" MMC 中，右键单击 "**端口"，** 然后选择 "**属性**"。 
    
    "端口属性" 对话框将打开。

19. 选择 " **WAN 微型端口（SSTP）** "，然后选择 "**配置**"。 此时将打开 "配置设备-WAN 微型端口（SSTP）" 对话框。

    a. 清除**远程访问连接（仅入站）** 和**请求拨号路由连接（入站和出站）** 复选框。

    b. 选择“确定”。

20. 选择 " **WAN 微型端口（L2TP）** " 并选择 "**配置**"。 此时将打开 "配置设备-WAN 微型端口（L2TP）" 对话框。

    a. 在 "**最大端口**数" 中，输入要与你要支持的同时 VPN 连接的最大数量相匹配的端口数。

    b. 选择“确定”。

21. 选择 " **WAN 微型端口（PPTP）** "，然后选择 "**配置**"。 此时将打开 "配置设备-WAN 微型端口（PPTP）" 对话框。

    a. 在 "**最大端口**数" 中，输入要与你要支持的同时 VPN 连接的最大数量相匹配的端口数。

    b. 选择“确定”。

22. 选择 " **WAN 微型端口（IKEv2）** "，然后选择 "**配置**"。 此时将打开 "配置设备-WAN 微型端口（IKEv2）" 对话框。

     a. 在 "**最大端口**数" 中，输入要与你要支持的同时 VPN 连接的最大数量相匹配的端口数。

     b. 选择“确定”。

23. 如果系统提示，请选择 **"是"** 以确认重新启动服务器，然后选择 "**关闭**" 以重新启动服务器。

## <a name="next-step"></a>下一步

[步骤4。安装和配置网络策略服务器（NPS）](vpn-deploy-nps.md)：在此步骤中，你可以使用 Windows PowerShell 或服务器管理器添加角色和功能向导 "安装网络策略服务器（nps）。 你还可以将 NPS 配置为处理从 VPN 服务器接收的连接请求的所有身份验证、授权和记帐职责。
