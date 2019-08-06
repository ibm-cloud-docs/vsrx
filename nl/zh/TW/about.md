---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: about, vsrx, overview, details, firewall, vpn, nat, routing, vlan

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# 關於 {{site.data.keyword.vsrx_full}}
{: #about-ibm-cloud-juniper-vsrx}

{{site.data.keyword.vsrx_full}} 可讓您透過採用 JunOS 軟體特性技術（例如，完整遞送堆疊、QoS 和資料流量共用、以原則為基礎的遞送以及 VPN）的完整特性企業級防火牆，有選擇地遞送專用和公用網路資料流量。vSRX 利用在裸機伺服器上執行的簡易性，提供效能、簡易配置和維護優勢。硬體會調整大小，以處理與多個 VLAN 關聯的遞送和安全負載，並且可以訂購包含冗餘網路鏈結和冗餘 RAID 陣列的硬體。所有 vSRX 特性都由客戶進行管理。

{{site.data.keyword.vsrx_full}} 提供兩種不同模式：獨立式模式或高可用性 (HA) 叢集。

{{site.data.keyword.vsrx_full}} 的其他文件可以在[補充文件](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation)主題中找到。
{: note}

## 防火牆
{: #firewall}

vSRX 部署為通過過濾面向專用和面向公共的資料流量，保護環境免受外部和內部威脅。客戶可以通過定義原則和規則以容許或拒絕（以及執行其他動作）入埠或出埠網路資料流量來自行管理 vSRX，從而保護其應用程式免被內部和外部訪問。系統是以有狀態方式支援 IPv4 及 IPv6 堆疊。

## 虛擬專用網路 (VPN) 閘道
{: #virtual-private-network-vpn-gateway}

使用 VPN 通道作業，藉由將 vSRX 佈建為網路閘道裝置，將現場資料中心或辦公室連接至 IBM Cloud。您可以使用 IPsec 網站至網站 VPN 通道，以進行從企業資料中心或辦公室到 IBM Cloud 網路的安全通訊。此外，還支援遠端存取 IPsec VPN。

如需 VPN 的詳細配置手冊，請參閱 [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn) 主題中提供的鏈結。

## 網址轉換 (NAT)
{: #network-address-translation-nat-}

利用 vSRX 閘道應用裝置，您可以佈建沒有公用網路介面的應用程式和資料庫伺服器，同時仍容許伺服器使用_來源 NAT_ 存取網際網路。為了增強安全，可以使用_目的地 NAT_ 來保護閘道裝置後面的伺服器。

## 企業級遞送
{: #enterprise-grade-routing}

vSRX 可讓您更靈活地在執行於不同隔離網路上的多層式應用程式之間建立連線功能。您可以使用 BGP 來設定動態遞送，這可讓您向 IBM Cloud 路由器宣佈自己的公用 IP 空間。此外，BGP 在混合使用通道和[Direct Link 解決方案](/docs/infrastructure/direct-link?topic=direct-link-overview-of-direct-link-offerings#overview-of-direct-link-offerings)時，為自訂專用網路配置提供了更大的彈性。

## 關於 VLAN 及閘道應用裝置角色的概念
{: #concepts-about-vlans-and-the-gateway-appliance-s-role}

VLAN（虛擬區域網路）是用於將實體網路劃分為多個虛擬區段的機制。為了方便起見，可以使用通常稱為「幹線」的程序，通過單一網路纜線來傳遞來自多個所選 VLAN 的資料流量。

vSRX 是以兩種不同介面來管理：vSRX 伺服器及「閘道應用裝置」設備。「閘道應用裝置」提供一個介面（GUI 及 API），供您選取要與 vSRX 相關聯的 VLAN。建立 VLAN 與「閘道應用裝置」的關聯，會將該 VLAN 及其所有子網路重新遞送（或「幹線」）至您的 vSRX，這可讓您控制過濾、轉遞及保護。相關聯 VLAN 中的伺服器只能透過 vSRX 從其他 VLAN 進行訪問；除非繞過 VLAN 或取消與 VLAN 的關聯，否則無法避開 vSRX。

依預設，新的「閘道應用裝置」會與兩個不可移除的「傳輸」VLAN 相關聯，每個 VLAN 都用於_公用_ 及_專用_ 網路。這些網路通常用於管理，而且它們可以藉由 vSRX 指令個別保護。

vSRX 只能管理透過閘道應用裝置與其相關聯的 VLAN。

如需如何從**閘道應用裝置詳細資料**畫面管理 VLAN 的相關資訊，請參閱[管理 VLAN](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans) 主題。
