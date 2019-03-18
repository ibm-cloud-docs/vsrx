---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 关于 IBM Cloud Juniper vSRX
{: #about-ibm-cloud-juniper-vsrx}

借助 IBM® Cloud Juniper vSRX，您可以通过基于 JunOS 软件功能（例如，全路由堆栈、QoS 和流量共享、基于策略的路由以及 VPN）的全功能企业级防火墙，选择性路由专用和公用网络流量。vSRX 利用在裸机服务器上运行的简易性，提供了高性能、配置和维护轻松的优势。硬件会调整大小，以处理多个 VLAN 的路由/安全负载，并且在订购时可以包含冗余网络链路和冗余 RAID 阵列。所有 vSRX 功能都由客户进行管理。

IBM Cloud vSRX 以两种不同的方式提供：独立集群或高可用性 (HA) 集群。

**注：**IBM Cloud Juniper vSRX 的其他文档可以在[补充文档](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation)主题中找到。

## 防火墙
vSRX 部署为通过过滤面向专用和公共的流量，保护环境免受外部和内部威胁。客户可以通过定义策略和规则以允许或拒绝（以及执行其他操作）入站或出站网络流量来管理 vSRX 本身，从而保护其应用程序免受内部和外部用户的影响。IPv4 和 IPv6 堆栈均以有状态方式受到支持。

## 虚拟专用网 (VPN) 网关
通过将 vSRX 作为网关设备供应，可使用 VPN 隧道将现场数据中心或办公室连接到 IBM Cloud。可以使用 IPsec 站点到站点 VPN 隧道来保护从企业数据中心或办公室到 IBM Cloud 网络的通信。此外，还支持远程访问 IPSEC VPN。

有关 VPN 的详细配置指南，请参阅 [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn) 主题中提供的链接。

## 网络地址转换 (NAT)
通过 vSRX 网关设备，您可以在没有公用网络接口的情况下供应应用程序和数据库服务器，同时仍允许服务器使用源 NAT 访问因特网。此外，还可以使用目标 NAT 将服务器隐藏在网关设备后面，以增强安全性。

## 企业级路由
对于不同隔离网络上的多层应用程序，vSRX 支持更灵活地在这些网络之间构建连接。您可以使用 BGP 来设置动态路由，这将允许您向 IBM Cloud 路由器声明您自己的公共 IP 空间。此外，BGP 在混合使用隧道和直接链路解决方案时，为定制专用网络配置提供了更大的灵活性。

## 关于 VLAN 和网关设备角色的概念
VLAN（虚拟 LAN）是用于将物理网络划分为多个虚拟分段的机制。为了方便起见，可以通过单一网络电缆来传递来自多个所选 VLAN 的流量，这一过程通常称为“中继”。

vSRX 在两个不同的界面中进行管理：vSRX 服务器和网关设备装置。网关设备提供的界面（GUI 和 API）可用于选择要与 vSRX 关联的 VLAN。通过将 VLAN 与网关设备相关联，可将 VLAN 及其所有子网重新路由（或“中继”）到 vSRX，从而为您提供对过滤、转发和保护操作的控制权。关联 VLAN 中的服务器只能通过 vSRX 从其他 VLAN 进行访问；除非绕过或解除关联 VLAN，否则无法避开 vSRX。

缺省情况下，新的网关设备与两个不可除去的“传输”VLAN 相关联，分别用于_公用_和_专用_网络。这些网络通常用于管理，并且可以通过 vSRX 命令单独进行保护。

vSRX 只能管理通过网关设备与其关联的 VLAN。

有关如何在**网关设备详细信息**屏幕中管理 VLAN 的信息，请参阅[管理 VLAN](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans) 主题。
