---

copyright:
  years: 2018
lastupdated: "2018-11-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# IBM Cloud Juniper vSRX Gateway 시작하기
{: #getting-started-with-ibm-cloud-juniper-vsrx-gateway}

IBM® Cloud Juniper vSRX Gateway를 시작하려면 먼저 사용자의 계정이 IBM Cloud에 연결되어 있는지 여부를 판별하십시오.

## 시작하기 전에

연결된 계정이 있는지 여부를 판별하려면 브라우저에서 [고객 포털 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){: new_window}로 이동하여 로그인하십시오. 계정이 연결되어 있지 않으면 오른쪽 상단에 **Bluemix에 대해 자세히 알아보기!** 단추가 표시됩니다.

## 주문 단계

다음 방법 중 하나를 사용하여 Gateway Appliance를 주문할 수 있습니다.

IBM Cloud Juniper vSRX Gateway의 알려진 제한사항의 목록은 [알려진 제한사항 주제](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx)를 참조하십시오.
{:note}

### 연결된 계정으로 주문
계정이 연결되어 있으면 다음 프로시저를 따르십시오.

1.	[IBM Cloud 콘솔![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.bluemix.net/){: new_window}을 열고 계정에 로그인하십시오.
2.	왼쪽 탐색에서 **인프라 > 네트워크 > Gateway Appliance**를 선택하십시오.
3.	**Gateway Appliance** 목록에서 **게이트웨이 작성**을 클릭하십시오.
4. **주문** 페이지에서 **호스트 이름** 및 **도메인**을 선택하십시오.
5. 원하는 경우 **고가용성 쌍** 옵션을 선택하십시오.

	<img src="images/linked_order.png" alt="그림" style="width: 700px;"/>

5. 그런 다음 **위치** 및 연관된 **팟(Pod)**을 선택한 후 **서버**와 원하는 **RAM**의 크기를 선택하십시오.

	듀얼 프로세서 멀티 코어 서버를 사용할 경우 서버 유형으로 **Intel Xeon 5120**을 선택해야 합니다. {:note:}

	<img src="images/linked_server.png" alt="그림" style="width: 600px;"/>

6. 새 게이트웨이에 대한 액세스를 인증하기 위해 SSH 키를 사용할 경우 SSH 키를 선택하십시오.
7. **이미지**에서 싱글 프로세서 서버용 **Juniper vSRX 15.x(최대 1bps) Standard** 또는 듀얼 프로세서 서버용 **Juniper vSRX 15.x(최대 10Gbps) Standard**를 선택하십시오.
8. 선택적인 추가 기능을 선택하고, 추가 **스토리지 디스크**를 추가하고, 원하는 **포트 속도 업링크**를 선택하십시오.
8. **주문 요약**의 선택사항을 검토한 후 서드파티 소프트웨어 이용 약관을 읽고 동의하십시오.
9. 마지막으로 **프로비저닝**을 클릭하십시오.

### 연결되지 않은 계정으로 주문
계정이 연결되어 있지 않으면 다음 프로시저를 따르십시오.

1.	[고객 포털 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://control.softlayer.com/){: new_window}을 열고 계정에 로그인하십시오.
2.	고객 포털 탐색에서 **네트워크 > Gateway Appliance**를 선택하십시오.
3.	**Gateway Appliance** 목록에서 **게이트웨이 주문**을 클릭하십시오.
4.	**주문** 페이지의 드롭 다운 메뉴에서 원하는 데이터 센터를 선택한 후 Juniper vSRX가 프로비저닝되는 서버 하드웨어의 원하는 유형을 선택하십시오.

	듀얼 프로세서 멀티 코어 서버를 사용할 경우 서버 유형으로 **Intel Xeon 5120**을 선택해야 합니다. {:note}

5.	**주문** 페이지에서 원하는 경우 **고가용성 쌍** 옵션을 선택한 후 **메모리** 크기를 선택하십시오.
6. 	그런 다음 **운영 체제**에서 **Juniper** 탭을 클릭하고 싱글 프로세서 서버용 **Juniper vSRX 15.x(최대 1bps) Standard** 또는 듀얼 프로세서 서버용 **Juniper vSRX 15.x(최대 10Gbps) Standard**를 선택하십시오.
7. 	마지막으로 원하는 네트워크 업링크 속도를 선택하십시오.
8.	선택사항을 검토한 후 **주문에 추가**를 클릭하십시오. 주문이 자동으로 확인됩니다.
9.	선택한 데이터 센터에서 고유한 VLAN을 이미 소유하고 있는 경우 **체크아웃** 페이지에서 보호할 백엔드 VLAN을 선택하십시오. 다음을 확인하십시오.
	* 서버에 대한 호스트 이름 및 도메인 이름을 지정하십시오.
	* 원하는 경우 액세스 인증을 위해 SSH 키를 선택하십시오.
	* IBM Cloud 서비스 이용 약관 및 서드파티 소프트웨어 이용 약관의 모든 상자를 확인하십시오.
10. **주문 제출**을 클릭하십시오.

## 다음에 수행할 작업
주문이 승인된 후 vSRX의 프로비저닝이 자동으로 시작됩니다. 프로비저닝 프로세스가 완료되면 게이트웨이가 **Gateway Appliance** 목록에 표시됩니다.

게이트웨이 이름을 클릭하여 **게이트웨이 세부사항** 페이지를 여십시오. 디바이스에 대한 IP 주소, 로그인 사용자 이름 및 비밀번호가 표시됩니다.

<img src="images/after_order.png" alt="그림" style="width: 700px;"/>
