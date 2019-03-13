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

# NAT 관련 작업
이 주제에서는 vSRX 어플라이언스의 sNAT를 위한 샘플 구성을 제공합니다. 이 구성을 통해 게이트웨이 뒤에 라우트된 사설 노드는 외부와 통신할 수 있습니다. 

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

IBM® Cloud Juniper vSRX를 위한 NAT를 구성하려면 Juniper 웹 사이트에서 이 [구성 안내서](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-nat.pdf)를 참조하십시오. 
