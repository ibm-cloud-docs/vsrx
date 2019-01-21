---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 出力の確認と変更のコミット
加えた変更と追加がステージングされた後に、以下のコマンドを実行して、アクティブ構成にコミットされる内容を確認します。

```
show | compare
```

下記のように出力されるはずです。

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

構成が正しいことを確認した後に、`commit` コマンドを実行して、変更をアクティブ構成にプッシュします。

この時点で IBM Cloud Juniper vSRX Standard は、トラフィックを新しい VLAN とサブネットに経路指定してフィルター操作するように構成され、インバウンド ping と SSH 接続のみが許可されます。 

次に、[VLAN の管理](manage-vlans.html)で示されているように VLAN を経路指定して、新機能の使用を開始してください。
