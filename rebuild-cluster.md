---

copyright:
  years: 2018
lastupdated: "2019-10-31"

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

# Rebuilding an HA vSRX Cluster
{: #rebuilding-an-ha-cluster}

Rebuilding an HA vSRX cluster is a very destructive procedure, and should be used only in a few specific scenarios. Consult your IBM Support representative before beginning this procedure.
{: important}

To rebuild one of your HA vSRX clusters, perform the following procedure:

1. From your browser, open [https://cloud.ibm.com ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com){:new_window} and log into your account.
2. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the top left, then click **Classic Infrastructure**.
3. Choose **Network > Gateway Appliances**.
4. Click on the server you want to reload.
5. Click the server name in the Hardware section.
6. Click the **Actions** dropdown and select **Rebuild Cluster**.
7. Carefully read the warning message. The operation to rebuild a cluster is destructive. If you wish to proceed, save your vSRX configuration before clicking **Rebuild** to start the process.
