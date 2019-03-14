---

copyright:
  years: 2018
lastupdated: "2018-11-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Getting Started With IBM Cloud Juniper vSRX Gateway
{: #getting-started-with-ibm-cloud-juniper-vsrx-gateway}

To get started with the IBM® Cloud Juniper vSRX Gateway, first determine whether your account is linked to IBM Cloud.

To find out whether you have a linked account, navigate to the [Customer Portal ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window} in your browser and log in. If your account is linked, you will not see a **Learn more about Bluemix!** button at the top right.

## Steps for ordering

You can order your Gateway Appliance, using one of these methods:

For a list of Known Limitations with IBM Cloud Juniper vSRX Gateway, refer to the [Known Limitations topic](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx).
{:note}

### Ordering with a linked account
If your account is linked, follow this procedure:

1.	Open the [IBM Cloud Console![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/){: new_window} and log into your account.
2.	In the left navigation, select **Infrastructure > Network > Gateway Appliances**.
3.	From the **Gateway Appliances** list, click **Create a Gateway**.
4. Choose **Juniper vSRX 15.x (up to 1 Gbps)** or **Juniper vSRX 15.x (up to 10 Gbps)** under **Gateway Vendor**.
5. Choose a **Hostname** and **Domain**.
6. Select the **High Availability Pair** option, if desired.

	<img src="images/linked_order.png" alt="drawing" style="width: 700px;"/>

7. Next, select your **Location** and the associated **Pod**, then choose your **Server** and the desired amount of **RAM**.

  Only pods that already have an associated VLAN will display here. If you wish to provision your Gateway Appliance in a pod you don't see listed, first create a VLAN there.
  {:note}

	<img src="images/linked_server.png" alt="drawing" style="width: 600px;"/>

8. Select an **SSH Key** if you want to use it to authenticate access to your new Gateway.
9. Select any optional add-ons, add any additional **Storage Disks**, then choose your desired **Uplink Port Speed**.
10. Review your selections in the **Order Summary**, then read and agree to the Third-party Software Terms.
11. Finally, click **Provision**.

### Ordering with an unlinked account
If your account is unlinked, follow this procedure:

1.	Open the [Customer Portal ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window} and log into your account.
2.	In the Customer Portal navigation, select **Network > Gateway Appliances**.
3.	From the **Gateway Appliances** list, click **Order Gateway**.
4.	From the **Order** page, select your desired data center from the dropdown menu, then choose the desired type of server hardware on which the Juniper vSRX will be provisioned.

	If you plan to use a Dual Processor Multi-Core Server, you must select **Intel Xeon 5120** as the server type.
  {:note}

5.	On the **Order** page, select the **High Availability Pair** option if desired, then select the **Memory** size.
6. 	Next, click the **Juniper** tab under **Operating System**, select **Juniper vSRX 15.x (up to 1 Gbps) Standard** for a single processor server, or **Juniper vSRX 15.x (up to 10 Gbps) Standard** for a dual processor server.
7. 	Finally, select the desired network uplink speed.
8.	Review your selections, then click **Add to Order**. Your order will be verified automatically.
9.	On the **Checkout** page, if you already own VLANs in the selected data center, select the back-end VLANs that you want to protect. Be sure to:
	* Give a hostname and domain name for your server.
	* Select an SSH key for access authentication, if desired.
	* Check all boxes for the IBM Cloud service terms and Third-party Software Terms.
10. Click **Submit Order**.

## What's next?
After your order is approved, the provisioning of your vSRX starts automatically. When the provisioning process is complete, the gateway will appear in the **Gateway Appliances** list.

Click the gateway name to open the **Gateway Details** page. You'll find the IP addresses, login username, and passwords for the device.

<img src="images/after_order.png" alt="drawing" style="width: 700px;"/>
