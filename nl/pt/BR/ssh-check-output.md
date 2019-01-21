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

# Certifique a saída e confirme as mudanças
Após estagiar as mudanças e inclusões feitas, execute o comando a seguir para certificar o que será confirmado na configuração ativa:

```
show | compare
```

Esta é a saída esperada:

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
+ source-address any; + destination-address any; + application any; + }
+ then {
+ permit; + }
+        }
+    }
+    from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC {
+        policy ALLOW_OUTBOUND {
+            description "Allow all outbound traffic from CUSTOMER-PUBLIC to the internet";
+            match {
+ source-address any; + destination-address any; + application any; + }
+ then {
+ permit; + }
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
+ then {
+ permit; + }
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

Depois de verificar que a configuração está correta, execute o comando `commit` para enviar por push as mudanças para a configuração ativa.

Agora, o seu IBM Cloud Juniper vSRX Standard está configurado para rotear e filtrar o tráfego para as novas VLAN e sub-rede, permitindo apenas pings de entrada e conexões SSH. 

Agora, é necessário rotear a VLAN conforme mostrado em [Gerenciar VLANs](manage-vlans.html) para começar a usar a nova funcionalidade.
