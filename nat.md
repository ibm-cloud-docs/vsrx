---

copyright:
  years: 2018
lastupdated: "2019-11-14"

keywords: nat, working, gateways, nodes

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Working with sNAT
{: #working-with-snat}
{: help}
{: support}

This topic provides a sample configuration for sNAT on a vSRX appliance. With this configuration, a private node routed behind the Gateway can communicate with the outside world.
{: shortdesc}

![Sample topology](images/Sample-Topology-SNAT.png "Sample topology"){: caption="Sample topology" caption-side="bottom"}


```sh
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

To configure NAT for the {{site.data.keyword.vsrx_full}}, refer to this [configuration guide](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-nat.pdf){: external} on the Juniper website.
