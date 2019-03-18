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

# Trabajar con sNAT
{: #working-with-snat}

En este tema se proporciona una configuración de ejemplo para sNAT en un dispositivo vSRX. Con esta configuración, un nodo privado direccionado detrás de la pasarela se puede comunicar con el mundo exterior.

<img src="images/Sample-Topology-SNAT.png" alt="dibujo" style="width: 500px;"/>

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

Para configurar NAT para IBM® Cloud Juniper vSRX, consulte esta [guía de configuración ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-nat.pdf){: new_window} en el sitio web de Juniper.
