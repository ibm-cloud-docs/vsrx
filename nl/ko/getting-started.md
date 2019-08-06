---

copyright:
  years: 2018
lastupdated: "2019-05-03"

keywords: vsrx, ordering, gateway, appliance

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

# {{site.data.keyword.vsrx_full}} Gateway 시작하기
{: #getting-started}

{{site.data.keyword.vsrx_full}} Gateway를 시작하려면 먼저 사용자의 계정이 IBM Cloud에 연결되어 있는지 여부를 판별하십시오.

연결된 계정이 있는지 여부를 판별하려면 브라우저에서 [고객 포털 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){: new_window}로 이동하여 로그인하십시오. 계정이 연결되어 있으면 오른쪽 상단에 **Bluemix에 대해 자세히 알아보기!** 단추가 표시되지 않습니다. 

## 주문 단계
{: #steps-for-ordering}

다음 방법 중 하나를 사용하여 Gateway Appliance를 주문할 수 있습니다.

{{site.data.keyword.vsrx_full}} Gateway의 알려진 제한사항의 목록은 [알려진 제한사항 주제](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx)를 참조하십시오.
{: note}

### 연결된 계정으로 주문
{: #ordering-with-a-linked-account}

계정이 연결되어 있으면 다음 프로시저를 따르십시오.

1. 브라우저의 [IBM Cloud 카탈로그![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/gen1/infrastructure/provision/gateway){: new_window}에서 게이트웨이 어플라이언스 페이지를 열고 계정에 로그인하십시오. 

  [IBM Cloud UI 콘솔![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com)에 로그인한 후 **클래식 인프라 > 네트워크 > 게이트웨이 어플라이언스**를 선택하여 이 페이지로 이동할 수도 있습니다.
또는 [IBM Cloud 카탈로그![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://cloud.ibm.com/catalog)에서 **네트워크** 카테고리를 선택한 후 **게이트웨이 어플라이언스** 타일을 선택하십시오. 

2. **게이트웨이 공급업체** 아래에서 **Juniper vSRX(최대 1Gbps)** 또는 **Juniper vSRX(최대 10 Gbps)**를 선택하십시오. 

3. **게이트웨이 어플라이언스** 섹션에서 **호스트 이름** 및 **도메인** 이름 정보를 입력하십시오. 이 필드는 이미 기본 정보로 채워져 있으므로 값이 올바른지 확인하십시오. 

	<img src="images/linked_order.png" alt="그림" style="width: 700px;"/>

4. 원하는 경우 **고가용성** 옵션을 선택한 후 원하는 데이터 센터 **위치**와 드롭 다운 메뉴에서 원하는 특정 **팟(Pod)**을 선택하십시오. 

  이미 연관된 VLAN이 있는 팟(Pod)만 여기에 표시됩니다. 나열되지 않은 팟(Pod)에 게이트웨이 어플라이언스를 프로비저닝하려면 먼저 VLAN을 작성하십시오.
  {: note}

	<img src="images/linked_server.png" alt="그림" style="width: 600px;"/>

4. **구성** 섹션에서 RAM 및 SSH 키(새 게이트웨이에 대한 액세스를 인증하기 위해 사용하려는 경우)를 선택하여 프로세서를 선택하십시오. 

  2단계에서 선택한 라이센스 버전을 기반으로 적절한 프로세서가 선택됩니다. 하지만 다른 RAM 구성을 선택할 수 있습니다.
  {: note}

5. **스토리지 디스크** 섹션에서 스토리지 요구사항을 충족하는 옵션을 선택하십시오. 

  RAID0 및 RAID1 옵션은 핫 스패어(기본 컴포넌트가 실패하는 즉시 서비스에 배치될 수 있는 백업 컴포넌트)로서 데이터 손실에 대해 추가적으로 보호하기 위해 사용할 수 있습니다.
  {: note}

  vSRX당 최대 4개의 디스크가 있을 수 있습니다. RAID 구성은 미러링되기 때문에 RAID 구성을 사용하는 "디스크 크기"가 사용 가능한 디스크 크기입니다.
  {: note}

  상세 로그를 생성하는 네트워크 진단을 실행할 계획인 경우 기본 디스크 설정보다 큰 크기를 확보해 두십시오.
  {: tip}

6. **네트워크 인터페이스** 섹션에서 **업링크 포트 속도**를 선택하십시오. 기본 선택사항은 단일 인터페이스이지만 중복 및 사설 전용 옵션도 있습니다. 요구사항에 가장 적합한 항목을 선택하십시오. 

  네트워크 인터페이스 **추가 기능** 섹션에서는 필요한 경우 IPv6 주소를 선택할 수 있으며 추가적으로 포함된 기본 옵션을 표시합니다. 

8. 선택사항을 검토하고 서드파티 서비스 계약을 읽었는지 확인한 후 **작성**을 클릭하십시오. 주문은 자동으로 확인됩니다. 

주문이 승인되면 {{site.data.keyword.vsrx_full}} 게이트웨이 프로비저닝이 자동으로 시작됩니다. 프로비저닝 프로세스가 완료되면 새 vSRX가 게이트웨이 어플라이언스 목록 페이지에 표시됩니다. 게이트웨이 이름을 클릭하여 게이트웨이 세부사항 페이지를 여십시오. 디바이스의 IP 주소, 로그인 사용자 이름 및 비밀번호가 표시됩니다.   

IBM Cloud 카탈로그에서 게이트웨이를 주문하고 구성하고 나면 동일한 설정으로 디바이스 자체도 구성해야 한다는 점을 기억하십시오.
{: tip}

### 연결되지 않은 계정으로 주문
{: #ordering-with-a-unlinked-account}

계정이 연결되어 있지 않으면 다음 프로시저를 따르십시오.

1.	[고객 포털 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){: new_window}을 열고 계정에 로그인하십시오.
2.	고객 포털 탐색에서 **네트워크 > Gateway Appliance**를 선택하십시오.
3.	**Gateway Appliance** 목록에서 **게이트웨이 주문**을 클릭하십시오.
4.	**주문** 페이지의 드롭 다운 메뉴에서 원하는 데이터 센터를 선택한 후 Juniper vSRX가 프로비저닝되는 서버 하드웨어의 원하는 유형을 선택하십시오.

	듀얼 프로세서 멀티 코어 서버를 사용할 경우 서버 유형으로 **Intel Xeon 5120**을 선택해야 합니다.
  {: note}

5.	**주문** 페이지에서 원하는 경우 **고가용성 쌍** 옵션을 선택한 후 **메모리** 크기를 선택하십시오.
6. 	다음으로 **운영 체제** 아래에서 **Juniper** 탭을 클릭하고 **Juniper vSRX(최대 1Gbps) Standard**(단일 프로세서 서버의 경우) 또는 **Juniper vSRX(최대 10Gbps) Standard**(듀얼 프로세서 서버의 경우)를 선택하십시오. 
7. 	마지막으로 원하는 네트워크 업링크 속도를 선택하십시오.
8.	선택사항을 검토한 후 **주문에 추가**를 클릭하십시오. 주문이 자동으로 확인됩니다.
9.	선택한 데이터 센터에서 고유한 VLAN을 이미 소유하고 있는 경우 **체크아웃** 페이지에서 보호할 백엔드 VLAN을 선택하십시오. 다음을 확인하십시오.
	* 서버의 호스트 이름 및 도메인 이름을 제공하십시오. 
	* 원하는 경우 액세스 인증을 위한 SSH 키를 선택하십시오. 
	* IBM Cloud 서비스 이용 약관 및 서드파티 소프트웨어 이용 약관의 모든 선택란을 선택하십시오. 
10. **주문 제출**을 클릭하십시오.

## 다음에 수행할 작업
{: #what-s-next-}

주문이 승인된 후 vSRX의 프로비저닝이 자동으로 시작됩니다. 프로비저닝 프로세스가 완료되면 게이트웨이가 **Gateway Appliance** 목록에 표시됩니다.

게이트웨이 이름을 클릭하여 **게이트웨이 세부사항** 페이지를 여십시오. 디바이스에 대한 IP 주소, 로그인 사용자 이름 및 비밀번호가 표시됩니다.

<img src="images/after_order.png" alt="그림" style="width: 700px;"/>
