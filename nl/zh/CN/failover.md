---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: working, failover, codes, failure, cli

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# 使用故障转移
{: #working-with-failover}

仅当 Juniper vSRX 网关设备以高可用性方式供应时，此部分才适用。
{: note}

本主题描述如何启动从主网关设备到备份设备的故障转移，以便在故障转移后，所有控制和数据平面流量都通过辅助网关设备进行路由。

为此，请执行以下过程：

1. 登录到主 vSRX 网关设备。

2. 通过在控制台提示符处运行 `cli` 命令来进入 CLI 方式。进入 CLI 方式时，控制台将显示节点角色：`primary` 或 `secondary`。

	确保您位于 `primary` 节点中。否则，请退出并登录到该对中的另一个 vSRX 网关设备。

2. 在主 vSRX 网关设备上，运行以下命令：

	```
	show chassis cluster status
	```
	输出应类似于以下内容：

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

	确保对于这两个冗余组，同一节点都设置为 `primary`。在不同的冗余组中可能是不同的节点设置为 `primary` 角色。 
	
	缺省情况下，对于冗余组 1，vSRX 会将 `Preempt` 设置为 `yes`，对于冗余组 0，会设置为 `no`。请参阅[此链接 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.juniper.net/documentation/en_US/junos/topics/topic-map/security-chassis-cluster-redundancy-group-failover.html){:new_window} 以了解有关抢占和故障转移行为的更多信息。
	{: note}

3. 通过在控制台提示符中运行以下命令来启动故障转移：

	```
	request chassis cluster failover redundancy-group <redundancy group number> node <node number>
	```

	选择步骤 2 的命令输出中的相应冗余组号和节点号。要对两个冗余组进行故障转移，请执行先前的命令两次，针对每个组执行一次。

4. 故障转移完成后，请验证控制台输出。现在，原来的 primary 节点应该列为 `secondary`。

5. 登录到对中的另一个 vSRX 网关。通过再次执行命令 `cli` 进入 CLI 方式，然后验证控制台输出是否显示为 `primary`。

在 Juniper vSRX 网关设备中进入 CLI 方式时，从控制平面角度，输出将显示为 `primary`。请始终检查 `show chassis cluster status` 输出，以确定哪个网关设备是数据平面角度的主网关设备。请参阅 [vSRX 缺省配置](/docs/infrastructure/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration)，以了解有关冗余组以及控制和数据平面的更多信息。
{: tip}
