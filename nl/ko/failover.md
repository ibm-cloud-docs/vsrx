---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: working, failover, codes, failure, cli

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

# 장애 복구 관련 작업
{: #working-with-failover}

이 절은 Juniper vSRX 게이트웨이 디바이스가 고가용성 모드에서 프로비저닝되는 경우에만 적용 가능합니다.
{: note}

이 절에서는 모든 제어 및 데이터 플레인 트래픽이 장애 복구 후 두 번째 게이트웨이 디바이스를 통해 라우트되도록 기본 게이트웨이 디바이스에서 장애 복구를 초기화하는 방법에 대해 설명합니다.

이를 수행하려면 다음 프로시저를 수행하십시오.

1. 기본 vSRX 게이트웨이 디바이스에 로그인하십시오.

2. 콘솔 프롬프트에서 `cli` 명령을 실행하여 CLI 모드로 전환하십시오. CLI 모드로 전환하면 콘솔에는 `primary` 또는 `secondary` 중 하나의 노드 역할이 표시됩니다.

	사용자가 `primary` 노드에 있는지 확인하십시오. 그렇지 않으면 종료한 후 다른 vSRX 게이트웨이 디바이스 쌍에 로그인하십시오.

2. 기본 vSRX 게이트웨이 디바이스에서 다음 명령을 실행하십시오.

	```
	show chassis cluster status
	```
	출력은 다음과 유사합니다.

	```
	장애 코드 모니터:
		CS  콜드 동기화 모니터링        FL  패브릭 연결 모니터링
		GR  GRES 모니터링               HW  하드웨어 모니터링
		IF  인터페이스 모니터링         IP  IP 모니터링
		LB  루프백 모니터링             MB  Mbuf 모니터링
		NH  Nexthop 모니터링            NP  NPC 모니터링
		SP  SPU 모니터링                SM  스케줄 모니터링
		CF  구성 동기화 모니터링

	클러스터 ID: 2
	노드   우선순위 상태          예방 매뉴얼   	모니터 실패

	중복성 그룹: 0, 장애 복구 횟수: 1
	node0  100      primary        no      no       없음
	node1  1        secondary      no      no       없음
	중복성 그룹: 1, 장애 복구 횟수: 1
	node0  100      primary        yes     no       없음
	node1  1        secondary      yes     no       없음

	{primary:node0}
	```

	두 중복성 그룹에 대해 동일한 노드가 `primary`로 설정되어 있는지 확인하십시오. 다른 노드가 다른 중복성 그룹에서 `primary` 역할로 설정될 수 있습니다. 
	
	기본적으로 vSRX는 `Preempt`를 중복성 그룹 1의 경우 `yes`로 설정하고 중복성 그룹 0의 경우 `no`로 설정합니다. [이 링크![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.juniper.net/documentation/en_US/junos/topics/topic-map/security-chassis-cluster-redundancy-group-failover.html){:new_window}를 참조하여 선점 및 장애 복구 동작에 대해 자세히 알아보십시오.
	{: note}

3. 콘솔 프롬프트에서 다음 명령을 실행하여 장애 복구를 초기화하십시오.

	```
	request chassis cluster failover redundancy-group <redundancy group number> node <node number>
	```

	2단계의 명령 출력에서 적합한 중복성 그룹 번호 및 노드 번호를 선택하십시오. 두 중복성 그룹의 장애를 복구하려면 각 그룹에 하나씩 이전 명령을 두 번 실행하십시오.

4. 장애 복구가 완료된 후 콘솔 출력을 확인하십시오. 이제 `secondary`로 나열되어야 합니다.

5. 다른 vSRX 게이트웨이 쌍에 로그인하십시오. `cli` 명령을 다시 실행하여 CLI 모드로 전환한 후 콘솔 출력이 `primary`로 표시되는지 확인하십시오.

Juniper vSRX 게이트웨이 디바이스에서 CLI 모드로 전환하면 출력이 제어 플레인 퍼스펙티브에서 `primary`로 표시됩니다. 데이터 플레인 퍼스펙티브에서 기본인 게이트웨이 디바이스를 판별하려면 항상 `show chassis cluster status` 출력을 확인하십시오. 중복성 그룹과 제어 플레인 및 데이터 플레인에 대해 자세히 알아보려면 [vSRX 기본 구성](/docs/infrastructure/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration)을 참조하십시오.
{: tip}
