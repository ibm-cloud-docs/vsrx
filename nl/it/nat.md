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

# Utilizzo di sNAT
{: #working-with-snat}

Questo argomento fornisce una configurazione di esempio per sNAT su un'applicazione vSRX. Con questa configurazione, un nodo privato instradato dietro il gateway può comunicare con il mondo esterno.

<img src="images/Sample-Topology-SNAT.png" alt="disegno" style="width: 500px;"/>

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

Per configurare NAT per IBM® Cloud Juniper vSRX, fai riferimento a questa [guida di configurazione ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-nat.pdf){: new_window} sul sito web Juniper.
