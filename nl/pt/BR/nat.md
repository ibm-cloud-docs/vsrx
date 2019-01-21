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

# Trabalhando com a NAT
Este tópico fornece uma configuração de amostra para a sNAT em um dispositivo vSRX. Com essa configuração, um nó privado roteado por trás do gateway pode se comunicar com o mundo externo.

<img src="images/Sample-Topology-SNAT.png" alt="drawing" style="width: 500px;"/>

```
from-zone CUSTOMER-PRIVATE to-zone SL-PUBLIC {
   policy SNAT {
       match {
           source-address any; destination-address any; application any; } then {
           permit; }
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

Para configurar a NAT para o IBM® Cloud Juniper vSRX, consulte esse [guia de configuração](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-nat.pdf) no website do Juniper.
