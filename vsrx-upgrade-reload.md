---

copyright:
  years: 2019
lastupdated: "2020-09-16"

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

# Upgrading using OS reload
{: #os-reload-upgrade}

To upgrade your vSRX using OS reload, perform the following procedure.

1.	**Standalone environment only:** [Export the vSRX configuration](/docs/vsrx?topic=vsrx-importing-exporting-vsrx-configuration#export-the-whole-vsrx-configuration).
2.	[Access the gateway details page](/docs/vsrx?topic=gateway-appliance-viewing-gateway-appliance-details).
3.	Run a [Readiness check](/docs/vsrx?topic=vsrx-vsrx-readiness) for “OS reload” and address any errors that are found.
4.	Perform an [OS reload](/docs/vsrx?topic=vsrx-reloading-the-os#performing-an-os-reload) for each bare metal server.

  When upgrading an HA cluster, the process will power off the node not undergoing the OS reload at the end of the upgrade process. This will transition the cluster’s primary node and any active network traffic to the newly upgraded one. Once the OS reload completes for the first node in the cluster, it is critical that the second node be left unpowered until the OS reload to upgrade that node is submitted and running. Powering the node on prior to the OS reload will cause the cluster to run with mismatched vSRX versions, potentially leading to a “split-brain” scenario where each node tries to claim primary ownership. This generally results in an outage. After the OS reload of the first node, the gateway will transition to “Upgrade Active” status.
  {: important}

5.	**Standalone environment only:** [Import the vSRX configuration](/docs/vsrx?topic=vsrx-importing-exporting-vsrx-configuration#import-the-whole-vsrx-configuration) and migrate the settings to the new architecture if necessary.

## vSRX configuration migration considerations
{: #migration-considerations}

For a High Availability environment, the upgrade restores the previous vSRX configuration. No further steps are needed.

For a Standalone environment, the upgrade does not restore the previous configuration, so you should export and import your configuration. Refer to [Importing and exporting a vSRX configuration](/docs/vsrx?topic=vsrx-importing-exporting-vsrx-configuration) for more information.

Additionally, when migrating from an older version, such as 15.1, your interface mappings may have changed. This requires some modifications to the vSRX configuration after the import. Refer to [Migrating 1G vSRX standalone configurations](/docs/vsrx?topic=vsrx-migrating-config#migrating-1g-standalone) for more information.
