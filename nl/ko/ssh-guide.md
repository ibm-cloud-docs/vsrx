---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords:

subcollection: vsrx, ssh, allowing, pinging, subnet, public

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

# SSH 및 Ping을 공인 서브넷으로 허용
{: #allowing-ssh-and-pinging-to-a-public-subnet}

이 안내서에서 새 인터페이스, 구역 및 주소록을 사용하여 {{site.data.keyword.vsrx_full}} Standard를 구성하는 방법에 대해 알아봅니다. 모든 트래픽에 대한 기본 조치가 삭제됨에 따라 이 안내서는 새 구역 내의 모든 트래픽, 새 구역과 이더넷 간의 모든 트래픽을 허용하고 새 VLAN에서 이더넷과 하나의 서브넷 간의 SSH 및 Ping만 허용하는 트래픽 플로우를 설정하는 방법을 보여줍니다.

이 예제에서 다음 값이 사용됩니다.

```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

이 단계별 안내서에서는 단일 공용 VLAN 및 서브넷을 가진 vSRX의 고가용성 배치를 가정합니다.
{: note}

## 다음에 수행할 항목
{: #what-you-ll-accomplish}

이 단계별 안내서에서는 서비스 구성 방법에 대한 정보를 제공합니다.

태스크  |설명
------------- | -------------
[새 인터페이스, 구역 및 주소록 서브넷 작성](/docs/infrastructure/vsrx?topic=vsrx-creating-the-new-interface-zone-and-address-book-subnet) | 새 VLAN에 대해 태그로 지정된 인터페이스 장치 및 보안 구역을 작성합니다.
[새 트래픽 플로우 작성](/docs/infrastructure/vsrx?topic=vsrx-creating-your-new-traffic-flows) | 인바운드 Ping 및 SSH를 허용하도록 새 트래픽 플로우를 작성합니다.
[출력 확인 및 변경사항 커미트](/docs/infrastructure/vsrx?topic=vsrx-confirming-the-output-and-commiting-the-changes) | 활성 구성에 커미트될 항목을 확인하기 위해 출력을 확인합니다.
