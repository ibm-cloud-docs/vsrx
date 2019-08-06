---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords:

subcollection: vsrx, firewalls, working, policy, policies, rules, zones, standalone, ha

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# ファイアウォールの処理
{: #working-with-firewalls}

{{site.data.keyword.vsrx_full}} では、セキュリティー・ゾーンの概念を使用しています。この概念では、各 vSRX インターフェースが「ゾーン」にマップされて、ステートフル・ファイアウォールが処理されます。 ステートレス・ファイアウォールは、ファイアウォール・フィルターによって制御されます。

ポリシーは、これらの定義済みゾーン間のトラフィックを許可およびブロックするために使用され、ここで定義されるルールはステートフルです。

IBM Cloud では、vSRX が 4 つの異なるセキュリティー・ゾーンを持つように設計されています。

| ゾーン                     | スタンドアロン・インターフェース | HA インターフェース |
| :---                     |        :----:        |         ---: |
| SL-Private (タグなし)　    | ge-0/0/0.0 or ae0.0  | reth0.0　　　      |
| SL-Public (タグなし)　     | ge-0/0/1.0 or ae1.0  | reth1.0　　　      |
| Customer-Private (タグ付き)| ge-0/0/0.1 or ae0.1  | reth2.1      　　　      |
| Customer-Public (タグ付き) | ge-0/0/1.1 or ae1.1  | reth3.1      　　　      |

## ゾーンのポリシー
{: #zone-policies}

ステートフル・ファイアウォールを構成するには、以下の手順を実行します。

1. セキュリティー・ゾーンを作成し、それぞれインターフェースを割り当てます。

	スタンドアロンのシナリオ:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces ge-0/0/1.1
	```
	高可用性のシナリオ:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces reth2.1
	```
2. 2 種類のゾーン間のポリシーとルールを定義します。

	以下の例は、ゾーン `Customer-Private` から `Customer-Public` へのトラフィックの ping を図示しています。

	```
	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP match source-address any destination-address any application junos-icmp

	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP then permit
	```

ポリシー内で定義できる属性の一部を以下に示します。

* 送信側アドレス
* 受信側アドレス
* アプリケーション
* アクション (permit/deny/reject/count/log)

これはステートフル操作なので、戻りパケット (この場合はエコー応答) を許可する必要はありません。

以下のコマンドを使用して、vSRX に向けられるトラフィックを許可します。

スタンドアロンの場合:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.0 host-inbound-traffic system-services all
```
HA の場合:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.0 host-inbound-traffic system-services all
```

OSPF や BGP などのプロトコルを許可するには、以下のコマンドを使用します。

スタンドアロンの場合:
```
set security zones security-zone trust interfaces ge-0/0/0.0 host-inbound-traffic protocols all
```
HA の場合:
```
set security zones security-zone trust interfaces reth2.0 host-inbound-traffic protocols all
```

## ファイアウォール・フィルター
{: #firewall-filters}

デフォルトでは、{{site.data.keyword.vsrx_full}} は `lo` インターフェースに `PROTECT-IN` フィルターを適用して、{{site.data.keyword.vsrx_full}} 自体に対する ping、SSH、HTTPS を許可し、その他のトラフィックをすべて除去します。

新しいステートレス・ファイアウォールを構成するには、以下の手順を実行します。

1. ファイアウォール・フィルターと条件を作成します (以下のフィルターでは ICMP のみが許可され、その他のトラフィックはすべて除去されます)。
	```
	set firewall filter ALLOW-PING term ICMP from protocol icmp
	set firewall filter ALLOW-PING term ICMP then accept
	```

2. フィルター・ルールをインターフェースに適用します (以下のコマンドでは、すべてのプライベート・ネットワーク・トラフィックにフィルターを適用します)。
	```
	set interfaces ge-0/0/0 unit 0 family inet filter input ALLOW-PING
	```
