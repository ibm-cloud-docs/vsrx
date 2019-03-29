---

copyright:
  years: 2018
lastupdated: "2018-11-06"

keywords: limitations, problems

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

# Known Limitations for IBM Cloud Juniper vSRX
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

Current limitations for {{site.data.keyword.cloud}} IBM® Cloud Juniper vSRX:

* Juniper vSRX Gateway is deployed with networking virtualization using Linux Bridge. Linux Bridge based networking virtualization can only achieve limited throughput and never line-rate throughput.

* There is no support to upgrade from Standalone to High-availability mode.

* IBM Cloud Juniper vSRX Gateway is deployed with the options of Junos OS version `15.1` or `18.4`. Currently, there is no support for upgrading/downgrading to a different version.

* The 60-day evaluation license may cause the kernel to generate ERROR messages ,even when there is another (valid) license on the system. You should remove any 60-day evaluation licenses to avoid this issue.
