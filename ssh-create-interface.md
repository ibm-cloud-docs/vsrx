---

copyright:
  years: 2018
lastupdated: "2019-11-14"

keywords: create, creating, interface, zone, address, subnets, ssh

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank_"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# Creating the new interface, zone, and address book subnet
{: #creating-the-new-interface-zone-and-address-book-subnet}

First, you'll need to create an interface unit for the VLAN and add the subnet's gateway address. You'll then be able to create a security zone associated with the new unit and an `address-book` entry for the subnet.
{: shortdesc}

The following examples detail a Highly Available (HA) vSRX cluster in both a private and public side configuraton. You must configure all associated private VLANs on `reth2`, and all associated public VLANs on `reth3`. After provisioning, the public WAN connection will be configured on `reth1`, and the private WAN connection on`reth0`. For each subnet on an associated VLAN, the subnet gateway needs to be configured on the VLAN interface(s). The second IP in the customer subnet, immediately following the network ID, is the subnet gateway. In the following example, `10.186.228.145/28` is the subnet gateway of `10.186.228.144/28` on the private VLAN, `1898`.

For more information on associated VLANS, refer to [Managing VLANs with a gateway appliance](/docs/vsrx?topic=gateway-appliance-managing-vlans-and-gateway-appliances).
{: note}

Private side configuration example:

```sh
set interfaces reth2 vlan-tagging
set interfaces reth2 redundant-ether-options redundancy-group 1
set interfaces reth2 unit 1898 vlan-id 1898
set interfaces reth2 unit 1898 family inet address 10.186.228.145/28
set interfaces reth2 unit 1898 family inet address 10.208.110.121/29
set interfaces reth2 unit 1898 family inet address 10.208.237.97/29
set security zones security-zone SL-PRIVATE interfaces reth2.1898 host-inbound-traffic system-services all
set security address-book global address VSI_PRIV_NET 10.208.237.96/29
set security address-book global address VSI_PRIV_NET1 10.186.228.144/28
set security address-book global address VSI_PRIV_NET2 10.208.110.120/29
```
{: codeblock}

Public side configuration example:

```sh
set interfaces reth3 vlan-tagging
set interfaces reth3 redundant-ether-options redundancy-group 1
set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29
```
{: codeblock}

## Filtering on loopback considerations
{: #loopback-considerations}

The `PROTECT-IN` filter on loopback blocks (by default) all local traffic traveling to and from the vSRX that hasn't been explicitly allowed. As a result, in order to ping the subnet gateways defined previously, or to ping servers on those subnets from the vSRX, the subnet gateways must be added to `PROTECT-IN`. This is configured by default for the `reth1` and `reth0` IP addresses and is why they are accessible after provisioning.


```sh
set firewall filter PROTECT-IN term PING from destination-address 10.208.237.97/32
set firewall filter PROTECT-IN term PING from destination-address 10.208.110.121/32
set firewall filter PROTECT-IN term PING from destination-address 10.186.228.145/32
set firewall filter PROTECT-IN term PING from destination-address 169.47.211.153/32
set firewall filter PROTECT-IN term PING from protocol icmp
set firewall filter PROTECT-IN term PING then accept
```
{: codeblock}
