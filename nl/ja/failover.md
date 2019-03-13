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

# フェイルオーバーの処理
**注:** このセクションは、Juniper vSRX ゲートウェイ・デバイスが高可用性モードでプロビジョンされる場合に限り適用できます。

このトピックでは、1 次ゲートウェイ・デバイスからバックアップ・デバイスへのフェイルオーバーを開始して、フェイルオーバー後にすべての制御プレーンやデータ・プレーンのトラフィックが 2 次ゲートウェイ・デバイスを通るように経路指定できるようにする方法について説明します。

これを行うには、以下の手順を実行します。

1. 1 次 vSRX ゲートウェイ・デバイスにログインします。

2. コンソール・プロンプトで、`cli` コマンドを実行して、CLI モードに入ります。CLI モードに入ると、コンソールに `primary` または `secondary` のいずれかのノード役割が表示されます。

	`primary` ノードで作業していることを確認します。1 次ノードでない場合は終了して、ペアの他方の vSRX ゲートウェイ・デバイスにログインします。

2. 1 次 vSRX ゲートウェイ・デバイスで、以下のコマンドを実行します。

	```
	show chassis cluster status
	```
	出力は以下のようになります。

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

	両方の冗長グループについて、同じノードが `primary` として設定されていることを確認します。冗長グループが異なると、`primary` 役割として設定されているノードも異なる可能性があります。

3. コンソール・プロンプトで以下のコマンドを実行して、フェイルオーバーを開始します。

	```
	request chassis cluster failover redundancy-group <冗長グループ番号> node <ノード番号>
	```

	ステップ 2 のコマンドの出力から、該当する冗長グループ番号とノード番号を選択します。両方の冗長グループをフェイルオーバーするには、前述のコマンドをグループごとに 1 回ずつ合計 2 回実行します。

4. フェイルオーバーの完了後に、コンソール出力を確認します。今回は `secondary` としてリストされるはずです。

5. ペアの他方の vSRX ゲートウェイにログインします。再度 `cli` をコマンド実行して CLI モードに入ってから、コンソール出力で `primary` として表示されていることを確認します。

**注:** Juniper vSRX ゲートウェイ・デバイスで CLI モードに入ると、出力は制御プレーンの観点から `primary` として表示されます。常に出力 `show chassis cluster status` を調べて、どのゲートウェイ・デバイスがデータ・プレーンの観点から 1 次であるかを判別します。冗長グループや、制御プレーンとデータ・プレーンについて詳しくは、[vSRX のデフォルト構成](vsrx-default-config.html)を参照してください。
