---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: create, creating, traffic, flows, ssh

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# 새 트래픽 플로우 작성
{: #creating-your-new-traffic-flows}

이제 새 구역(`CUSTOMER-PUBLIC`)을 작성함에 따라 네트워크 트래픽 플로우를 제어하도록 정책을 구성해야 합니다. 아래 구성된 첫 번째 플로우는 `CUSTOMER-PUBLIC` 구역 내의 모든 트래픽을 허용합니다. 두 번째 플로우는 `CUSTOMER-PUBLIC`과 공용 인터넷 간의 모든 트래픽을 허용하고, 세 번째 플로우는 공용 인터넷과 `CUSTOMER-PUBLIC` 간의 SSH 및 PING 트래픽을 허용하고 나머지는 삭제합니다(기본 조치는 `drop`임).

전체 명령을 보려면 오른쪽으로 스크롤하십시오!   
{: important}

```
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL description "Allow all traffic within CUSTOMER_PUBLIC zone"
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL match source-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL match destination-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL match application any
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL then permit

set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND description "Allow all outbound traffic from CUSTOMER-PUBLIC to the internet"
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND match source-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND match destination-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND match application any
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND then permit

set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH description "Allow ping and SSH from the internet to the public subnet"
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match source-address any
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match destination-address VSI_PUB_NET
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match application junos-ssh
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match application junos-ping
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH then permit
```  
