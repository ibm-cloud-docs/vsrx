---

copyright:
  years: 2018, 2020
lastupdated: "2023-03-02"

keywords: ordering, gateway, appliance, vsrx, license

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Setting up your vSRX as a VLAN gateway
{: #vsrx-vlan-zone-address}

This topic provides examples on setting up your vSRX as a gateway for systems on a VLAN. 
{: shortdesc}

You need to know:

* Your vSRX type, Highly Available (HA) or Singularly Available (SA)
* The VLAN you want to connect to and its type (private or public)
* The ID of that vlan
* The subnet addresses along with the CIDR

## Example 1
{: #vsrx-vlan1}

In this example, we have an SA vSRX and a private VLAN with an ID of 1439. The VLAN has one subnet with the address/CIDR `10.150.236.128/26`.

To create the example VLAN interface, you need to determine its base interface according to the following settings:

1. SA private vlan base interface is `ae0`.
2. SA public vlan base interface is `ae1`.
3. HA private vlan base interface is `reth2`.
4. HA public vlan base interface is `reth3`.

In this case, the base interface is `ae0`. 

To create the VLAN interface, run this command: `set interfaces base_interface unit vlan_id vlan-id vlan_id`.

For example:

```sh
set interfaces ae0 unit 1439 vlan-id 1439
```
{: pre}

For each subnet associated with the VLAN, the gateway IP is configured on the vlan interface. 

In this case, we have only one subnet with an address of `10.150.236.128/26`. The gateway IP for this subnet is `10.150.236.129`, which is the IP next to the subnet IP. 

To set the IP, run the following command:

```sh
set interfaces ae0 unit 1439 family inet address 10.150.236.129/26
```
{: pre}

To create a security zone associated with the VLAN interface, name the zone `CUSTOMER-PRIVATE` and specify all its services:

```sh
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1898 host-inbound-traffic system-services all
```
{: pre}

Security policies use zones and addresses. As a result, you must also make the address book of the subnet available. In this example, the name of the book is `VSI_PRIV_NET`. To define the book, run the command:

```sh
set security address-book global address VSI_PRIV_NET 10.150.236.128/26
```
{: pre}

## Example 2
{: #vsrx-vlan2}

The next example depicts a HA vSRX and a VLAN with three subnets:

* `10.208.110.121/29`
* `10.186.228.145/28`
* `10.208.237.97/29`

The VLAN is private and its ID is `1898`.

You must configure an IP address and an address book for each of the three subnets. Use the following eight commands (in the same order as the ones illustrated in the first example) to configure the VLAN:

```sh
set interfaces reth2 unit 1898 vlan-id 1898
set interfaces reth2 unit 1898 family inet address 10.208.237.97/29
set interfaces reth2 unit 1898 family inet address 10.186.228.145/28
set interfaces reth2 unit 1898 family inet address 10.208.110.121/29
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1898 host-inbound-traffic system-services all
set security address-book global address VSI_PRIV_NET 10.208.237.96/29
set security address-book global address VSI_PRIV_NET1 10.186.228.144/28
set security address-book global address VSI_PRIV_NET2 10.208.110.120/29
```
{: pre}

## Example 3
{: #vsrx-vlan3}

In the final example, the vSRX is HA but the VLAN is public. Its ID is `1523` and there is only one subnet: `169.47.211.152/29`. Use the following four commands (in the same order as the ones illustrated in the first example) to configure the VLAN:

```sh
set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29
```
{: pre}

Here, the base interface is `reth3`, as the vSRX is HA and the VLAN is public.
