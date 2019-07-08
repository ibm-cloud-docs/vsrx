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

# 使用 sNAT
{: #working-with-snat}

本主題提供 vSRX 應用裝置上的 sNAT 配置範例。使用此配置，「閘道」後面遞送的專用節點可以與外界通訊。

<img src="images/Sample-Topology-SNAT.png" alt="圖片" style="width: 500px;"/>

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

若要為 IBM® Cloud Juniper vSRX 配置 NAT，請參閱 Juniper 網站上的此[配置手冊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-nat.pdf){: new_window}。
