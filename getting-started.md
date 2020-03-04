---

copyright:
  years: 2018
lastupdated: "2020-02-21"

keywords: vsrx, ordering, gateway, appliance

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:preview: .preview}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Getting started with IBM Cloud Juniper vSRX
{: #getting-started}

{{site.data.keyword.vsrx_full}} allows you to route private and public network traffic selectively, through a full-featured, enterprise-level firewall that is powered by JunOS software features, such as full routing stacks, QoS and traffic sharing, policy-based routing, and VPN.
{: shortdesc}

For a list of Known Limitations with {{site.data.keyword.vsrx_full}} Gateway, refer to the [Known Limitations topic](/docs/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx).
{: note}

## Choosing a vSRX license
{: #choosing-license}

Currently, only {{site.data.keyword.vsrx_full}} 10G Standalone configurations can choose between the following license options. Full support for the various vSRX configurations, including 1G and High Availability, will be introduced soon.
{: important}

There are two license types available for your {{site.data.keyword.vsrx_full}}:

* Standard
* Content Security Bundle (CSB)

Each license includes a different set of features and options, and the following table outlines the differences.

| License Type  | Features |
| ------------- | ------------- |
| **Standard** | <ul><li>Core security: firewall, ALG, screens, user firewall</li><li>IPsec VPN (site-to-site VPN)</li><li>NAT</li><li>CoS</li><li>Routing services: BGP, OSPF, DHCP, J-Flow, IPv4</li><li>Foundation: Static routing, management (J-Web, CLI, and NETCONF), on-box logging, diagnostics</li></ul> |
| **Content Security Bundle (CSB)** <br></br><br>Includes all Standard features, along with the additional features listed in the next column.</br> | <ul><li>AppSecure<ul><li>Application Tracking (AppTrack)</li><li>Application Firewall (AppFW)</li><li>Application Quality of Service (AppQoS)</li><li>Advanced policy-based routing (APBR)</li><li>Application Quality of Experience (AppQoE)</li></ul></li></ul><ul><li>User Firewall<li>IPS</li><li>UTM</li><ul><li>Anti Virus</li><li>Anti Spam</li><li>Web Filtering</li><li>Content Filtering</li></ul><br></br><li>SSL Proxy</li><ul><li>SSL Forward Proxy</li><li>SSL Reverse Proxy</li><li>SSL Decrypting Mirror</li></ul></li></ul> |

You can specify your license type when ordering your vSRX, as well as change the license using the [Gateway Appliance Details](/docs/vsrx?topic=vsrx-performing-ibm-cloud-juniper-vsrx-basics#vsrx-licenses) page.
{: note}

### Ordering a vSRX
{: #ordering-with-a-linked-account}

IBM Cloud has temporarily suspended new sales of 1G Highly Available (HA) Juniper installations. This restriction is due to a pending design change that is required to improve HA stability. The offering is projected to become available again in Q2 2020.
{: preview}

You can order your {{site.data.keyword.vsrx_full}} by performing the following procedure:

1. From your browser, open the Gateway Appliances page in the [Cloud Catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/gen1/infrastructure/provision/gateway){: new_window} and log into your account.

  You can also get to this page by logging into the [IBM Cloud UI Console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com) and selecting **Classic Infrastructure > Network > Gateway appliance**. Alternatively, from the [IBM Cloud Catalog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/catalog), select the **Network** category then choose the **Gateway Appliance** tile.

2. Choose **Juniper vSRX (up to 1 Gbps)** or **Juniper vSRX (up to 10 Gbps)** under **Gateway Vendor**.

3. Choose your license type from **License add-ons**, either Standard or CSB.
  Refer to the previous section for information on the features offered with each license.
  {: tip}

  Currently, only {{site.data.keyword.vsrx_full}} 10G Standalone configurations can choose between license options. Full support among all the various vSRX configurations, including 1G and High Availability, will be introduced soon.
  {: important}

3. From the **Gateway appliance** section, enter your **Hostname** and **Domain** name information. These fields will already be populated with default information, so ensure the values are correct.

	![Linked order](images/linked_order.png "Linked order")

4. Check the **High Availability** option if desired, then select your desired data center **Location**, and the specific **Pod** you want from the dropdown menu.

  Only pods that already have an associated VLAN will display here. If you wish to provision your Gateway Appliance in a pod you don't see listed, first create a VLAN there.
  {: note}

	![Linked server](images/linked_server.png "Linked server")

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

## What's next?
{: #what-s-next-}

After your order is approved, the provisioning of your vSRX starts automatically. When the provisioning process is complete, the gateway will appear in the [Gateway Appliances](/docs/vsrx?topic=gateway-appliance-viewing-all-gateway-appliances) list.

Click the gateway name to open the **Gateway Details** page. You'll find the IP addresses, login username, and passwords for the device.

![After ordering](images/after_order.png "After ordering")
