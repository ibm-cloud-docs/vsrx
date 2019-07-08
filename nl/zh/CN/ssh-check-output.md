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

# 确认输出并落实更改
{: #confirming-the-output-and-commiting-the-changes}

在已对所做的更改和添加进行编译打包后，运行以下命令来确认将落实到活动配置的内容：

```
show | compare
```

下面是预期的输出：

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

检查以确认配置正确后，运行 `commit` 命令以将更改推送到活动配置。

IBM Cloud Juniper vSRX Standard 现在配置为路由和过滤流至新 VLAN 和子网的流量，并仅允许入站 ping 和 SSH 连接。

现在，您应该如[管理 VLAN](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans)中所示来路由 VLAN，以开始使用新功能。
