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

# IBM Cloud Juniper vSRX 정보 
{: #about-ibm-cloud-juniper-vsrx}

 BM® Cloud Juniper vSRX를 사용하면 JunOS 소프트웨어 기능(예: 전체 라우팅 스택, QoS 및 트래픽 공유, 정책 기반 라우팅 및 VPN)으로 작동되는 전체 기능 엔터프라이즈 레벨 방화벽을 통해 공용 및 사설 네트워크 트래픽을 선택적으로 라우트할 수 있습니다. vSRX는 베어메탈 서버의 단순성을 사용하여 성능, 구성 용이성 및 유지보수 이점을 제공합니다. 하드웨어는 다중 VLAN을 위한 라우팅/보안 로드를 처리하도록 크기가 조정되며 중복 네트워크 링크 및 중복 RAID 배열로 정렬될 수 있습니다. 모든 vSRX 기능은 고객이 관리합니다.

IBM Cloud vSRX는 독립형 또는 고가용성(HA) 클러스터의 두 가지 모드로 제공됩니다.

**참고:** IBM Cloud Juniper vSRX를 위한 추가 문서는 [보충 문서](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation) 주제에서 찾을 수 있습니다.

## 방화벽
vSRX는 개인용 및 공용 연결 트래픽을 모두 필터링하여 외부 및 내부 위협으로부터 사용자 환경을 보호하도록 배치됩니다. 고객은 인바운드 또는 아웃바운드 네트워크 트래픽을 허용하거나 거부하도록(기타 조치 중에) 정책 및 규칙을 정의하여 vSRX를 자체적으로 관리할 수 있으며 이를 통해 내부 및 외부 사용자로부터 애플리케이션이 보호됩니다. IPv4 및 IPv6 스택은 모두 Stateful 방식으로 지원됩니다.

## 가상 사설망(VPN) 게이트웨이
네트워크 게이트웨이 디바이스로 vSRX를 프로비저닝하여 VPN 터널링 사용을 통해 온사이트 데이터 센터 또는 사무실을 IBM Cloud에 연결하십시오. 엔터프라이즈 데이터 센터 또는 사무실과 IBM Cloud 네트워크 간의 보안 통신을 위해 IPsec 사이트 대 사이트 VPN 터널을 사용할 수 있습니다. 원격 액세스 IPSEC VPN도 지원됩니다.

VPN에 대한 자세한 구성 안내서는 [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn) 주제에서 제공된 링크를 참조하십시오.

## 네트워크 주소 변환(NAT)
서버에서 소스 NAT를 사용하여 계속해서 인터넷에 액세스할 수 있는 동안 vSRX Gateway Appliance를 통해 공용 네트워크 인터페이스 없이 애플리케이션 및 데이터베이스 서버를 프로비저닝할 수 있습니다. 강화된 보안을 위해 대상 NAT를 사용하여 서버를 게이트웨이 디바이스 뒤로 숨길 수도 있습니다.

## 엔터프라이즈 단계 라우팅
다른 격리된 네트워크에 있는 다계층 애플리케이션의 경우 vSRX를 통해 더욱 향상된 유연성으로 네트워크 간의 연결을 빌드할 수 있습니다. BGP를 사용하여 동적 라우팅을 설정할 수 있으며 이를 통해 고유한 공인 IP 주소를 IBM Cloud 라우터에 알릴 수 있습니다. BGP는 터널과 직접 링크 솔루션을 함께 사용하여 사용자 정의 사설 네트워크 구성에 더욱 향상된 유연성도 제공합니다.

## VLAN 및 Gateway Appliance의 역할에 대한 개념
VLAN(가상 LAN)은 실제 네트워크를 다수의 가상 세그먼트로 분리하는 메커니즘입니다. 편의상 여러 번 선택된 VLAN의 트래픽은 보통 "트렁킹"이라고 하는 프로세스인 단일 네트워크 케이블을 통해 제공될 수 있습니다.

vSRX는 vSRX 서버 및 Gateway Appliance 설비의 두 가지 인터페이스로 관리됩니다. Gateway Appliance는 vSRX와 연관시킬 VLAN을 선택하기 위해 인터페이스(GUI 및 API)를 제공합니다. Gateway Appliance와의 VLAN 연관으로 해당 VLAN 및 vSRX의 모든 서브넷이 다시 라우트되어 필터링, 전달 및 보호를 제어할 수 있습니다. 연관된 VLAN의 서버는 vSRX를 통해 다른 VLAN에서만 연결될 수 있습니다. VLAN을 무시하거나 분리하지 않으면 vSRX를 통과할 수 없습니다.

기본적으로 새 Gateway Appliance는 두 가지 고정 "전송" VLAN(_public_ 및 _private_ 네트워크 하나씩)과 연관됩니다. 일반적으로 이 네트워크는 관리를 위해 사용되고 vSRX 명령으로 각각 보안 설정될 수 있습니다.

vSRX는 Gateway Appliance를 통해 연관되는 VLAN만 관리할 수 있습니다.

**Gateway Appliance 세부사항** 화면에서 VLAN을 관리하는 방법에 대한 정보는 [VLAN 관리](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans) 주제를 참조하십시오.
