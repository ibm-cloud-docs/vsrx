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

{{site.data.keyword.cloud}} IBM® Cloud Juniper vSRX 的当前限制：

* Juniper vSRX 网关使用 Linux Bridge 通过联网虚拟化进行部署。基于 Linux Bridge 的联网虚拟化只能实现有限的吞吐量，而绝不能实现线路速率吞吐量。

* 不支持从独立方式升级到高可用性方式。

* IBM Cloud Juniper vSRX 网关通过 Junos OS V`15.1X49-D123` 进行部署。目前，不支持升级为其他版本。
