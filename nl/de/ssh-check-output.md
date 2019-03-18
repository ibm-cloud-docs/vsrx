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

# Ausgabe bestätigen und Änderungen festschreiben
{: #confirming-the-output-and-commiting-the-changes}

Wenn die von Ihnen vorgenommenen Änderungen und Zusätze zwischengespeichert wurden, führen Sie den folgenden Befehl aus, um zu bestätigen, was für die aktive Konfiguration festgeschrieben werden soll:

```
show | compare
```

Dies ist die erwartete Ausgabe:

```
[edit security address-book global]
     address SL_PUB_MGMT { ... }
+    address VSI_PUB_NET 169.47.211.152/29;
[edit security policies]
     from-zone SL-PUBLIC to-zone SL-PUBLIC { ... }
+    from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC {
+        policy ALLOW_INTERNAL {
+            description "Jeglichen Datenverkehr innerhalb der Zone CUSTOMER_PUBLIC zulassen";
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
+            description "Jeglichen ausgehenden Datenverkehr von CUSTOMER-PUBLIC an das Internet zulassen";
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
+            description "Ping und SSH an öffentliches Teilnetz zulassen";
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

Führen Sie nach der Überprüfung der Richtigkeit der Konfiguration den Befehl `commit` aus, um die Änderungen mit einer Push-Operation an die aktive Konfiguration zu übertragen.

Ihre Komponente Juniper vSRX Standard für IBM Cloud ist nun so konfiguriert, dass Datenverkehr an das neue VLAN und das neue Teilnetz weitergeleitet und gefiltert wird; dabei werden nur eingehende Pingbefehle und SSH-Verbindungen zugelassen. 

Sie sollten das VLAN nun wie in [VLANs verwalten](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans) gezeigt weiterleiten, um die neue Funktionalität in Betrieb zu nehmen.
