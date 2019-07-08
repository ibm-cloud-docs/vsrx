---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords:

subcollection: vsrx, ssh, allowing, pinging, subnet, public

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# SSH の許可およびパブリック・サブネットへの ping
{: #allowing-ssh-and-pinging-to-a-public-subnet}

このガイドでは、新しいインターフェース、ゾーン、およびアドレス帳を持つ IBM® Cloud Juniper vSRX Standard を構成する方法を学ぶことができます。 すべてのトラフィックのデフォルトのアクションはドロップなので、このガイドでは新しいゾーン内のすべてのトラフィックと新しいゾーンからイントラネットへのすべてのトラフィックを許可し、インターネットから新しい VLAN の 1 つのサブネットへの SSH および ping のみを許可するトラフィック・フローをセットアップする方法について説明します。

この例では、次の値を使用しています。

```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

このステップバイステップ・ガイドでは、単一のパブリック VLAN とサブネットを持つ vSRX の高可用性デプロイメントが想定されています。
{: note}

## このガイドで達成できること
{: #what-you-ll-accomplish}

このステップバイステップ・ガイドでは、サービスを構成する方法を学ぶことができます。

タスク  | 説明
------------- | -------------
[新しいインターフェース、ゾーン、およびアドレス帳サブネットの作成](/docs/infrastructure/vsrx?topic=vsrx-creating-the-new-interface-zone-and-address-book-subnet) | 新規 VLAN のタグ付きインターフェース・ユニットおよびセキュリティー・ゾーンを作成します。
[新しいトラフィック・フローの作成](/docs/infrastructure/vsrx?topic=vsrx-creating-your-new-traffic-flows) | インバウンド ping および SSH を許可する新しいトラフィック・フローを作成します。
[出力の確認と、変更のコミット](/docs/infrastructure/vsrx?topic=vsrx-confirming-the-output-and-commiting-the-changes) | 出力をチェックして、アクティブ構成にコミットされる内容を確認します。
