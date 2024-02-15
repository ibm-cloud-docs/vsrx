---

copyright:
  years: 2020
lastupdated: "2020-07-30"

keywords: management, interface, fpx0, subnets, IPs, VLAN, nodes

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Configuring the management interfaces
{: #config-mgmt-interfaces}

The {{site.data.keyword.vsrx_full}} nodes provide built-in management interfaces ("fxp0") that are not configured by default. When configured, these private interfaces can be used to communicate with the individual node, which might be useful in a high availability cluster for monitoring the status of the secondary node over SSH, ping, SNMP, and so on. Since the private IP for the vSRX floats to the primary node, it is not possible to directly access the secondary node.
{: shortdesc}

Configuration of the fxp0 interface requires IPs in a subnet that is attached to the private transit VLAN for the gateway. Although the primary subnet that comes with the gateway has IPs that might be available, it is not recommended for this use. This is because the primary subnet is reserved for the gateway provisioning infrastructure, and IP collisions might occur if additional gateways are deployed in the same pod.

You can allocate a secondary subnet for the private transit VLAN, and use IPs from this subnet to configure fxp0 and the host bridge interface for PING and SSH access. To do so, perform the following procedure:

1. [Order a portable private subnet](/classic/network/subnet/provision) and assign it to the vSRX private transit VLAN. You can find the private transit VLAN on the gateway details page.

   Ensure that the subnet includes at least 8 addresses to support 2 IPs for the host bridge interfaces, and 2 IPs for the vSRX fxp0 interfaces.
   {: note}

2. Configure the host `br0:0` bridge interfaces by using 2 IPs from the new subnet. For example:

   On Ubuntu host 0: `ifconfig br0:0 10.177.75.140 netmask 255.255.255.248`

   On Ubuntu host 1: `ifconfig br0:0 10.177.75.141 netmask 255.255.255.248`

3. Persist the bridge interface configurations across reboots by modifying `/etc/network/interfaces` on each Ubuntu host. For example:

   ```text
   auto br0:0
   iface br0:0 inet static
   address 10.177.75.140
   netmask 255.255.255.248
   post-up /sbin/ifconfig br0:0 10.177.75.140 netmask 255.255.255.248
   ```

4. Assign the 2 IPs to the vSRX fxp0 interface and create backup router configurations for access to the secondary node's fxp0 interface:

   ```sh
   set groups node0 interfaces fxp0 unit 0 family inet address 10.177.75.138/29
   set groups node1 interfaces fxp0 unit 0 family inet address 10.177.75.139/29
   set groups node0 system backup-router 10.177.75.137 destination [ 0.0.0.0/1 128.0.0.0/1 ]
   set groups node1 system backup-router 10.177.75.137 destination [ 0.0.0.0/1 128.0.0.0/1 ]
   ```

   Additional information on configuring the backup router can be found in [this Juniper article](https://supportportal.juniper.net/s/article/SRX-Cannot-manage-SRX-via-fxp0-when-destination-in-Backup-Router-is-0-0?language=en_US){: external}.
   {: note}

5. Create a static route to the subnet. For example:

   `set routing-options static route 10.177.75.136/29 next-hop 10.177.75.137`

6. Create firewall filters to allow PING and SSH to the fxp0 management interfaces:

   ```sh
   set firewall filter PROTECT-IN term PING from destination-address 10.177.75.136/29
   set firewall filter PROTECT-IN term SSH from destination-address 10.177.75.136/29
   ```
