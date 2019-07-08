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

# 创建新的接口、专区和地址簿子网
{: #creating-the-new-interface-zone-and-address-book-subnet}

首先，需要为 VLAN 创建接口单元，然后添加子网的网关地址。接着，可以创建与新单元关联的安全专区，并为子网创建 `address-book` 条目。  

向右滚动可查看整个命令！
{: important}

```
set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29
```
