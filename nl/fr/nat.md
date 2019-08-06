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

# Utilisation de sNAT
{: #working-with-snat}

Cette rubrique offre un exemple de configuration pour sNAT sur un dispositif vSRX. Dans cette configuration, un noeud privé acheminé derrière la passerelle peut communiquer avec le monde extérieur.

<img src="images/Sample-Topology-SNAT.png" alt="drawing" style="width: 500px;"/>

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

Pour configurer la conversion d'adresses réseau (NAT) pour {{site.data.keyword.vsrx_full}}, voir ce [guide de configuration ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-nat.pdf){: new_window} sur le site Web Juniper.
