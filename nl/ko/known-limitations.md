---

copyright:
  years: 2018
lastupdated: "2018-11-06"

keywords: limitations, problems

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

# IBM Cloud Juniper vSRX에 대한 알려진 제한사항
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

{{site.data.keyword.cloud}} IBM® Cloud Juniper vSRX의 현재 제한사항:

* Juniper vSRX Gateway는 Linux Bridge를 사용하여 네트워킹 가상화로 배치됩니다. Linux Bridge 기반 네트워킹 가상화는 제한된 처리량에만 도달하고 최대 속도 처리량에는 도달하지 않을 수 있습니다.

* 독립형에서 고가용성 모드로의 업그레이드는 지원되지 않습니다.

* IBM Cloud Juniper vSRX 게이트웨이는 Junos OS 버전 `15.1` 또는 `18.4` 옵션과 함께 배치됩니다. 현재는 다른 버전으로 업그레이드/다운그레이드를 지원하지 않습니다. 

* 60일 평가판 라이센스를 사용하면 시스템에 다른 유효한 라이센스가 있는 경우에도 커널에서 오류 메시지를 생성할 수 있습니다. 이 문제를 방지하려면 60일 평가판 라이센스를 모두 제거해야 합니다. 이를 수행하려면 다음 프로시저를 수행하십시오.

1. vSRX 게이트웨이 디바이스에 로그인하십시오. 

2. 콘솔 프롬프트에서 `cli` 명령을 실행하여 CLI 모드로 전환하십시오.

3. 다음 명령을 실행하여 라이센스 ID를 얻으십시오. 

```
show system license
```
출력은 다음과 유사합니다.

```
License usage:
                                 Licenses     Licenses    Licenses    Expiry
  Feature name                       used    installed      needed
  logical-system                        0            3           0    permanent
  Virtual Appliance                     1            1           0    2021-10-18 00:00:00 UTC
  remote-access-ipsec-vpn-client        0            2           0    permanent

Licenses installed:
  License identifier: E2018101804
  License version: 4
  Software Serial Number: SUB00024128768
  Customer ID: IBM_SL_10G
  Features:
    Virtual Appliance - Virtual Appliance
      date-based, 2018-10-18 00:00:00 UTC - 2021-10-18 00:00:00 UTC
```

4. 삭제할 라이센스의 ID를 복사한 후 다음 명령을 실행하십시오. 

```
request system license delete <license identifier>
```
