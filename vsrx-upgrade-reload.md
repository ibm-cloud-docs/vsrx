---

copyright:
  years: 2017, 2025
lastupdated: "2025-04-25"

keywords: reloading, os, upgrading, kvm, ha, standalone

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Upgrading by using OS reload
{: #os-reload-upgrade}

This document outlines the process to update the Junos version for both stand-alone and high-availability (HA) vSRX gateway appliance deployments. The upgrade also includes deploying a specific, tested Ubuntu version paired with the Junos version. Review the complete process outlined in the following sections before you start your Juniper vSRX upgrade maintenance window.

The stand-alone vSRX upgrade is highly impactful, causing traffic downtime during the reload and reconfiguration. You must manually back up and restore the configuration because the upgrade process erases all configurations.
{: important}

## Upgrading a stand-alone vSRX deployment
{: #upgrading-standalone-vsrx}

To upgrade a stand-alone vSRX deployment, follow these steps:

1. [Export the current vSRX configuration](/docs/vsrx?topic=vsrx-importing-exporting-vsrx-configuration#export-the-whole-vsrx-configuration): Back up the settings before you start the deployment because the reload removes all configurations.
1. [Access the gateway details page](/docs/vsrx?topic=vsrx-viewing-gateway-appliance-details): View the gateway appliance's specifics by navigating to its details page.
1. Run a [Readiness check](/docs/vsrx?topic=vsrx-vsrx-readiness) for “Version upgrade” and address any errors that are found.

   Run the readiness check several hours before the maintenance so that any outstanding access and configuration requirements are addressed before the upgrade maintenance. Readiness checks take about 30 minutes to run, and a readiness check status expires after 5 hours.
   {: important}

1. Perform an [OS reload](/docs/vsrx?topic=vsrx-reloading-the-os#performing-an-os-reload) for the bare metal server. Edit the selection and specify the version where the system reloads or upgrades.

## Upgrading a High-Availabity vSRX deployment
{: #upgrading-ha-vsrx}

The HA vSRX upgrade causes minimal downtime, limited to failover periods from primary to backup. Your previous configurations are automatically backed up and restored, but it's critical to keep offsite backups for added security. Plan 2 to 5 hours for each node upgrade, and set aside 8 to 10 hours to complete the entire cluster upgrade.
{: important}

To upgrade an HA vSRX deployment, follow these steps:

1. [Access the gateway details page](/docs/vsrx?topic=vsrx-viewing-gateway-appliance-details).
1. Run a [Readiness check](/docs/vsrx?topic=vsrx-vsrx-readiness) for “Version upgrade” and address any errors that are found.

   Run the readiness check several hours before the maintenance so that any outstanding access and configuration requirements are addressed before the upgrade maintenance. Readiness checks take about 30 minutes to run, and a readiness check status expires after 5 hours.
   {: important}

1. Perform an [OS reload](/docs/vsrx?topic=vsrx-reloading-the-os#performing-an-os-reload) on each bare metal server one at a time, starting the next one only after the previous finishes. For each reload, manually select the OS version for installation or upgrade.

   When you upgrade an HA cluster, the process automatically powers off the node not undergoing the OS reload at the end of the upgrade process. If you start the upgrade with the first node, the second node handles active network traffic during the reload. After the first node finishes reloading, the second node's VM is automatically powered off, and traffic shifts to the first node, which becomes the primary node with the new version. Leave the second node powered off at this stage. This action is intentional to prevent a version mismatch, where both nodes try to become primary causing an outage. After the first node's OS reload is complete and you confirm that traffic flows correctly, rerun the upgrade readiness check if needed, then proceed with the second node.
   {: important}

## vSRX configuration migration considerations
{: #migration-considerations}

For a High Availability environment, the upgrade restores the previous vSRX configuration. No further steps are needed.

For a stand-alone environment, the upgrade does not restore the previous configuration, so you must export and import your configuration. For more information, see [Importing and exporting a vSRX configuration](/docs/vsrx?topic=vsrx-importing-exporting-vsrx-configuration).

Also, when you migrate from an older version, such as 15.1, you might notice changes in interface mappings. This process requires some modifications to the vSRX configuration after the import. for more information, see [Migrating 1G vSRX stand-alone configurations](/docs/vsrx?topic=vsrx-migrating-config#migrating-1g-standalone).
