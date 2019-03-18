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

# 關於 IBM Cloud Juniper vSRX
{: #about-ibm-cloud-juniper-vsrx}

IBM® Cloud Juniper vSRX 容許您透過採用 JunOS 軟體特性技術（例如完整遞送堆疊、服務品質及資料流量共用、以原則為基礎的遞送，以及 VPN）的全功能企業層級防火牆，選擇性地遞送專用及公用網路資料流量。vSRX 提供效能、易於配置及維護優勢，並簡化裸機伺服器上的執行作業。此硬體會調整大小，以處理多個 VLAN 的遞送/安全負載，而且可以搭配備援網路鏈結及備援 RAID 陣列來訂購。所有 vSRX 特性都由客戶進行管理。

IBM Cloud vSRX 提供兩種不同模式：獨立式或「高可用性 (HA)」叢集。

**附註：**可在[補充文件](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation)主題中找到 IBM Cloud Juniper vSRX 的其他文件。

## 防火牆
vSRX 會進行部署，透過過濾專用及公用樣式資料流量，以保護您的環境免於外部及內部威脅。客戶可以管理 vSRX 本身，方法為定義原則及規則以容許或拒絕（在其他動作之間）入埠或出埠網路資料流量，保護其應用程式免於內部及外部使用者存取。系統是以有狀態方式支援 IPv4 及 IPv6 堆疊。

## 虛擬專用網路 (VPN) 閘道
使用 VPN 通道作業，藉由將 vSRX 佈建為網路閘道裝置，將現場資料中心或辦公室連接至 IBM Cloud。您可以使用 IPsec 網站至網站 VPN 通道，以進行從企業資料中心或辦公室到 IBM Cloud 網路的安全通訊。同時支援遠端存取 IPSEC VPN。

如需 VPN 的詳細配置手冊，請參閱 [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn) 主題中提供的鏈結。

## 網址轉換 (NAT)
使用 vSRX 閘道應用裝置時，您可以在沒有公用網路介面的情況下佈建應用程式及資料庫伺服器，同時仍容許伺服器使用「來源 NAT」存取網際網路。您也可以使用「目的地 NAT」將伺服器隱藏在閘道裝置之後，以加強安全。

## 企業級遞送
對於不同隔離網路上的多層應用程式，vSRX 可讓您在這些網路之間建置連線功能，提供更大的彈性。您可以使用 BGP 來設定動態遞送，這可讓您向 IBM Cloud 路由器宣佈自己的公用 IP 空間。使用混合通道及直接鏈結解決方案時，BGP 也會為自訂的專用網路配置提供更多的彈性。

## 關於 VLAN 及閘道應用裝置角色的概念
VLAN（虛擬 LAN）是將實體網路隔離成許多虛擬區段的一種機制。為了方便起見，多個所選 VLAN 的資料流量可以透過單一網路纜線來遞送，這個程序通常稱為「幹線」。

vSRX 是以兩種不同介面來管理：vSRX 伺服器及「閘道應用裝置」設備。「閘道應用裝置」提供一個介面（GUI 及 API），供您選取要與 vSRX 相關聯的 VLAN。建立 VLAN 與「閘道應用裝置」的關聯，會將該 VLAN 及其所有子網路重新遞送（或「幹線」）至您的 vSRX，這可讓您控制過濾、轉遞及保護。只能透過 vSRX 從其他 VLAN 連接至關聯 VLAN 中的伺服器；除非您略過或取消關聯 VLAN，否則無法規避 vSRX。

依預設，新的「閘道應用裝置」會與兩個不可移除的「傳輸」VLAN 相關聯，每個 VLAN 都用於_公用_ 及_專用_ 網路。這些網路通常用於管理，而且它們可以藉由 vSRX 指令個別保護。

vSRX 只能透過「閘道應用裝置」管理與其相關聯的 VLAN。

如需如何從**閘道應用裝置詳細資料**畫面管理 VLAN 的相關資訊，請參閱[管理 VLAN](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans) 主題。
