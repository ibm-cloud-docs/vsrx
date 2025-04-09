---

copyright:
  years: 2017, 2025
lastupdated: "2025-04-09"

keywords: ordering, gateway, appliance, vsrx, license

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with IBM Cloud Juniper vSRX
{: #getting-started-vsrx}

{{site.data.keyword.vsrx_full}} allows you to route private and public network traffic on a per VLAN basis, through a full-featured, enterprise-level firewall that is powered by Junos OS software features. This gives you the ability to manage your VLANs, interfaces, subnets and routing as well as create security policies and VPNs for secure access to and between your cloud services.
{: shortdesc}

For a list of known limitations with {{site.data.keyword.vsrx_full}} Gateway, see [Known limitations](/docs/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx).
{: note}

## Choosing a vSRX license
{: #choosing-vsrx-license}

Three license types are available for your {{site.data.keyword.vsrx_full}}:

* Standard
* Content Security Bundle (CSB)
* Remote access VPN users (50 concurent users)

The CSB license is not available on vSRX gateways that are running with Linux Bridge based network models. The license is only available on SR-IOV enabled gateways. Details can be found [here](/docs/vsrx?topic=vsrx-unsupported-upgrade).
{: note}

Remote VPN user licenses are only supported on versions 22.2 and later.
{: note}

Each license includes a different set of features and options, and the following table outlines the differences.

| License Type  | Features |
| ------------- | ------------- |
| **Standard** | - Core security: firewall, ALG, screens, user firewall  \n - IPsec VPN (site-to-site VPN)  \n - NAT  \n - CoS  \n - Routing services: BGP, OSPF, DHCP, J-Flow, IPv4  \n - Foundation: Static routing, management (J-Web, CLI, and NETCONF), on-box logging, diagnostics |
| **Content Security Bundle (CSB)**  \n Includes all Standard features, along with the additional features listed in the next column. | - AppSecure  \n  - Application Tracking (AppTrack)  \n  - Application Firewall (AppFW)  \n  - Application Quality of Service (AppQoS)  \n  - Advanced policy-based routing (APBR)  \n  - Application Quality of Experience (AppQoE)  \n - User Firewall  \n - IPS  \n  - UTM  \n  - Anti Virus  \n  - Anti Spam  \n  - Web Filtering   \n  - Content Filtering  \n  - SSL Proxy  \n  - SSL Forward Proxy  \n  - SSL Reverse Proxy  \n  - SSL Decrypting Mirror |
| **Remote access VPN users** \n Juniper Secure Connect - SSL VPN and IPSEC | - VPN user license (50 concurrent users per license) \n - Select up to 10 licenses \n - Securely and automatically validates that the most current security policy is enforced \n  - Supports external multifactor authentication (MFA) solutions \n  - Provides integrated biometric authentication on devices with hardware support
{: caption="License differences" caption-side="bottom"}

You can specify your license type when you order your vSRX, as well as change the license by using the [Gateway Appliance Details](/docs/vsrx?topic=vsrx-vsrx-licenses#vsrx-licenses) page.
{: note}

## Ordering a vSRX
{: #ordering-vsrx-with-a-linked-account}

You can order your {{site.data.keyword.vsrx_full}} by following these steps:

1. From your browser, open the Gateway Appliances page in the [IBM Cloud catalog](/gen1/infrastructure/provision/gateway){: external} and log in to your account.

   You can also get here by logging in to the [IBM Cloud UI console](/login){: external} and selecting **Infrastructure > Classic Infrastructure**. Then click **Network > Gateway Appliances**. Alternatively, from the [IBM Cloud catalog](/catalog){: external}, select the **Networking** category then choose the **Gateway Appliance** tile.

2. Choose **Juniper vSRX (up to 1 Gbps)** or **Juniper vSRX (up to 10 Gbps)** under **Gateway Vendor**.

3. Choose your license type from **license add-ons**, either Standard or CSB.

   See the previous section for information on the features offered with each license.
   {: tip}

4. From the **Gateway appliance** section, enter your **Hostname** and **Domain** name information. These fields are already be populated with default information, so ensure that the values are correct.

5. Check the **High Availability** option if needed, then select a data center **Location**, and the specific **Pod** you want from the menu.

   Only pods that already have an associated VLAN are displayed here. If you want to provision your gateway appliance in a pod you don't see listed, first create a VLAN there.
   {: note}

6. From the **Configuration** section, choose your processor's RAM. You can also define an SSH key, if you want to use it to authenticate access to your new Gateway.

   The appropriate processor is chosen for you based on the license version you selected in step two. However, you can choose different RAM configurations.
   {: note}

7. From the **Storage disks** section, choose the options that meet your storage requirements.

   RAID configurations are available for customizing storage performance, size and data protection. RAID1 or RAID10 are recommended for a combination of data protection and performance. RAID0 provides the highest read/write performance with the least data protection. If you choose RAID0, ensure that you have a data backup plan. A disk failure will mean the complete rebuild of the RAID with new disks, as well as the rebuilding and reloading of the appliance.

   You can have up to four disks per vSRX. "Disk size" with a RAID configuration is the usable disk size, as RAID configurations changes the amount of available storage. This does not apply to RAID0.
   {: tip}

8. From the **Network interface** section, select your **Uplink port speeds**. The default selection is a single interface, but redundant and private only options are available as well. Choose the one that best fits your needs.

   The Network Interface **Add Ons** section allows you to select an IPv6 address if required, and shows you any additional included default options.

9. Review your selections, check that you read the Third-Party Service Agreements, then click **Create**. The order is verified automatically.

After your order is approved, the provisioning of your {{site.data.keyword.vsrx_full}} Gateway starts automatically. When the provisioning process is complete, the new vSRX appears in the Gateway Appliances list page. Click the gateway name to open the Gateway Details page. The IP addresses, login username, and password for the device appear.

After you order and configure your gateway from the IBM Cloud catalog, you must also login to and configure the device itself with customized configurations for your cloud environment. This includes VLAN interfaces, subnet gateway IP addresses, security policies and any additional features that you require.
{: tip}

## Next steps
{: #what-s-next-}

After your order is approved, the provisioning of your vSRX starts automatically. When the provisioning process is complete, the gateway appears in the [Gateway Appliances](/docs/gateway-appliance?topic=gateway-appliance-viewing-all-gateway-appliances) list.

Click the gateway name to open the **Gateway Details** page. You find the IP addresses, login username, and passwords for the device.
