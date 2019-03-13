---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Erneutes Laden/Migration des Betriebssystems
Der Prozess zum erneuten Laden des Betriebssystems wird verwendet, um einen Gateway-Server erneut zu erstellen. Bei dem Prozess werden folgende Aktionen ausgeführt:

* Betriebssystem des Server-Hosts erneut laden
* Kernel-based Virtual Machine (KVM) im Betriebssystem installieren
* vSRX-VM in der KVM erstellen
* vSRX-Komponente mit der Standardkonfiguration für IBM® Cloud neu konfigurieren

Das Ausführen des Prozesses dauert in der Regel 1 Stunde und 40 Minuten. Eigenständige Gateways sind in diesem Zeitraum außer Betrieb. Wenn Sie ein Juniper-Gateway mit Hochverfügbarkeit verwenden und das Betriebssystem auf einem Ihrer Server erneut laden, wird für die vSRX-Komponente ein Failover auf einen anderen Server im Cluster ausgeführt und die Komponente fährt fort, Datenverkehr zu verarbeiten. Sobald das erneute Laden abgeschlossen ist, wird der Server wieder im Cluster verfügbar.

**Vorsicht:** Wenn Sie bereits ein Juniper vSRX-Cluster mit Hochverfügbarkeit ausführen, dürfen Sie ein erneutes Laden des Betriebssystems nicht gleichzeitig auf beiden Servern des Hochverfügbarkeitsgateways ausführen. Dadurch würde der vSRX-Cluster gelöscht und das Gateway wäre außer Betrieb. Wurde der vSRX-Cluster gelöscht, müssen Sie die Option **Cluster erneut erstellen** verwenden (Details finden Sie unten), um die vSRX-Komponente erneut bereitzustellen und den Hochverfügbarkeitscluster neu zu erstellen.

## Erneutes Laden des Betriebssystems ausführen
Führen Sie das folgende Verfahren aus, um das Betriebssystem für einen Gateway-Server erneut zu laden:

1. [Rufen Sie die Anzeige für die Gateway-Appliances auf](access-gateway-appliances.html), die sich im Kundenportal befindet, und navigieren Sie zur Seite mit den Gateway-Details, indem Sie den Namen des gewünschten Gateways auswählen.

2. Klicken Sie in der Hardwareanzeige auf den Servernamen.
![Hardware-Server](images/os_hardware.png)

3. Klicken Sie auf der Seite der Einheit im Dropdown-Menü 'Aktion' auf **Betriebssystem erneut laden**, um auf die Seite mit der Serverkonfiguration zuzugreifen.
![Details zur Einheit](images/os_device_page.png)

4. Auf der Seite mit der Serverkonfiguration können Sie das erneute Laden konfigurieren und starten. Wenn Sie das erneute Laden von einem anderen Betriebssystem ausführen, klicken Sie auf die Option **Bearbeiten** neben **Betriebssystem**, wählen Sie **Juniper** aus und wählen Sie anschließend eine der Optionen für Juniper vSRX 15.x Standard aus. Wenn Sie mit dem Ändern Ihrer Einstellungen fertig sind, wählen Sie **Über der Konfiguration erneut laden** aus, um fortzufahren.

5. Die Anzeige mit den Details zum erneuten Laden des Betriebssystems wird angezeigt. Prüfen Sie die gewählten Einstellungen und klicken Sie auf **Einstellungen bearbeiten**, wenn Änderungen erforderlich sind. Klicken Sie andernfalls auf **Weiter**, um fortzufahren.

6. Stimmen Sie in der Bestätigungsanzeige für das erneute Laden des Betriebssystems den Bedingungen der Rahmenvereinbarung zu und beginnen Sie dann den Prozess für das erneute Laden des Betriebssystems, indem Sie auf **Erneutes Laden des Betriebssystems bestätigen** klicken. Wenn Sie nicht mit dem erneuten Laden fortfahren möchten, klicken Sie auf **Abbrechen**.

## Migration von einem Vyatta/VRA-Server (VRA – Virtual Router Appliance) auf eine Juniper vSRX-Komponente mithilfe des erneuten Ladens des Betriebssystems ausführen
Wenn Sie ein erneutes Laden für einen eigenständigen Vyatta-Server ausführen, wird eine eigenständige Juniper vSRX-Komponente bereitgestellt, wenn das erneute Laden des Betriebssystems abgeschlossen ist. Es werden dieselben IP-Adressen des Gateways verwendet und das Kennwort für den Rootbenutzer auf dem Host-Server (sowie das Kennwort für den Benutzer mit Verwaltungsaufgaben und den Rootbenutzer in der vSRX-Komponente) wird zurückgesetzt.

Wenn Sie Vyatta-Server mit Hochverfügbarkeit erneut laden, müssen Sie den Befehl `Betriebssystem erneut laden` auf beiden Servern ausführen. Dadurch wird Ubuntu 16.04 installiert. Verwenden Sie als Nächstes die Option zum erneuten Erstellen eines Clusters (Details finden Sie im folgenden Abschnitt), um die vSRX-Komponente bereitzustellen und den Hochverfügbarkeitscluster zu erstellen. Es werden dieselben IP-Adressen des Gateways verwendet wie bei einer eigenständigen vSRX-Komponente und das zum Rootbenutzer gehörige Kennwort auf dem Host-Server (genauso wie das Kennwort für den Benutzer mit Verwaltungsaufgaben und den Rootbenutzer in der vSRX-Komponente) wird zurückgesetzt.

**Achtung:** Führen Sie ein erneutes Laden des Betriebssystems nicht auf nur einem einzigen Server des Vyatta-Hochverfügbarkeitsclusters aus. Das Vorhandensein zweier unterschiedlicher Betriebssysteme in einem einzigen Gateway-Hochverfügbarkeitscluster ist nicht unterstützt.

## vSRX-Hochverfügbarkeitscluster erneut erstellen
Führen Sie das folgende Verfahren aus, um einen Ihrer vSRX-Hochverfügbarkeitscluster erneut zu erstellen:

1. [Rufen Sie die Anzeige für die Gateway-Appliances auf](access-gateway-appliances.html), die sich im Kundenportal befindet, und navigieren Sie zur Seite mit den Gateway-Details, indem Sie den gewünschten Namen eines Gateways mit Hochverfügbarkeit auswählen.

2. Klicken Sie in der vSRX-Anzeige auf **Cluster erneut erstellen**.
![Cluster erneut erstellen](images/rebuild_cluster.png)

3. Lesen Sie die Warnnachricht sorgfältig. Die Operation zum erneuten Erstellen eines Clusters ist zerstörerisch. Wenn Sie fortfahren möchten, müssen Sie Ihre vSRX-Konfiguration speichern, bevor Sie den Prozess durch Klicken auf **Erneut erstellen** starten.
![Erneutes Erstellen des Clusters bestätigen](images/rebuild_cluster_confirm.png)
