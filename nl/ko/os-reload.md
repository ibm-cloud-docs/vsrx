---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: reloading, os, upgrading, kvm, ha, standalone

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

# OS 다시 로드
{: #reloading-the-os}

OS 다시 로드 프로세스는 게이트웨이 서버를 다시 빌드하는 데 사용됩니다. 프로세스에서는 다음 조치를 수행합니다.

* 서버 호스트의 운영 체제 다시 로드
* 운영 체제에 KVM 설치
* KVM에서 vSRX VM 작성
* IBM® Cloud를 위한 기본 구성으로 vSRX 다시 구성

프로세스를 완료하는 데 보통 1시간 40분이 필요합니다. 이 기간 동안 독립형 게이트웨이 사용이 중단됩니다. Juniper 고가용성(HA) 게이트웨이의 경우 클러스터 중 하나에 OS를 다시 로드하면 vSRX는 클러스터의 다른 서버에 대한 장애가 복구되고 데이터 트래픽을 계속 처리합니다. 다시 로드가 완료되면 서버에서 클러스터를 다시 결합합니다.

HA vSRX에서 성공적으로 다시 로드하거나 클러스터를 다시 빌드하려면 다음 조건을 충족하십시오. 

* 프로비저닝된 vSRX 게이트웨이의 루트 비밀번호가 vSRX 포털에 정의된 루트 비밀번호와 일치해야 합니다. 포털의 비밀번호는 게이트웨이가 처음으로 프로비저닝될 때 정의되어 현재 게이트웨이 비밀번호와 일치하지 않을 수 있습니다. 처음 프로비저닝한 후 비밀번호가 변경된 경우에는 SSH를 사용하여 vSRX 게이트웨이에 연결한 후 일치하도록 루트 비밀번호를 변경하십시오. 비밀번호가 변경되면 OS 다시 로드 또는 클러스터 다시 빌드 오퍼레이션으로 진행할 수 있습니다. 

  <img src="images/gw-vsrx-password.png" alt="그림" style="width: 700px;"/>

* 고가용성 게이트웨이의 두 서버 모두에서 동시에 OS 다시 로드를 수행하지 **마십시오**. 

HA 게이트웨이의 두 서버 모두에서 동시에 OS 다시 로드를 수행하면 vSRX 클러스터가 영구 삭제되고 게이트웨이 사용이 중단됩니다. vSRX 클러스터가 영구 삭제되는 경우 **클러스터 다시 빌드** 옵션(아래 설명됨)을 사용하여 vSRX를 다시 프로비저닝하고 HA 클러스터를 다시 작성해야 합니다.
{: important}

## OS 다시 로드 수행
{: #performing-an-os-reload}

게이트웨이 서버를 위한 OS를 다시 로드하려면 다음 프로시저를 수행하십시오.

1. 고객 포털에서 [Gateway Appliance 화면에 액세스](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances)하고 원하는 게이트웨이 이름을 선택하여 게이트웨이 세부사항 페이지로 이동하십시오.

  <img src="images/gw-sa-details.png" alt="그림" style="width: 700px;"/>

2. 하드웨어 패널에서 서버 이름을 클릭하십시오.

  ![하드웨어 서버](images/os_hardware.png)

3. 디바이스 페이지의 조치 드롭 다운 메뉴에서 **OS 다시 로드**를 클릭하여 서버 구성 페이지에 액세스하십시오. 

  ![디바이스 세부사항](images/os_device_page.png)

4. 서버 구성 페이지에서 다시 로드를 구성하고 시작할 수 있습니다. 다른 OS에서 다시 로드하는 중인 경우 **운영 체제** 옆에 있는 **편집**을 클릭하고 **Juniper**를 선택한 후 Juniper vSRX 15.x Standard 옵션 중 하나를 선택하십시오. 설정 수정이 완료되면 **위의 구성 다시 로드**를 선택하여 계속하십시오.

5. OS 다시 로드 세부사항 화면이 표시됩니다. 선택한 설정을 검토하고 **설정 편집**(변경해야 하는 경우)을 클릭하십시오. 그렇지 않으면 **다음**을 클릭하여 계속하십시오.

6. OS 다시 로드 확인 화면에서 마스터 서비스 계약의 조항에 동의한 후 **OS 다시 로드 확인**을 클릭하여 OS 다시 로드 프로세스를 시작하십시오. 다시 로드를 계속하지 않으려면 **취소**를 클릭하십시오.

## HA vSRX 클러스터 다시 빌드
{: #rebuilding-an-ha-vsrx-cluster}

HA vSRX 클러스터 중 하나를 다시 빌드하려면 다음 프로시저를 수행하십시오.

1. 고객 포털에서 [Gateway Appliance 화면에 액세스](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances)하고 원하는 HA 게이트웨이 이름을 선택하여 게이트웨이 세부사항 페이지로 이동하십시오.

2. **조치** 드롭 다운을 클릭한 후 **클러스터 다시 빌드**를 선택하십시오. 

3. 경고 메시지를 주의하여 읽어보십시오. 클러스터를 빌드하기 위한 오퍼레이션은 파괴적입니다. 계속하려면 **다시 빌드**를 클릭하여 프로세스를 시작하기 전에 vSRX 구성을 저장하십시오. 

  ![클러스터 다시 빌드 확인](images/rebuild_cluster_confirm.png)
