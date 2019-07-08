---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: basics, performing, accessing, ssh, device, gateway, configuration, mode, juniper, ui, dns, htp, password

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# IBM Cloud Juniper vSRX 기본사항 수행
{: #performing-ibm-cloud-juniper-vsrx-basics}

IBM® Cloud Juniper vSRX 게이트웨이는 SSH를 통해 원격 콘솔 세션을 사용하거나 Juniper 웹 관리 GUI에 로그인하여 구성될 수 있습니다.

쉘 및 인터페이스 외부에서 vSRX를 구성하면 예기치 않은 결과가 생성될 수 있으므로 권장되지 않습니다.
{: note}

## SSH를 사용하여 디바이스에 액세스
{: #accessing-the-device-using-ssh}

사용자가 SoftLayer VPN에 있는 경우 공인 IP 주소를 통하거나 사설 IP 주소를 통해 SSH를 사용하여 vSRX에 액세스할 수 있습니다.

1. Gateway Appliance 세부사항 화면으로 이동하여 공용 게이트웨이 IP 또는 사설 게이트웨이 IP를 가져오십시오.

  <img src="images/gw-sa-details.png" alt="그림" style="width: 700px;"/>

2. "눈" 아이콘을 클릭하여 관리자의 비밀번호를 표시하십시오.

3. `ssh admin@<gateway-ip>` 명령을 실행한 후 관리자의 비밀번호를 입력하십시오.

"눈" 아이콘이 표시되지 않으면 비밀번호를 볼 수 있는 권한이 없는 것일 수 있습니다. 계정 소유자가 갖고 있는 액세스 권한을 확인하십시오.
{: note}

## 구성 모드에 액세스
{: accessing-the-configuration-mode}

쉘이 vSRX에 열리면 `config` 명령을 실행하여 구성 모드로 설정될 수 있습니다. 다음 명령을 사용하여 이 모드에서 여러 사항을 수행할 수 있습니다.

* `show` - 구성 보기  
* `show | compare` - 스테이징된 변경사항 보기
* `set` - 변경사항 스테이징
* `commit check` - 구성의 구문 확인

변경사항에 문제가 없으면 `commit`와 `save` 명령을 차례로 실행하여 변경사항을 활성 구성으로 커미트할 수 있습니다.  

구성 모드를 유지하려면 `exit` 명령을 실행하십시오.

## Juniper 웹 관리 UI를 사용하여 디바이스에 액세스
{: #accessing-the-device-using-the-juniper-web-management-ui}

기본적으로 Juniper 웹 관리 GUI는 자체 서명 인증서가 생성된 vSRX로 구성되었습니다. 포트 8443에서 https만 사용으로 설정됩니다. `https://gateway-ip:8443`에서 액세스할 수 있습니다.

![Gateway Appliance HA 세부사항](images/vSRX-webui.png)

## 시스템 사용자 작성
{: #creating-system-users}

기본적으로 IBM Cloud Juniper vSRX는 사용자 이름 `admin`의 SSH 액세스 권한을 사용하여 구성됩니다. 추가 사용자는 고유한 우선순위 세트로 추가될 수 있습니다. 예를 들면, 다음과 같습니다.

```
set system login user ops class operator authentication encrypted-password <CYPHER>
```

이 예제에서 `ops`는 사용자 이름이고 `operator`는 사용자에게 지정된 클래스/권한 레벨입니다.

사용자 정의된 클래스는 사전 정의된 클래스와 반대로 정의될 수도 있습니다.

## vSRX 호스트 이름 정의
{: #defining-the-vsrx-hostname}

다음 명령을 사용하여 vSRX 호스트 이름을 설정하거나 변경할 수 있습니다.

```
set system host-name <hostname>
```

## DNS 및 NTP 구성
{: #configuring-dns-and-ntp}

이름 서버 분석 및 NTP를 구성하려면 다음 명령을 실행하십시오.

```
set system name-server <DNS server>
set system ntp <NTP server>
```

## 루트 비밀번호 변경
{: #changing-the-root-password}

다음 명령을 실행하여 루트 비밀번호를 변경할 수 있습니다.

```
set system root-authentication plain-text-password
```

이 프롬프트를 통해 사용자는 구성에 암호화되고 저장되며 표시되지 않는 새 비밀번호를 입력할 수 있습니다.
