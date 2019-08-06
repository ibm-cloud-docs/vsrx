---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords:

subcollection: vsrx, ssh, allowing, pinging, subnet, public

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

# 允许流至公用子网的 SSH 和 ping 流量
{: #allowing-ssh-and-pinging-to-a-public-subnet}

在本指南中，您将了解如何为 {{site.data.keyword.vsrx_full}} Standard 配置新的接口、专区和地址簿。由于所有流量的缺省操作均为丢弃，因此本指南将说明如何设置流量流以允许新专区内的所有流量，允许从新专区流至因特网的所有流量，以及仅允许从因特网流至新 VLAN 上的一个子网的 SSH 和 ping 流量。

在此示例中，将使用以下值。

```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

此逐步指南假定 vSRX 是高可用性部署，并具有单个公用 VLAN 和子网。
{: note}

## 需要完成的任务
{: #what-you-ll-accomplish}

在此逐步指南中，您将了解如何配置服务：

任务|描述
------------- | -------------
[创建新的接口、专区和地址簿子网](/docs/infrastructure/vsrx?topic=vsrx-creating-the-new-interface-zone-and-address-book-subnet)|为新 VLAN 创建已标记的接口单元和安全专区。
[创建新的流量流](/docs/infrastructure/vsrx?topic=vsrx-creating-your-new-traffic-flows)|创建新的流量流以允许入站 ping 和 SSH。
[确认输出并落实更改](/docs/infrastructure/vsrx?topic=vsrx-confirming-the-output-and-commiting-the-changes)|检查输出以确认将落实到活动配置的内容。
