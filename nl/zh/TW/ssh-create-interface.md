---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: create, creating, interface, zone, address, subnets, ssh

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# 建立新介面、區域及通訊錄子網路
{: #creating-the-new-interface-zone-and-address-book-subnet}

首先，您需要建立 VLAN 的介面單元，並新增子網路的閘道位址。然後，您可以建立與新單元相關聯的安全區域，以及子網路的 `address-book` 項目。  

捲動至右側，以檢視整個指令！
{: important}

```
set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29
```
