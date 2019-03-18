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

# Mit sNAT arbeiten
{: #working-with-snat}

In diesem Abschnitt wird eine Beispielkonfiguration für sNAT auf einer vSRX-Appliance bereitgestellt. Mit dieser Konfiguration kann ein privater Knoten, dessen Weiterleitung hinter dem Gateway erfolgt, mit der Außenwelt kommunizieren.

<img src="images/Sample-Topology-SNAT.png" alt="Zeichnung" style="width: 500px;"/>

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

Ziehen Sie bei der Konfiguration von NAT für die Komponente Juniper vSRX für IBM® Cloud dieses [Konfigurationshandbuch ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-nat.pdf){: new_window} zurate, das Sie auf der Juniper-Website finden.
