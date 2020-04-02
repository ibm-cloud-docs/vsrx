---

copyright:
  years: 2018
lastupdated: "2019-11-14"

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
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Rebuilding a High Availability (HA) vSRX cluster
{: #rebuilding-an-ha-cluster}
{: help}
{: support}

You can rebuild a High Availability (HA) {{site.data.keyword.vsrx_full}} cluster using the information here.
{: shortdesc}

Rebuilding an HA vSRX cluster is a very destructive procedure, and should be used only in a few specific scenarios. Consult your IBM Support representative before beginning this procedure.
{: important}

For a successful rebuild of a cluster on an HA vSRX, ensure the following:

* The vSRX configuration should not be modified during the execution of the Rebuild Cluster operations. Examples include automated software agents attempting to modify one or both vSRX nodes. Configurations changes can corrupt the Rebuild Cluster operation.

* The root password for the provisioned vSRX Gateway must match the root password defined in the vSRX portal. The password in the portal was defined when the Gateway was first provisioned, and may not match the current Gateway password. If the password was changed after the initial provisioning, then use SSH to connect to the vSRX Gateway and change the root password to match. Once the passwords match, you can proceed with the Rebuild Cluster operation.

  ![vSRX Password](images/gw-vsrx-password.png "vSRX Password")

* The host password(s) must match the password(s) in the vSRX portal. In addition, the host OS must enable root SSH access to the vSRX Private IP prior to doing a rebuild cluster.

## Rebuilding an HA cluster

To rebuild one of your HA vSRX clusters, perform the following procedure:

1. From your browser, open [https://cloud.ibm.com ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com){:new_window} and log into your account.
2. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the top left, then click **Classic Infrastructure**.
3. Choose **Network > Gateway Appliances**.
4. Click on the server you want to reload.
5. Click the server name in the Hardware section.
6. Click the **Actions** dropdown and select **Rebuild Cluster**.
7. Carefully read the warning message. The operation to rebuild a cluster is destructive. If you wish to proceed, save your vSRX configuration before clicking **Rebuild** to start the process.
