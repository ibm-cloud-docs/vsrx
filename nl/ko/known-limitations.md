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

# IBM Cloud Juniper vSRX에 대한 알려진 제한사항 
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

{{site.data.keyword.cloud}} IBM® Cloud Juniper vSRX의 현재 제한사항:

* Juniper vSRX Gateway는 Linux Bridge를 사용하여 네트워킹 가상화로 배치됩니다. Linux Bridge 기반 네트워킹 가상화는 제한된 처리량에만 도달하고 최대 속도 처리량에는 도달하지 않을 수 있습니다.

* 독립형에서 고가용성 모드로의 업그레이드는 지원되지 않습니다.

* IBM Cloud Juniper vSRX Gateway는 Junos OS 버전 `15.1X49-D123`으로 배치됩니다. 현재 다른 버전에 대한 업그레이드는 지원되지 않습니다.
