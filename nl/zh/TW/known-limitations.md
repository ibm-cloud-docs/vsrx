---

copyright:
  years: 2018
lastupdated: "2018-11-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# IBM Cloud Juniper vSRX 的已知限制
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

{{site.data.keyword.cloud}}IBM® Cloud Juniper vSRX 的現行限制：

* Juniper vSRX Gateway 是使用 Linux Bridge 搭配網路虛擬化進行部署。Linux Bridge 型網路虛擬化只能達到有限的傳輸量且永達不到線路速率傳輸量。

* 不支援從「獨立式」升級至「高可用性」模式。

* IBM Cloud Juniper vSRX Gateway 是使用 Junos OS 版本 `15.1X49-D123` 進行部署。目前，不支援升級至不同版本。
