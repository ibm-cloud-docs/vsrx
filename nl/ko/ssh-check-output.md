---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: confirming, output, committing, changes, vlans, ssh

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# 출력 확인 및 변경사항 커미트
{: #confirming-the-output-and-commiting-the-changes}

수행된 변경사항 및 추가사항이 시작된 후 다음 명령을 실행하여 활성 구성에 커미트되는 항목을 확인하십시오.

```
show | compare
```

예상되는 출력은 다음과 같습니다.

```
[edit security address-book global]
     address SL_PUB_MGMT { ... }
+    address VSI_PUB_NET 169.47.211.152/29;
[edit security policies]
     from-zone SL-PUBLIC to-zone SL-PUBLIC { ... }
+    from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC {
+        policy ALLOW_INTERNAL {
+            description "Allow all traffic within CUSTOMER_PUBLIC zone";
+            match {
+                source-address any;
+                destination-address any;
+                application any;
+            }
+            then {
+                permit;
+            }
+        }
+    }
+    from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC {
+        policy ALLOW_OUTBOUND {
+            description "Allow all outbound traffic from CUSTOMER-PUBLIC to the internet";
+            match {
+                source-address any;
+                destination-address any;
+                application any;
+            }
+            then {
+                permit;
+            }
+        }
+    }
+    from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC {
+        policy ALLOW_PING_SSH {
+            description "Allow ping and SSH to public subnet";
+            match {
+                source-address any;
+                destination-address VSI_PUB_NET;
+                application [ junos-ssh junos-ping ];
+            }
+            then {
+                permit;
+            }
+        }
+    }
[edit security zones]
     security-zone SL-PUBLIC { ... }
+    security-zone CUSTOMER-PUBLIC {
+        interfaces {
+            reth3.1523 {
+                host-inbound-traffic {
+                    system-services {
+                        all;
+                    }
+                }
+            }                          
+        }
+    }
[edit interfaces reth3]
+    unit 1523 {
+        vlan-id 1523;
+        family inet {
+            address 169.47.211.153/29;
+        }
+    }
```

구성이 올바른지 확인한 후 `commit` 명령을 실행하여 변경사항을 활성 구성으로 푸시하십시오.

IBM Cloud Juniper vSRX Standard는 인바운드 Ping 및 SSH 연결만 허용하여 이제 라우트되고 새 VLAN과 서브넷에 대한 트래픽을 필터링하도록 구성됩니다.

이제 새 기능을 사용하여 시작하도록 [VLAN 관리](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans)에 표시된 대로 VLAN을 라우트해야 합니다.
