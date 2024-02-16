---

copyright:
  years: 2019
lastupdated: "2020-09-16"

keywords: reloading, os, upgrading, kvm, ha, standalone

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Upgrading by using OS reload
{: #os-reload-upgrade}

To upgrade your vSRX by using OS reload, follow these steps:

1. **Stand-alone environment only:** [Export the vSRX configuration](/docs/vsrx?topic=vsrx-importing-exporting-vsrx-configuration#export-the-whole-vsrx-configuration).
2. [Access the gateway details page](/docs/vsrx?topic=vsrx-viewing-gateway-appliance-details).
3. Run a [Readiness check](/docs/vsrx?topic=vsrx-vsrx-readiness) for “Version upgrade” and address any errors that are found.

   Run your readiness check well before the actual upgrade maintenance to ensure that any outstanding access and configuration requirements are addressed before the upgrade maintenance. Also run another readiness check immediately before the maintenance action, as readiness checks expire after 5 hours.
   {: important}

4. Perform an [OS reload](/docs/vsrx?topic=vsrx-reloading-the-os#performing-an-os-reload) for each bare metal server.

   When you upgrade an HA cluster, the process powers off the node not undergoing the OS reload at the end of the upgrade process. This transitions the cluster’s primary node and any active network traffic to the newly upgraded one. After the OS reload completes for the first node in the cluster, it is critical that the second node is left unpowered until the OS reload to upgrade that node is submitted and running. Powering on the node before the OS reload causes the cluster to run with mismatched vSRX versions, potentially leading to a “split-brain” scenario where each node tries to claim primary ownership. This generally results in an outage. After the OS reload of the first node, the gateway transitions to “Upgrade Active” status.
   {: important}

5. **Stand-alone environment only:** [Import the vSRX configuration](/docs/vsrx?topic=vsrx-importing-exporting-vsrx-configuration#import-the-whole-vsrx-configuration) and migrate the settings to the new architecture if necessary.

## vSRX configuration migration considerations
{: #migration-considerations}

For a High Availability environment, the upgrade restores the previous vSRX configuration. No further steps are needed.

For a stand-alone environment, the upgrade does not restore the previous configuration, so you should export and import your configuration. Refer to [Importing and exporting a vSRX configuration](/docs/vsrx?topic=vsrx-importing-exporting-vsrx-configuration) for more information.

Also, when you migrate from an older version, such as 15.1, your interface mappings might have changed. This requires some modifications to the vSRX configuration after the import. Refer to [Migrating 1G vSRX stand-alone configurations](/docs/vsrx?topic=vsrx-migrating-config#migrating-1g-standalone) for more information.
