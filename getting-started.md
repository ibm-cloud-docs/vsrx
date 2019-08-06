---

copyright:
  years: 2018
lastupdated: "2019-05-03"

keywords: vsrx, ordering, gateway, appliance

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

# Getting Started With IBM Cloud Juniper vSRX
{: #getting-started}

To get started with the {{site.data.keyword.vsrx_full}} Gateway, first determine whether your account is linked to IBM Cloud.

To find out whether you have a linked account, navigate to the [Customer Portal ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window} in your browser and log in. If your account is linked, you will not see a **Learn more about Bluemix!** button at the top right.

## Steps for ordering
{: #steps-for-ordering}

You can order your Gateway Appliance, using one of these methods:

For a list of Known Limitations with {{site.data.keyword.vsrx_full}} Gateway, refer to the [Known Limitations topic](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx).
{: note}

### Ordering with a linked account
{: #ordering-with-a-linked-account}

If your account is linked, follow this procedure:

1. From your browser, open the Gateway Appliances page in the [Cloud Catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/gen1/infrastructure/provision/gateway){: new_window} and log into your account.

  You can also get to this page by logging into the [IBM Cloud UI Console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com) and selecting **Classic Infrastructure > Network > Gateway appliance**.
Alternatively, from the [IBM Cloud Catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog), select the **Network** category then choose the **Gateway Appliance** tile.

2. Choose **Juniper vSRX (up to 1 Gbps)** or **Juniper vSRX (up to 10 Gbps)** under **Gateway Vendor**.

3. From the **Gateway appliance** section, enter your **Hostname** and **Domain** name information. These fields will already be populated with default information, so ensure the values are correct.

	<img src="images/linked_order.png" alt="drawing" style="width: 700px;"/>

4. Check the **High Availability** option if desired, then select your desired data center **Location**, and the specific **Pod** you want from the dropdown menu.

  Only pods that already have an associated VLAN will display here. If you wish to provision your Gateway Appliance in a pod you don't see listed, first create a VLAN there.
  {: note}

	<img src="images/linked_server.png" alt="drawing" style="width: 600px;"/>

5. From the **Configuration** section, choose your processor's RAM. You can also define an SSH key, if you want to use it to authenticate access to your new Gateway.

  The appropriate processor is chosen for you based on the license version you selected in step two. You can choose different RAM configurations, however.
  {: note}

6. From the **Storage disks** section, choose the options that meet your storage requirements.

  RAID0 and RAID1 options are available for added protection against data loss, as are hot spares (backup components that can be placed into service immediately when a primary component fails).
  {: note}

  You may have up to four disks per vSRX. "Disk size" with a RAID configuration is the usable disk size, as RAID configurations are mirrored.
  {: note}

  Reserve more than the default disk setting if you plan to run network diagnostics that generate detailed logs.
  {: tip}

7. From the **Network interface** section, select your **Uplink port speeds**. The default selection is a single interface, but there are redundant and private only options as well. Choose the one that best fits your needs.

  The Network Interface **Add Ons** section allows you to select an IPv6 address if required, and shows you any additional included default options.

8. Review your selections, check that you have read the Third Party Service Agreements, then click **Create**. The order is verified automatically.

After your order is approved, the provisioning of your {{site.data.keyword.vsrx_full}} Gateway starts automatically. When the provisioning process is complete, the new vSRX will appear in the Gateway Appliances list page. Click the gateway name to open the Gateway Details page. You will find the IP addresses, login username, and password for the device.  

Remember that once you order and configure your gateway from the IBM Cloud Catalog, you must also configure the device itself with the same settings.
{: tip}

### Ordering with an unlinked account
{: #ordering-with-a-unlinked-account}

If your account is unlinked, follow this procedure:

1.	Open the [Customer Portal ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window} and log into your account.
2.	In the Customer Portal navigation, select **Network > Gateway Appliances**.
3.	From the **Gateway Appliances** list, click **Order Gateway**.
4.	From the **Order** page, select your desired data center from the dropdown menu, then choose the desired type of server hardware on which the Juniper vSRX will be provisioned.

	If you plan to use a Dual Processor Multi-Core Server, you must select **Intel Xeon 5120** as the server type.
  {: note}

5.	On the **Order** page, select the **High Availability Pair** option if desired, then select the **Memory** size.
6. 	Next, click the **Juniper** tab under **Operating System**, select **Juniper vSRX (up to 1 Gbps) Standard** for a single processor server, or **Juniper vSRX (up to 10 Gbps) Standard** for a dual processor server.
7. 	Finally, select the desired network uplink speed.
8.	Review your selections, then click **Add to Order**. Your order will be verified automatically.
9.	On the **Checkout** page, if you already own VLANs in the selected data center, select the back-end VLANs that you want to protect. Be sure to:
	* Give a hostname and domain name for your server.
	* Select an SSH key for access authentication, if desired.
	* Check all boxes for the IBM Cloud service terms and Third-party Software Terms.
10. Click **Submit Order**.

## What's next?
{: #what-s-next-}

After your order is approved, the provisioning of your vSRX starts automatically. When the provisioning process is complete, the gateway will appear in the **Gateway Appliances** list.

Click the gateway name to open the **Gateway Details** page. You'll find the IP addresses, login username, and passwords for the device.

<img src="images/after_order.png" alt="drawing" style="width: 700px;"/>
