---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: reloading, migrating, os, upgrading, kvm, ha, standalone

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

# Reloading and Migrating the OS
{: #reloading-an-migrating-the-os}

The OS Reload process is used to rebuild a gateway server. The process performs the following actions:

* Reload the server host's operating system
* Install KVM in the operating system
* Create a vSRX VM in the KVM
* Reconfigure the vSRX with the default configuration for IBM® Cloud

The process usually requires 1 hour 40 minutes to complete. Standalone Gateways will be out of service during this period. For Juniper High Availability (HA) Gateways, when you reload the OS on one of your servers, the vSRX will failover to another server in the cluster, and continue to process data traffic. Once the reload is complete, the server will rejoin the cluster.

If you're already running a Juniper vSRX HA cluster, do not perform an OS reload on both servers of the HA Gateway at the same time. Doing so will destroy the vSRX cluster and cause the Gateway to be out of service. If the vSRX cluster is destroyed, you must use the **Rebuild Cluster** option (detailed below) to re-provision vSRX and recreate the HA cluster.
{: important}

## Performing an OS reload
To reload the OS for a gateway server, perform the following procedure:

1. [Access the Gateway Appliances screen](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) in the Customer Portal, and navigate to the Gateway details page by selecting desired Gateway name.

  <img src="images/gw-sa-details.png" alt="drawing" style="width: 700px;"/>

2. Click the server name in the Hardware Panel.

  ![Hardware Server](images/os_hardware.png)

3. On the device's page, click **OS Reload** in the Action drop down menu to access the Server Configuration page.

  ![Device Details](images/os_device_page.png)

4. On the Server Configuration page, you can configure and start the reload. If you're reloading from a different OS, click the **Edit** next to **Operating System**, select **Juniper**, then pick one of the Juniper vSRX 15.x Standard options. When you are done modifying your settings, select **Reload Above Configuration** to continue.

5. The OS Reload details screen displays. Review the settings you have chosen, and click **Edit Settings** if changes are required. Otherwise, click **Next** to proceed.

6. On the OS Reload confirmation screen, agree to the terms of the Master Service Agreement, then begin the OS Reload process by clicking **Confirm OS Reload**. If you do not want to proceed with the reload, click **Cancel**.

## Migrating from a Vyatta/VRA Server to a Juniper vSRX using OS Reload
If you are reloading a standalone Vyatta Server, then a standalone Juniper vSRX will be provisioned once the OS reload completes. The same gateway IP addresses will be used, and the password for the root user on the host server (as well as the password for the admin and root users in the vSRX) will be reset.

If you are reloading High Availability Vyatta Servers, you must perform an OS Reload on both hardware servers. This installs Ubuntu 16.04. Next, use the Rebuild Cluster option (detailed in the following section) to provision the vSRX and create the HA cluster. As with a Standalone vSRX, the same gateway IP addresses will be used, and the password for the root user on the host server (as well as the password for the admin and root users in the vSRX) will be reset.

Do not perform an OS Reload on only one server of the Vyatta HA cluster. Having two different Operating Systems on a single Gateway HA cluster is not supported.
{: important}

## Rebuilding an HA vSRX Cluster
To rebuild one of your HA vSRX clusters, perform the following procedure:

1. [Access the Gateway Appliances screen](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) in the Customer Portal, and navigate to the Gateway details page by selecting the desired HA Gateway name.

2. Click the **Actions** dropdown and select **Rebuild Cluster**.

3. Carefully read the warning message. The operation to rebuild a cluster is destructive. If you wish to proceed, save your vSRX configuration before clicking **Rebuild** to start the process.

  ![Confirm Rebuild Cluster](images/rebuild_cluster_confirm.png)
