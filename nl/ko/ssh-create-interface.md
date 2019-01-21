---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 새 인터페이스, 구역 및 주소록 서브넷 작성
먼저 VLAN을 위한 인터페이스 장치를 작성하고 서브넷의 게이트웨이 주소를 추가해야 합니다. 그런 다음 새 장치와 연관된 보안 구역 및 서브넷의 `address-book` 항목을 작성할 수 있습니다.   

**참고:** 전체 명령을 보려면 오른쪽으로 스크롤하십시오!

```
set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29
```
