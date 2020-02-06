---

copyright:
  years: 2018
lastupdated: "2019-11-13"

keywords: working, failover, codes, failure, cli

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Working with Failover
{: #working-with-failover}
{: help}
{: support}

You can initiate failover from your primary {{site.data.keyword.vsrx_full}} to a backup device, so that all control and data plane traffic is routed through the secondary gateway device after failover.
{: shortdesc}

This section is only applicable if your Juniper vSRX gateway devices are provisioned in High-Availability mode.
{: note}

To do so, perform the following procedure:

1. Login to your primary vSRX gateway device.

2. Enter CLI mode by running the command `cli` at the console prompt. When you enter CLI mode, the console displays the node role, either `primary` or `secondary`.

	Ensure that you are in the `primary` node. If you are not, exit and login to the other vSRX gateway device of the pair.

2. On the primary vSRX gateway device, run the command:

	```
	show chassis cluster status
	```
	The output should be similar to the following:

	```
	Monitor Failure codes:
		CS  Cold Sync monitoring        FL  Fabric Connection monitoring
		GR  GRES monitoring             HW  Hardware monitoring
		IF  Interface monitoring        IP  IP monitoring
		LB  Loopback monitoring         MB  Mbuf monitoring
		NH  Nexthop monitoring          NP  NPC monitoring
		SP  SPU monitoring              SM  Schedule monitoring
		CF  Config Sync monitoring

	Cluster ID: 2
	Node   Priority Status         Preempt Manual   	Monitor-failures

	Redundancy group: 0 , Failover count: 1
	node0  100      primary        no      no       None
	node1  1        secondary      no      no       None
	Redundancy group: 1 , Failover count: 1
	node0  100      primary        yes     no       None
	node1  1        secondary      yes     no       None

	{primary:node0}
	```

	Ensure that, for both redundancy groups, the same node is set as `primary`. It is possible for different nodes to be set as the `primary` role in different redundancy groups.

	The vSRX, by default, sets `Preempt` to `yes` for Redundancy group 1, and `no` for Redundancy group 0. Refer to [this link ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.juniper.net/documentation/en_US/junos/topics/topic-map/security-chassis-cluster-redundancy-group-failover.html){:new_window} to learn more about pre-emption and failover behavior.
	{: note}

3. Initiate failover by running the following command in the console prompt:

	```
	request chassis cluster failover redundancy-group <redundancy group number> node <node number>
	```

	Select the appropriate redundancy group number and node number from the output of the command in step two. To failover both redundancy groups, execute the previous command twice, one for each group.

4. After failover is complete, verify the console output. It should now be listed as `secondary`.

5. Login to the other vSRX gateway of your pair. Enter into CLI mode by again executing the command `cli` and then verify that the console output shows as `primary`.

When you enter CLI mode in your Juniper vSRX gateway device, the output will show as `primary` from the control plane perspective. Always check the `show chassis cluster status` output to determine which gateway device is primary from data plane perspective. Refer to [vSRX Default Configuration](/docs/infrastructure/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration) to learn more about redundancy groups, as well as the control and data planes.
{: tip}
