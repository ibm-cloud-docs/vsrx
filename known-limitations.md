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

# Known Limitations

Current limitations for IBM Cloud Juniper vSRX:

* IBM Cloud Juniper vSRX Gateway is deployed with Networking virtualization using Linux Bridge. Linux Bridge based Networking virtualization can only achieve limited throughput and never line-rate throughput.

* Only 1Gbps license and interfaces are supported on Juniper vSRX. 10Gbps support is coming soon.

* There is no support to upgrade from Standalone to High-availaibity mode.

* IBM Cloud Juniper vSRX Gateway is deployed with Junos OS version `15.1X49-D123`. Currently, there is no support for upgrading to a different version.
