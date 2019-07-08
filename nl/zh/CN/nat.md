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

本主题提供了 vSRX 设备上 sNAT 的样本配置。通过此配置，在网关后面路由的专用节点可以与外部世界进行通信。

<img src="images/Sample-Topology-SNAT.png" alt="图样" style="width: 500px;"/>

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

要为 IBM® Cloud Juniper vSRX 配置 NAT，请参阅 Juniper Web 站点上的此[配置指南 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-nat.pdf){: new_window}。
