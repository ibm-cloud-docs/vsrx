---

copyright:
  years: 2018
lastupdated: "2019-09-16"

keywords: reloading, os, upgrading, kvm, ha, standalone

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Reloading the OS
{: #reloading-the-os}

The OS reload process is used to rebuild a gateway server. The process performs the following actions:

* Reload the server host's operating system (OS). This will generate a new host OS password.
* Install KVM in the operating system
* Create a vSRX VM in the KVM
* Reconfigure the vSRX with the default configuration for IBM® Cloud

The process usually requires 1 hour 40 minutes to complete. Standalone Gateways will be out of service during this period. For Juniper High Availability (HA) Gateways, when you reload the OS on one of your servers, the vSRX will failover to another server in the cluster, and continue to process data traffic. Once the reload is complete, the server will rejoin the cluster.

For a successful reload or rebuild of the cluster on an HA vSRX:

* The vSRX configuration should not be modified during the execution of the OS Reload and Rebuild Cluster operations. Examples include automated software agents attempting to modify one or both vSRX nodes. Configurations changes can corrupt the OS Reload and Rebuild Cluster operations.

* The root password for the provisioned vSRX Gateway must match the root password defined in the vSRX portal. The password in the portal was defined when the Gateway was first provisioned, and may not match the current Gateway password. If the password was changed after the initial provisioning, then use SSH to connect to the vSRX Gateway and change the root password to match. Once the passwords match, you can proceed with the OS Reload or Rebuild Cluster operation.

  <img src="images/gw-vsrx-password.png" alt="drawing" style="width: 700px;"/>

* The vSRX configuration must allow root SSH access to the vSRX Private IP, prior to the OS reload request. This is required to rejoin the cluster. Once the OS reload is complete, the SSH access may be disabled.

* **Do NOT** perform an OS reload on both servers of the Highly Available gateway at the same time.

Performing an OS reload on both servers of the HA gateway at the same time will destroy the vSRX cluster and cause the gateway to be out of service. If the vSRX cluster is destroyed, you must use the **Rebuild Cluster** option (detailed below) to re-provision vSRX and recreate the HA cluster.
{: important}

* For the Rebuild Cluster option only, the host password(s) must match the password(s) in the vSRX portal. In addition, the host OS must enable root SSH access to the vSRX Private IP prior to doing a rebuild cluster.

## Performing an OS reload
{: #performing-an-os-reload}

To reload the OS for a gateway server, perform the following procedure:

To reload your OS, perform the following procedure:

1. From your browser, open [https://cloud.ibm.com ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com){:new_window} and log into your account.
2. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the top left, then click **Classic Infrastructure**.
3. Choose **Network > Gateway Appliances**.
4. Click on the server you want to reload.
5. Click the server name in the Hardware section.
4. Select **OS Reload** from the **Actions** dropdown menu on the top right of the page.
5. In the OS Reload screen, click **Edit** for the Category that requires an update. Select **Juniper** as the Vendor, and the OS version you wish to reload.
6. Click the **Reload Above Configuration** button to proceed to the **Review** pop-up. Click **Cancel** to cancel the changes to the device and exit the screen.
7. Verify that all details in the New Configuration section are correct. Click **Next** to advance to the Confirm pop-up.
8. Click the **Confirm OS Reload** button to confirm and initiate the OS Reload. Click **Cancel** to cancel the action.
