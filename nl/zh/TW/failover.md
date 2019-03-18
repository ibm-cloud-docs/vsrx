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

# 使用失效接手
{: #working-with-failover}

**附註：**只有在「高可用性」模式中已佈建您的 Juniper vSRX 閘道裝置時，本節才適用。

本主題說明如何從主要閘道裝置起始失效接手至備份裝置，以在失效接手之後透過次要閘道裝置遞送所有控制及資料平面資料流量。

若要這樣做，請執行下列程序：

1. 登入主要 vSRX 閘道裝置。

2. 在主控台提示中執行 `cli` 指令，以進入 CLI 模式。當您進入 CLI 模式時，主控台會顯示節點角色，即 `primary` 或 `secondary`。

	確定您位於 `primary` 節點。如果不是，請退出然後登入配對的另一個 vSRX 閘道裝置。

2. 在主要 vSRX 閘道裝置上，執行以下指令：

	```
	show chassis cluster status
	```
	其輸出應該類似於下列內容：

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

	確定針對這兩個備援群組，將相同節點設為 `primary`。在不同的備援群組中，不同的節點有可能設為 `primary` 角色。

3. 在主控台提示中執行下列指令，以起始失效接手：

	```
	request chassis cluster failover redundancy-group <redundancy group number> node <node number>
	```

	從步驟 2 的指令輸出中，選取適當的備援群組號碼及節點號碼。若要失效接手這兩個備援群組，請執行前一個指令兩次，每個群組一次。

4. 在失效接手完成之後，請驗證主控台輸出。它現在應該列為 `secondary`。

5. 登入配對的另一個 vSRX 閘道。再次執行 `cli` 指令以進入 CLI 模式，然後驗證主控台輸出顯示為 `primary`。

**附註：**當您在 Juniper vSRX 閘道裝置中進入 CLI 模式時，輸出會在控制平面視景中顯示為 `primary`。請務必檢查 `show chassis cluster status` 輸出，以從資料平面視景中判定哪個閘道裝置是主要的。請參閱 [vSRX 預設配置](/docs/infrastructure/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration)，以進一步瞭解備援群組，以及控制和資料平面。
