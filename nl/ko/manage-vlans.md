---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: manage, managing, vlan, gateway, route, bypass, disassociate, associate, configuration, disassociating, associating, standalone, ha

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# IBM VLAN 관리
{: #managing-ibm-vlans}

[Gateway Appliance 세부사항 화면](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)에서 다양한 조치를 수행할 수 있습니다.

## VLAN을 Gateway Appliance와 연관
{: #associate-a-vlan-to-a-gateway-appliance}

VLAN은 라우트되기 전에 Gateway Appliance와 연관되어야 합니다. VLAN 연관은 VLAN이 Gateway Appliance에 라우트될 수 있도록 적격한 VLAN을 네트워크 게이트웨이에 연결하는 것입니다. 이 연관은 VLAN을 Gateway Appliance로 자동으로 라우트하지 않습니다. VLAN은 라우트될 때까지 프론트 엔드 및 백엔드 고객 라우터를 계속해서 사용합니다.

VLAN은 한 번에 하나의 게이트웨이에만 연관될 수 있고 방화벽은 보유하지 않아야 합니다. VLAN을 네트워크 게이트웨이와 연관시키려면 다음 프로시저를 수행하십시오.

1. 고객 포털에서 [Gateway Appliance 세부사항 화면에 액세스](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)하십시오.
2. VLAN 탭을 선택하십시오.
3. **VLAN 연관**을 클릭하고 드롭 다운에서 VLAN을 선택하십시오.
4. **저장**을 클릭하고 선택사항을 확인하십시오. VLAN 연관 조치는 방화벽을 통해 VLAN을 라우트하지 않습니다.

VLAN을 Gateway Appliance와 연관시킨 후 VLAN은 Gateway Appliance 세부사항 화면의 연관된 VLAN 섹션에 표시됩니다. 이 섹션에서 VLAN은 게이트웨이로 라우트될 수 있거나 게이트웨이에서 분리될 수 있습니다. 추가적인 적격한 VLAN은 위의 단계를 반복하여 언제든지 Gateway Appliance와 연관될 수 있습니다.

## 연관된 VLAN 라우트
{: #route-an-associated-vlan}

연관된 VLAN은 Gateway Appliance에 연결되지만 VLAN 내부 및 외부의 트래픽은 VLAN이 라우트될 때까지 게이트웨이에 도달하지 않습니다. 연관된 VLAN이 라우트된 후 모든 프론트 및 백엔드 트래픽은 고객 라우터와 반대로 Gateway Appliance를 통해 라우트됩니다.

연관된 VLAN을 라우트하려면 다음 프로시저를 수행하십시오.

1. 고객 포털에서 [Gateway Appliance 세부사항 화면에 액세스](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)하십시오.
2. VLAN 탭을 선택하십시오.
3. 선택란을 전환하여 원하는 VLAN을 선택하십시오.
4. **라우트 통과**를 클릭하고 선택사항을 확인하십시오.

VLAN을 라우트한 후 모든 프론트 엔드 및 백엔드가 고객 라우터에서 네트워크 게이트웨이로 이동합니다. 트래픽과 Gateway Appliance에 자체적으로 관련되는 추가 제어는 게이트웨이의 관리 도구에 액세스하여 수행될 수 있습니다. 네트워크 게이트웨이를 통한 라우팅은 [Gateway Appliance를 무시](#bypass-gateway-appliance-routing-for-a-vlan)하여 언제든지 연결이 끊어질 수 있습니다.

## VLAN을 위한 Gateway Appliance 라우팅 무시
{: #bypass-gateway-appliance-routing-for-a-vlan}

VLAN이 라우트된 후 모든 프론트 및 백엔드 트래픽은 네트워크 게이트웨이를 통해 이동합니다. 언제든지 Gateway Appliance가 무시되어 트래픽이 프론트 및 백엔드 고객 라우터(FCR 및 BCR)로 리턴됩니다.

VLAN을 무시하면 VLAN은 네트워크 게이트웨이와 연관된 상태로 유지될 수 있습니다. VLAN이 더 이상 Gateway Appliance와 연관되지 않는 경우 [Gateway Appliance에서 VLAN 분리](#disassociate-a-vlan-from-a-gateway-appliance)를 참조하십시오.

VLAN을 위한 게이트웨이 라우팅을 무시하려면 다음 프로시저를 수행하십시오.

1. 고객 포털에서 [Gateway Appliance 세부사항 화면에 액세스](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)하십시오.
2. VLAN 탭을 선택하십시오.
3. 선택란을 전환하여 원하는 VLAN을 선택하십시오.
4. **라우트 어라운드**를 클릭하고 선택사항을 확인하십시오.

네트워크 게이트웨이를 무시한 후 모든 프론트 엔드 및 백엔드 트래픽은 VLAN과 연관된 FCR 및 BCR을 통해 라우트됩니다. VLAN은 Gateway Appliance와 연관된 상태로 유지되며 언제든지 Gateway Appliance로 다시 라우트될 수 있습니다.

## Gateway Appliance에서 VLAN 분리
{: #disassociate-a-vlan-from-a-gateway-appliance}

VLAN은 [연관](#associate-a-vlan-to-a-gateway-appliance)을 통해 언제든지 하나의 Gateway Appliance에 연결될 수 있습니다. 연관은 VLAN이 언제든지 Gateway Appliance에 라우트될 수 있도록 합니다. VLAN이 다른 Gateway Appliance와 연관되어야 하거나 VLAN이 더 이상 게이트웨이와 연관되지 않아야 하는 경우 분리는 필수입니다. 해당 경우 분리는 VLAN과 Gateway Appliance 간의 "연결"을 제거하여 VLAN이 다른 게이트웨이와 연관될 수 있습니다.

Gateway Appliance에서 VLAN을 분리하려면 다음 프로시저를 수행하십시오.

1. 고객 포털에서 [Gateway Appliance 세부사항 화면에 액세스](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)하십시오.
2. VLAN 탭을 선택하십시오.
3. 선택란을 전환하여 원하는 VLAN을 선택하십시오.
4. **연관**을 클릭하고 선택사항을 확인하십시오.

Gateway Appliance에서 VLAN을 분리한 후 VLAN은 다른 게이트웨이와 연관될 수 있습니다. VLAN은 언제든지 Gateway Appliance로 다시 연관될 수 있습니다. Gateway Appliance에서 VLAN을 분리한 후 VLAN의 트래픽은 게이트웨이를 통해 라우트될 수 없습니다. VLAN은 라우트되기 전에 Gateway Appliance와 연관되어야 합니다.

## 동일한 네트워크 인터페이스를 통한 다중 VLAN 라우트
{: #route-multiple-vlans-over-the-same-network-interface}

{{site.data.keyword.vsrx_full}}는 동일한 네트워크 인터페이스를 통해 다중 VLAN으로 작동될 수 있습니다. 동시에 태그로 지정되지 않고 태그로 지정된 트래픽을 처리할 수도 있습니다. 이는 인터페이스 캡슐화를 `flexible-vlan-tagging`으로 설정하여 독립형 디바이스에서 수행되거나 태그로 지정된 인터페이스로 reth2 및 reth3을 사용하여 고가용성 디바이스에서 수행됩니다. 기본 구성의 일부로 수행되며 수정될 필요는 없습니다.  독립형 디바이스에서 장치 0은 태그로 지정되지 않은 하위 인터페이스입니다. 그렇지 않으면 0이 아닌 장치가 태그로 지정됩니다.

태그로 지정된 추가 인터페이스를 구성하려면 다음 명령 세트를 사용하십시오.

독립형의 경우:
```
set interfaces ge-0/0/0 unit 50 vlan-id 50
set interfaces ge-0/0/0 unit 50 family inet address <IP/MASK>
```

HA의 경우:
```
set interfaces reth2 unit 50 vlan-id 50
set interfaces reth2 unit 50 family inet address <IP/MASK>
```

장치 0에 태그가 지정되지 않은 경우에도 `native-vlan`으로 구성된 VLAN ID를 참조하기 위해 `JunOS`에 장치 0이 필요합니다. 이 예제에서 `native-vlan-id`가 `10`이므로 장치 0에는 `10`의 `vlan-id`도 있어야 합니다. 이렇게 하면 `JunOS`는 장치 0이 태그로 지정되지 않도록 알림을 받습니다.
{: note}

## vSRX를 위한 샘플 VLAN 구성
{: #sample-vlan-configuration-for-vsrx}

다음은 두 개의 사설 인터페이스 및 하나의 고객 구역을 정의하는 vSRX를 위한 샘플 구성입니다.
이 샘플 구성을 통해 사설 VLAN1과 사설 VLAN2는 서로 통신할 수 있습니다. 독립형 vSRX 인터페이스는 ge-0/0/0(사설) 및 ge-0/0/1(공용)으로 정의되고 고가용성 인스턴스는 reth2(HA 사설) 및 reth3(HA 공용)으로 정의됩니다.

<img src="images/Sample-Topology-VLAN-to-VLAN.png" alt="그림" style="width: 500px;"/>

```
# show interfaces

ge-0/0/0 {
   description PRIVATE_VLANs;
   flexible-vlan-tagging;
   native-vlan-id 1121;
   unit 0 {
       vlan-id 1121;
       family inet {
           address 10.184.108.158/26;
       }
   }
   unit 10 {
       vlan-id 1811;
       family inet {
           address 10.184.237.201/29;
       }
   }
   unit 20 {
       vlan-id 1812;
       family inet {
           address 10.185.48.9/29;
       }
   }
}


# show security zones security-zone CUSTOMER-PRIVATE
interfaces {
   ge-0/0/0.10 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
   ge-0/0/0.20 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
}
# show security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PRIVATE
policy Allow_C_C {
   match {
       source-address any;
       destination-address any;
       application any;
   }
   then {
       permit;
   }
}
```
