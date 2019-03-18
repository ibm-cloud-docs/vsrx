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

# 라우팅 관련 작업
{: #working-with-routing}

IBM® Cloud Juniper vSRX는 `JunOS`를 기반으로 하며 전체 Juniper 라우팅 스택에 대한 액세스 권한을 제공합니다.

##정적 라우팅
정적 라우트를 구성하려면 다음 명령을 실행하십시오.

###기본 라우트 설정
```
set routing-options static route 0/0 next-hop <Gateway IP>
```

### 정적 라우트 작성
```
set routing-options static route <PREFIX/MASK> next-hop <Gateway IP>
```  

###기본 OSPF 라우팅
영역 0만 사용하여 기본 OSPF 라우팅을 설정하려면 md5 인증 사용을 통해 다음 명령을 실행하십시오.

```
set protocols ospf area 0 interface ge-0/0/1.0 authentication md5 0 key <KEY>
```

### 기본 BGP 라우팅
기본 BGP 라우팅을 설정하려면 먼저 로컬 AS를 정의하십시오.

```
set routing-options autonomous-system 65001
```

그런 다음 BGP 인접 항목 및 세션 속성을 구성하십시오.

```
set protocols bgp group CUSTOMER local-address 1.1.1.1
set protocols bgp group CUSTOMER family inet unicast
set protocols bgp group CUSTOMER family inet6 unicast
set protocols bgp group CUSTOMER peer-as 65002
set protocols bgp group CUSTOMER neighbor 2.2.2.2
```

이 예제에서 BGP는 다음을 위해 구성됩니다.

* 세션을 설정하기 위해 `1.1.1.1`의 소스 IP 주소를 사용합니다.
* ipv4 및 ipv6 unicast 패밀리를 모두 조정합니다.
* `AS 65002`에 속하는 인접 항목과 피어합니다.
* 인접 항목 IP `2.2.2.2`를 피어합니다.

추가 구성은 [Juniper 웹 사이트 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.juniper.net/documentation/en_US/junos11.4/information-products/topic-collections/config-guide-routing/config-guide-routing.pdf){: new_window}을 참조하십시오.
