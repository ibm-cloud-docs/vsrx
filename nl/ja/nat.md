---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: nat, working, gateways, nodes

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

# sNAT の操作
{: #working-with-snat}

このトピックには、vSRX アプライアンス上での sNAT のサンプル構成が記載されています。 この構成を使用すると、ゲートウェイの背後に経路指定されたプライベート・ノードが外界と通信できます。

<img src="images/Sample-Topology-SNAT.png" alt="図面" style="width: 500px;"/>

```
from-zone CUSTOMER-PRIVATE to-zone SL-PUBLIC {
   policy SNAT {
       match {
           source-address any;
           destination-address any;
           application any;
       }
       then {
           permit;
       }
   }
}

nat {
   source {
       rule-set rs1 {
           from zone CUSTOMER-PRIVATE;
           to zone SL-PUBLIC;
           rule r1 {
               match {
                   source-address 0.0.0.0/0;
                   destination-address 0.0.0.0/0;
               }
               then {
                   source-nat {
                       interface;
                   }
               }
           }
       }
   }
}
```

{{site.data.keyword.vsrx_full}} 用に NAT を構成するには、Juniper Web サイト上のこの[構成ガイド![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-nat.pdf){: new_window}を参照してください。
