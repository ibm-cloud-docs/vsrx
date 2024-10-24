---

copyright:
  years: 2017, 2024
lastupdated: "2024-10-24"

keywords: reloading, os, upgrading, kvm, ha, standalone

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Reloading the OS
{: #reloading-the-os}
{: help}
{: support}

The OS reload process is used to rebuild a {{site.data.keyword.vsrx_full}} server.
{: shortdesc}

The process typically performs the following actions:

* Reload the server host's operating system (OS). This action generates a new host OS password.
* Install KVM in the operating system
* Create a vSRX VM in the KVM
* Reconfigure the vSRX with the default configuration for IBM® Cloud

The process can take between 2 and 5 hours to complete. Stand-alone gateways are out of service during this period. For Juniper High Availability (HA) gateways, when you reload the OS on one of your servers, the vSRX fails over to another server in the cluster and continues to process data traffic. After the reload completes, the server rejoins the cluster.

If the OS reload is changing your vSRX version, then refer to [Upgrading using OS Reload](/docs/vsrx?topic=vsrx-os-reload-upgrade#os-reload-upgrade) to understand the downgrade and upgrade process.
{: important}

For a successful OS Reload on a vSRX, ensure the following:

* The vSRX configuration should not be modified during the OS reload operation. For example, automated software agents that attempt to modify one or both vSRX nodes. Configurations changes like these can corrupt the OS reload.

* The root password for the provisioned vSRX gateway must match the root password that is defined in the vSRX portal. The password in the portal was defined when you first provisioned the gateway, and it might not match the current gateway password. If so, then use SSH to connect to the vSRX gateway and change the root password to match. You can then proceed with the OS reload operation.

* The vSRX configuration must allow root SSH access to the vSRX private IP before the OS reload request. This is required to rejoin the cluster. After the OS reload completes, if wanted, you can disable SSH access again.

* "Do NOT" perform an OS reload on both servers of the Highly Available gateway at the same time.

   Performing an OS reload on both servers of the HA gateway at the same time destroys the vSRX cluster and causes the gateway to be out of service. If the vSRX cluster is destroyed, you must use the [Rebuild cluster](/docs/vsrx?topic=vsrx-rebuilding-an-ha-cluster) option to reprovision the vSRX and re-create the HA cluster.
   {: important}

* The IPMI interface for the bare-metal server must be enabled or the following error is issued:

   ```sh
   You cannot toggle the IPMI interface while transactions are running.
   ```

## Performing an OS reload
{: #performing-an-os-reload}

To reload your OS, follow these steps:

1. From your browser, open [IBM Cloud console](/login){: external} and log in to your account.
2. Run a [Readiness check](/docs/vsrx?topic=vsrx-vsrx-readiness#vsrx-readiness) for “OS Reload” and address any errors that are found.
3. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure > Classic Infrastructure**.
4. Choose **Network > Gateway Appliances**.
5. Click the server that you want to reload.
6. Click the server name in the Hardware section.
7. Select **OS Reload** from the **Actions** menu on the upper right of the page.
8. In the **OS Reload** screen, click **Edit** for the Category that requires an update. Select **Juniper** as the Vendor, and the OS version you want to reload.
9. Click **Reload Above Configuration** to proceed to the **Review** window. Click **Cancel** to cancel the changes to the device and exit the screen.
10. Verify that all details in the **New Configuration** section are correct. Click **Next** to advance to the Confirm window.
11. Click **Confirm OS Reload** to confirm and initiate the OS Reload. Or click **Cancel** to cancel the action.

## vSRX version mismatches
{: #vsrx-version-mismatches}

A {{site.data.keyword.vsrx_full}} cluster must have the same vSRX version on each node to fully support the High Availability feature. If a cluster has mismatched vSRX versions, then you must reload the OS of the node with the older version (by using the procedure in this topic) so that both nodes are at the same version level.

A version mismatch applies to both minor release mismatches and major release mismatches.
{: note}
