---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 新規インターフェース、ゾーン、およびアドレス帳サブネットの作成
まず、VLAN のインターフェース・ユニットを作成し、サブネットのゲートウェイ・アドレスを追加する必要があります。その後、新規ユニットに関連付けられたセキュリティー・ゾーンと、そのサブネットの `address-book` エントリーを作成できます。  

**注:** 右側にスクロールすると、コマンド全体を表示できます。

```
set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29
```
