---

copyright:
  years: 2018
lastupdated: "2019-11-13"

keywords: about, vsrx, overview, details, firewall, vpn, nat, routing, vlan

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# About IBM Cloud Juniper vSRX
{: #about-ibm-cloud-juniper-vsrx}

The vSRX provides performance, ease of configuration, and maintenance advantages with the simplicity of running on a bare metal server. The hardware is sized to handle the routing and security load associated with multiple VLANs, and it can be ordered with redundant network links and redundant RAID arrays. All vSRX features are customer-managed.
{: shortdesc}

The {{site.data.keyword.vsrx_full}} is offered in two different modes: standalone mode or High Availability (HA) cluster.

Additional documentation for {{site.data.keyword.vsrx_full}} can be found in the [Supplemental Documentation](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation) topic.
{: note}

## Firewall
{: #firewall}

The vSRX deploys to protect your environment from external and internal threats by filtering private- and public-facing traffic. Customers can manage the vSRX themselves by defining policies and rules that allow or deny (among other actions) inbound or outbound network traffic, thereby protecting their applications from internal and external approaches. Both IPv4 and IPv6 stacks are supported in a stateful manner.

## Virtual private network (VPN) gateway
{: #virtual-private-network-vpn-gateway}

Connect your on-site data center or office to the IBM Cloud using VPN tunneling by provisioning your vSRX as a network gateway device. You can use an IPsec site-to-site VPN tunnel for secure communication from your enterprise data center or office to your IBM Cloud network. Remote access IPsec VPN also is supported.

For a detailed configuration guide on VPN, please refer to the links provided in the topic [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn).

## Network address translation (NAT)
{: #network-address-translation-nat-}

With the vSRX gateway appliance, you can provision application and database servers without public network interfaces, and still allow your servers access to the Internet using _source NAT_. For enhanced security, you can protect your servers behind the gateway device, using _destination NAT_.

## Enterprise-grade routing
{: #enterprise-grade-routing}

The vSRX empowers you with greater flexibility to build connectivity between multi-tiered applications running on different isolated networks. You can set up dynamic routing using BGP, which allows you to announce your own public IP space to the IBM Cloud routers. BGP also offers more flexibility for custom private network configurations, when you're using a mix of tunnels and [Direct Link solutions](/docs/infrastructure/direct-link?topic=direct-link-overview-of-direct-link-offerings#overview-of-direct-link-offerings).

## Concepts about VLANs and the gateway appliance's role
{: #concepts-about-vlans-and-the-gateway-appliance-s-role}

A VLAN (virtual local area network) is a mechanism that segregates a physical network into many virtual segments. For convenience, traffic from multiple selected VLANs can be delivered through a single network cable, using a process commonly called "trunking."

vSRX is managed in two different interfaces: The vSRX server(s) and the Gateway Appliance fixture. The Gateway Appliance provides an interface (GUI and API) for selecting the VLANs you want to associate with your vSRX. Associating a VLAN with a Gateway Appliance reroutes (or "trunks") that VLAN and all of its subnets to your vSRX, giving you control over filtering, forwarding, and protection. Servers in an associated VLAN can be reached from other VLANs only by going through your vSRX; it is not possible to circumvent the vSRX unless you bypass or disassociate the VLAN.

By default, a new Gateway Appliance is associated with two non-removable "transit" VLANs, one each for your _public_ and _private_ networks. These networks typically are used for administration, and they can be secured by vSRX commands separately.

The vSRX can manage VLANs that are associated with it through the Gateway Appliance (only).

For information on how to manage VLANs from the **Gateway Appliances Details** screen, refer to the [Manage VLANs](/docs/infrastructure/vsrx?topic=gateway-appliance-managing-vlans-and-gateway-appliances) topic.
