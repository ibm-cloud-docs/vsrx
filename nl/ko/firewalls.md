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

# 방화벽 관련 작업
IBM® Cloud Juniper vSRX는 보안 구역의 개념을 사용합니다. 여기서, 각 vSRX 인터페이스는 Stateful 펌웨어를 처리하기 위해 "구역"으로 맵핑됩니다. Stateless 방화벽은 방화벽 필터로 제어됩니다. 

정책은 이 정의된 구역 간의 트래픽을 허용하고 차단하는 데 사용되며, 여기에 정의된 규칙은 Stateful입니다. 

IBM Cloud에서 vSRX는 다음 네 가지 보안 구역을 갖추도록 설계되었습니다. 

| 구역                     | 독립형 인터페이스    | HA 인터페이스|
| :---                     |        :----:        |         ---: |
| SL-Private(태그로 지정됨 )  | ge-0/0/0.0           | reth0.0      |
| SL-Public(태그로 지정되지 않음) | ge-0/0/1.0           | reth1.0      |
| Customer-Private(태그로 지정됨) | ge-0/0/0.1           | reth2.1      |
| Customer-Public(태그로 지정되지 않음) | ge-0/0/1.1           | reth3.1      |

## 구역 정책
Stateful 방화벽을 구성하려면 다음 프로시저를 수행하십시오.

1. 보안 구역을 작성하고 각 인터페이스를 지정하십시오.

	독립형 시나리오:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces ge-0/0/1.1
	```
	고가용성 시나리오:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces reth2.1
	```
2. 두 개의 다른 구역 간에 정책 및 규칙을 정의하십시오.

	다음 예제에서는 `Customer-Private` 구역에서 `Customer-Public`까지의 Ping 트래픽에 대해 설명합니다.

	```
	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP match source-address any destination-address any application junos-icmp

	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP then permit
	```

정책에 정의될 수 있는 속성 중 일부는 다음과 같습니다.

* 소스 주소
* 대상 주소
* 애플리케이션
* 조치(허용/거부/거절/계수/로그)

이는 Stateful 오퍼레이션이므로 리턴 패킷을 허용할 필요가 없습니다(해당 경우, 에코에서 응답됨). 

vSRX로 이동되는 트래픽을 허용하려면 다음 명령을 사용하십시오.

독립형의 경우:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.0 host-inbound-traffic system-services all
```
HA의 경우:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.0 host-inbound-traffic system-services all
```

OSPF 또는 BGP와 같은 프로토콜을 허용하려면 다음 명령을 사용하십시오.

독립형의 경우:
```
set security zones security-zone trust interfaces ge-0/0/0.0 host-inbound-traffic protocols all
```
HA의 경우:
```
set security zones security-zone trust interfaces reth2.0 host-inbound-traffic protocols all
```

## 방화벽 필터
기본적으로 IBM Cloud Juniper vSRX는 Ping, SSH 및 HTTPS를 자체로 허용하고 `PROTECT-IN` 필터를 `lo` 인터페이스에 적용하여 기타 모든 트래픽을 삭제합니다.

새 Stateless 방화벽을 구성하려면 다음 프로시저를 수행하십시오.

1. 방화벽 필터 및 기간을 작성하십시오(다음 필터는 ICMP만 허용하고 기타 모든 트래픽을 삭제함).
	```
	set firewall filter ALLOW-PING term ICMP from protocol icmp
	set firewall filter ALLOW-PING term ICMP then accept
	```

2. 필터 규칙을 인터페이스에 적용하십시오(다음 명령으로 필터가 모든 사설 네트워크 트래픽에 적용됨).
	```
	set interfaces ge-0/0/0 unit 0 family inet filter input ALLOW-PING
	```
