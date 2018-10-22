---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# About
IBM Cloud Juniper vSRX allows you to selectively route private and public network traffic through a full-featured enterprise level firewall that is powered by JunOS software features, such as full routing stacks, QoS and traffic sharing, policy-based routing, and VPN. The vSRX provides performance, ease of configuration and maintenance advantages with the simplicity of running on a bare metal server. The hardware is sized to handle the routing/security load for multiple VLANs and can be ordered with redundant network links and redundant RAID arrays. All vSRX features are customer-managed.

The IBM Cloud vSRX is offered in two different modes: standalone or High Availability (HA) cluster.

**NOTE:** Additional documentation for IBM Cloud Juniper vSRX can be found in the [Supplemental Documentation](vsrx-docs.html) topic.

##Firewall
The vSRX deploys to protect your environment from external and internal threats by filtering both private and public facing traffic. Customers can manage the vSRX themselves by defining policies and rules to allow or deny (among other actions) inbound or outbound network traffic, protecting their applications from internal and external users. Both IPv4 and IPv6 stacks are supported in a stateful manner. 

## Virtual Private Network (VPN) Gateway
Connect your on-site data center or office to the IBM Cloud using VPN tunneling by provisioning your vSRX as a network gateway device. You can use an IPsec site-to-site VPN tunnel for secure communication from your enterprise data center or office to your IBM Cloud network. Remote access IPSEC VPN is also supported.

For a detailed configuration guide on VPN, please refer to the links provided in the topic [VPN](vpn.html).

## Network Address Translation (NAT)
With the vSRX gateway appliance, you can provision application and database servers without public network interfaces while still allowing your servers to access the Internet using Source NAT. You can also hide your servers behind the gateway device with Destination NAT for enhanced security.

## Enterprise-grade Routing
For multi-tiered applications on different isolated networks, the vSRX enables you to build connectivity between these networks with greater flexibility. You can set up dynamic routing using BGP, which allows you to announce your own public IP space to the IBM Cloud routers. BGP will also offer more flexibility for custom private network configurations when using a mix of tunnels and direct link solutions.
