---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: working, routing, static, default, creating, ospf, bgp

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

# 使用遞送
{: #working-with-routing}

IBM® Cloud Juniper vSRX 係以 `JunOS` 為基礎，可讓您存取完整 Juniper 遞送堆疊。

##靜態遞送
{: #static-routing}

若要配置靜態路由，請執行下列指令：

###設定預設路由
{: #setting-a-default-route}

```
set routing-options static route 0/0 next-hop <Gateway IP>
```

### 建立靜態路由
{: #creating-a-static-route}
```
set routing-options static route <PREFIX/MASK> next-hop <Gateway IP>
```  

###基本 OSPF 遞送
{: #basic-ospf-routing}

若要僅使用區域 0 設定基本 OSPF 遞送，請使用 md5 鑑別來執行下列指令：

```
set protocols ospf area 0 interface ge-0/0/1.0 authentication md5 0 key <KEY>
```

### 基本 BGP 遞送
{: #basic-bgp-routing}

若要設定基本 BGP 遞送，請先定義本端 AS：

```
set routing-options autonomous-system 65001
```

然後，配置 BGP 鄰接項及其階段作業屬性：

```
set protocols bgp group CUSTOMER local-address 1.1.1.1
set protocols bgp group CUSTOMER family inet unicast
set protocols bgp group CUSTOMER family inet6 unicast
set protocols bgp group CUSTOMER peer-as 65002
set protocols bgp group CUSTOMER neighbor 2.2.2.2
```

在此範例中，會配置 BGP 進行下列作業：

* 使用 `1.1.1.1` 的來源 IP 位址來建立階段作業
* 同時協議 ipv4 及 ipv6 單點播送系列
* 與屬於 `AS 65002` 的鄰接項對等
* 對等節點鄰接項 IP `2.2.2.2`

您可以在 [Juniper 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.juniper.net/documentation/en_US/junos11.4/information-products/topic-collections/config-guide-routing/config-guide-routing.pdf){: new_window} 上找到其他配置。
