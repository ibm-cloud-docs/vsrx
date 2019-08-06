---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: manage, managing, vlan, gateway, route, bypass, disassociate, associate, configuration, disassociating, associating, standalone, ha

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

# IBM VLAN の管理
{: #managing-ibm-vlans}

[「ゲートウェイ・アプライアンスの詳細 (Gateway Appliance Details)」画面 ](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)からさまざまなアクションを実行できます。

## ゲートウェイ・アプライアンスへの VLAN の関連付け
{: #associate-a-vlan-to-a-gateway-appliance}

VLAN を経路指定するには、その前にゲートウェイ・アプライアンスに VLAN を関連付ける必要があります。 VLAN の関連付けとは、VLAN をゲートウェイ・アプライアンスに経路指定できるように、適格な VLAN をネットワーク・ゲートウェイにリンクすることです。 この関連付けにより、VLAN がゲートウェイ・アプライアンスに自動的に経路指定されるわけではありません。経路指定されるまで、VLAN はフロントエンドとバックエンドのお客様のルーターを使用し続けます。

VLAN は、一度に 1 つのゲートウェイにのみ関連付けられ、ファイアウォールを持つことはできません。 以下の手順に従って VLAN をネットワーク・ゲートウェイに関連付けます。

1. カスタマー・ポータルの[「ゲートウェイ・アプライアンスの詳細 (Gateway Appliance Details)」画面にアクセス](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)します。
2. 「VLAN」タブを選択します。
3. **「VLAN の関連付け (Associate VLAN)」**をクリックし、ドロップダウンから VLAN を選択します。
4. **「保存」**をクリックし、選択内容を確認します。 VLAN 関連付けアクションでは、ファイアウォールを経由するようには VLAN は経路指定されません。

VLAN をゲートウェイ・アプライアンスに関連付けた後、その VLAN は「ゲートウェイ・アプライアンスの詳細 (Gateway Appliance Details)」画面の「関連付けられた VLAN」セクションに表示されます。 このセクションで、VLAN をゲートウェイに経路指定したり、ゲートウェイから関連付けを解除したりすることができます。 上記のステップを繰り返すことで、適格な VLAN をいつでもゲートウェイ・アプライアンスにさらに関連付けることができます。

## 関連付けられた VLAN の経路指定
{: #route-an-associated-vlan}

関連付けられた VLAN はゲートウェイ・アプライアンスにリンクされますが、 VLAN が経路指定されるまで、VLAN との間の両方向のトラフィックはゲートウェイに到達しません。 関連付けられた VLAN が経路指定された後、フロントエンドとバックエンドのすべてのトラフィックは、お客様のルーターではなく、ゲートウェイ・アプライアンスを通るように経路指定されます。

関連付けられた VLAN を経路指定するには、次の手順を実行します。

1. カスタマー・ポータルの[「ゲートウェイ・アプライアンスの詳細 (Gateway Appliance Details)」画面にアクセス](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)します。
2. 「VLAN」タブを選択します。
3. チェック・ボックスを切り替えることでご希望の VLAN を選択します。
4. **「通る経路」**をクリックし、選択内容を確認します。

VLAN を経路指定した後、フロントエンドとバックエンドのすべてのトラフィックは、お客様のルーターからネットワーク・ゲートウェイに移動します。 トラフィックとゲートウェイ・アプライアンス自体に関連した制御をさらに行うには、ゲートウェイの管理ツールにアクセスすることで可能です。 ネットワーク・ゲートウェイを通る経路指定は、[ゲートウェイ・アプライアンスをバイパスする](#bypass-gateway-appliance-routing-for-a-vlan)ことによっていつでも中止できます。

## VLAN のゲートウェイ・アプライアンスの経路指定のバイパス
{: #bypass-gateway-appliance-routing-for-a-vlan}

VLAN が経路指定された後、フロントエンドとバックエンドのすべてのトラフィックは、ネットワーク・ゲートウェイを通って移動します。 ゲートウェイ・アプライアンスは、トラフィックがフロントエンドとバックエンドのお客様のルーター (FCR と BCR) に戻れるように、いつでもバイパスすることができます。

VLAN をバイパスすると、VLAN をネットワーク・ゲートウェイに関連付けたままにすることができます。 VLAN をゲートウェイ・アプライアンスと関連付ける必要がなくなった場合は、[ゲートウェイ・アプライアンスからの VLAN の関連付け解除](#disassociate-a-vlan-from-a-gateway-appliance)を参照してください。

以下の手順を実行して、VLAN のゲートウェイ経路指定をバイパスします。

1. カスタマー・ポータルの[「ゲートウェイ・アプライアンスの詳細 (Gateway Appliance Details)」画面にアクセス](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)します。
2. 「VLAN」タブを選択します。
3. チェック・ボックスを切り替えることでご希望の VLAN を選択します。
4. **「回る経路」**をクリックし、選択内容を確認します。

ネットワーク・ゲートウェイをバイパスした後、フロントエンドとバックエンドのすべてのトラフィックは、VLAN に関連付けられた FCR と BCR を通過するようになります。 VLAN は、ゲートウェイ・アプライアンスに関連付けされたままになり、いつでもゲートウェイ・アプライアンスに経路を戻すことができます。

## ゲートウェイ・アプライアンスからの VLAN の関連付け解除
{: #disassociate-a-vlan-from-a-gateway-appliance}

VLAN は、[関連付け](#associate-a-vlan-to-a-gateway-appliance)を介して、一度に 1 つのゲートウェイ・アプライアンスにリンクできます。 関連付けにより、VLAN のゲートウェイ・アプライアンスへの経路指定はいつでも可能です。 VLAN を別のゲートウェイ・アプライアンスに関連付ける必要がある場合、または VLAN をそのゲートウェイに関連付ける必要がなくなった場合は、関連付けの解除が必要です。 関連付け解除により、VLAN からゲートウェイ・アプライアンスへの「リンク」が削除され、必要に応じて別のゲートウェイに関連付けることができます。

以下の手順に従って VLAN からゲートウェイ・アプライアンスへの関連付けを解除します。

1. カスタマー・ポータルの[「ゲートウェイ・アプライアンスの詳細 (Gateway Appliance Details)」画面にアクセス](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)します。
2. 「VLAN」タブを選択します。
3. チェック・ボックスを切り替えることでご希望の VLAN を選択します。
4. **「関連付け解除」**をクリックし、選択内容を確認します。

ゲートウェイ・アプライアンスから VLAN を関連付け解除した後、VLAN を別のゲートウェイに関連付けることができます。 また、いつでも、VLAN を元のゲートウェイ・アプライアンスに再び関連付けることができます。 ゲートウェイ・アプライアンスから VLAN の関連付けを解除した後、VLAN のトラフィックをゲートウェイ経由で経路指定することはできません。 VLAN を経路指定するには、その前にゲートウェイ・アプライアンスに関連付ける必要があります。

## 同じネットワーク・インターフェース上で複数の VLAN を経路指定する
{: #route-multiple-vlans-over-the-same-network-interface}

{{site.data.keyword.vsrx_full}} は、同じネットワーク・インターフェース上で複数の VLAN と運用できます。 タグなしのトラフィックとタグ付きのトラフィックの両方を同時に処理することもできます。 この処理は、スタンドアロン・デバイス上でインターフェースのカプセル化を `flexible-vlan-tagging` に設定して行うか、高可用性デバイス上でタグ付けされたインターフェースとして reth2 と reth3 を使用して行います。 これはデフォルト構成の一部として行われ、変更する必要はありません。  スタンドアロン・デバイスでは、Unit 0 はタグなしのサブインターフェースで、その他のゼロでないユニットはタグ付けされます。

追加のタグ付きインターフェースを構成するには、以下のコマンド・セットを使用します。

スタンドアロンの場合:
```
set interfaces ge-0/0/0 unit 50 vlan-id 50
set interfaces ge-0/0/0 unit 50 family inet address <IP/MASK>
```

HA の場合:
```
set interfaces reth2 unit 50 vlan-id 50
set interfaces reth2 unit 50 family inet address <IP/MASK>
```

Unit 0 は、タグなしであっても、`native-vlan` として構成されている VLAN ID を `JunOS` が参照するために必要です。この例では、`native-vlan-id` が `10` なので、Unit 0 の `vlan-id` も `10` にする必要があります。 このようにして、Unit 0 にタグを付けないことが `JunOS` に通知されます。
{: note}

## vSRX 用の VLAN 構成の例
{: #sample-vlan-configuration-for-vsrx}

以下に、vSRX 用の構成の例を示します。2 つのプライベート・インターフェースと 1 つのカスタマー・ゾーンが定義されています。
このサンプル構成では、プライベート VLAN1 とプライベート VLAN2 が相互に通信できます。 スタンドアロン vSRX インターフェースは ge-0/0/0 (プライベート) および ge-0/0/1 (パブリック) として定義され、高可用性インスタンスの場合は reth2 (HA プライベート) および reth3 (HA パブリック) として定義されます。

<img src="images/Sample-Topology-VLAN-to-VLAN.png" alt="図面" style="width: 500px;"/>

```
# show interfaces

ge-0/0/0 {
   description PRIVATE_VLANs;
   flexible-vlan-tagging;
   native-vlan-id 1121;
   unit 0 {
       vlan-id 1121;
       family inet {
           address 10.184.108.158/26;
       }
   }
   unit 10 {
       vlan-id 1811;
       family inet {
           address 10.184.237.201/29;
       }
   }
   unit 20 {
       vlan-id 1812;
       family inet {
           address 10.185.48.9/29;
       }
   }
}


# show security zones security-zone CUSTOMER-PRIVATE
interfaces {
   ge-0/0/0.10 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
   ge-0/0/0.20 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
}
# show security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PRIVATE
policy Allow_C_C {
   match {
       source-address any;
       destination-address any;
       application any;
   }
   then {
       permit;
   }
}
```
