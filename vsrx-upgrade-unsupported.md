---

copyright:
  years: 2019
lastupdated: "2020-09-18"

keywords: reloading, os, upgrading, kvm, ha, standalone

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Unsupported upgrades
{: #unsupported-upgrade}

Early deployments of 1G vSRX 15.1 and 18.4 gateways used a networking design based on Linux Bridging. Newer 1G deployments use a networking design based on SR-IOV. For more information, see [Understanding the vSRX default configuration](/docs/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration).
{: shortdesc}

Early 1G deployments generally used an Intel 1270v6 4-Core, Sky-Lake-based processor. This processor does not support SR-IOV. Newer vSRX versions, such as 19.4, require the SR-IOV networking design. Therefore, vSRX version upgrades are not supported for deployments based on this 1270v6 processor.

To upgrade to a newer vSRX version, such as 19.4, you must place a new vSRX order. After completion, you can migrate the configuration from the old design to the new, but you must also apply some manual configuration changes to the new vSRX. For more information, see [Migrating legacy configurations to the current vSRX architecture](/docs/vsrx?topic=vsrx-migrating-config).
