

Creating the new vlan interface, zone, and address book subnet

There are five steps to setup a vSRX as a gateway for systems on a vlan:

1. Get vSRX type (HA or SA), vlan type (private or public), vlan id, and subnet(s) address along with cidr
2. create vlan interface
3. configure subnet gateway ip(s) on vlan interface
4. create a security zone associated with the vlan interface
5. create address book for the subnet

In our example we have an SA (Singlely Available) vsrx and a private vlan with
id 1439. The vlan has one subnet with address/cidr 10.150.236.128/26

To create vlan interface we need to determine its base interface according to
the following rules:

1. SA private vlan base interface is ae0.
2. SA public vlan base interface is ae1.
3. HA private vlan base interface is reth2.
4. HA public vlan base interface is reth3.

So the base interface for our vlan interface is ae0. The command to create
the vlan interface, which is just a unit of its base interface, is:
set interfaces ae0 unit 1439 vlan-id 1439

Here is the genenel form of the command to create a vlan interface:
set interfaces base_interface unit vlan_id vlan-id vlan_id

For each subnet associated with the vlan we configure gateway ip on the vlan
interface. In our case we ony have one subnet with address 10.150.236.128/26.
The gateway ip for this subnet is 10.150.236.129 which is the ip next to the
subnet ip. Here is the command to set the ip:
set interfaces ae0 unit 1439 family inet address 10.150.236.129/26

To create a security zone associated to the vlan interface we name the zone
as CUSTOMER-PRIVATE and specifu all the services:
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1898 host-inbound-traffic system-services all

Security policies use zones and addresses. So we also want to make the address
book of the subnet available. Let's name the book as VSI_PRIV_NET. To define
the book we just need to run the command:
set security address-book global address VSI_PRIV_NET 10.150.236.128/26

In summary, the commands to setup vsrx for the new vlan are:
set interfaces ae0 unit 1439 vlan-id 1439
set interfaces ae0 unit 1439 family inet address 10.150.236.129/26
set security zones security-zone CUSTOMER-PRIVATE interfaces ae0.1439 host-inbound-traffic system-services all
set security address-book global address VSI_PRIV_NET 10.150.236.128/26

In the next example the vsrx is HA (Highly Available) and the vlan has
three subnets:
10.208.110.121/29
10.186.228.145/28
10.208.237.97/29
The vlan is private and its id is 1898.

For each subnet we need to configure an ip address as well as create an
address book. Here are the eight commands to setup the vlan:

set interfaces reth2 unit 1898 vlan-id 1898
set interfaces reth2 unit 1898 family inet address 10.208.237.97/29
set interfaces reth2 unit 1898 family inet address 10.186.228.145/28
set interfaces reth2 unit 1898 family inet address 10.208.110.121/29
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1898 host-inbound-traffic system-services all
set security address-book global address VSI_PRIV_NET 10.208.237.96/29
set security address-book global address VSI_PRIV_NET1 10.186.228.144/28
set security address-book global address VSI_PRIV_NET2 10.208.110.120/29

In the final example the vsrx is HA but the vlan is public. Vlan id is 1523
and there is only one subnet which is 169.47.211.152/29. The four commands
bellow setup the vlan:

set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29

This time the base interface is reth3 because the vsrx is HA and the vlan
is public.
