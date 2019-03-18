---

copyright:
  years: 2018
lastupdated: "2018-11-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Einführung in das Gateway Juniper vSRX für IBM Cloud
{: #getting-started-with-ibm-cloud-juniper-vsrx-gateway}

Ermitteln Sie für den Start des Gateways Juniper vSRX für IBM® Cloud zunächst, ob Ihr Konto mit IBM Cloud verknüpft ist.

## Vorbereitende Schritte

Um zu ermitteln, ob Ihr Konto verknüpft ist, navigieren Sie in Ihrem Browser zum [Kundenportal ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){: new_window} und melden Sie sich dort an. Wenn Ihr Konto nicht verknüpft ist, wird in der rechten oberen Ecke **Mehr über Bluemix erfahren!** angezeigt.

## Schritte zur Bestellung

Sie können Ihre Gateway-Appliance mithilfe einer der folgenden Methoden bestellen:

Sie finden eine Liste mit den bekannten Einschränkungen für das Gateway Juniper vSRX für IBM Cloud im [Abschnitt 'Bekannte Einschränkungen'](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx).
{:note}

### Mit einem verknüpften Konto bestellen
Ist Ihr Konto verknüpft, verwenden Sie folgendes Verfahren:

1.	Öffnen Sie die [IBM Cloud-Konsole ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.bluemix.net/){: new_window} und melden Sie sich bei Ihrem Konto an.
2.	Wählen Sie in der linken Navigationsleiste die Optionen **Infrastruktur > Netz > Gateway-Appliances** aus.
3.	Klicken Sie in der Liste mit den **Gateway-Appliances** auf **Gateway erstellen**.
4. Wählen Sie auf der Seite **Bestellen** Werte für **Hostname** und **Domäne** aus.
5. Wählen Sie, falls gewünscht, die Option **HA-Paar** aus.

	<img src="images/linked_order.png" alt="Zeichnung" style="width: 700px;"/>

5. Wählen Sie als Nächstes Ihren **Standort** und den zugeordneten **Pod** aus; wählen Sie anschließend Ihren **Server** und die gewünschte Menge an **RAM** aus.

	Wenn Sie planen, einen Multi-Core-Server mit Dualprozessor zu verwenden, müssen Sie als Servertyp **Intel Xeon 5120** auswählen. {:note:}

	<img src="images/linked_server.png" alt="Zeichnung" style="width: 600px;"/>

6. Wählen Sie einen SSH-Schlüssel aus, wenn Sie ihn für die Authentifizierung des Zugriffs auf Ihr neues Gateway verwenden wollen.
7. Wählen Sie unter **Image** für einen Server mit Einzelprozessor die Option **Juniper vSRX 15.x (bis 1 Gb/s) Standard** oder für einen Server mit Dualprozessor die Option **Juniper vSRX 15.x (bis zu 10 Gb/s) Standard** aus.
8. Wählen Sie beliebig optionale Add-ons aus, fügen Sie zusätzliche **Speicherplatten** hinzu und wählen Sie die gewünschte **Uplink-Port-Geschwindigkeit** aus.
8. Überprüfen Sie Ihre Auswahl in der **Bestellübersicht**, lesen Sie die Bedingungen für die Software anderer Anbieter und stimmen Sie zu.
9. Klicken Sie zuletzt auf **Bereitstellen**.

### Mit einem nicht verknüpften Konto bestellen
Ist Ihr Konto nicht verknüpft, verwenden Sie folgendes Verfahren:

1.	Öffnen Sie das [Kundenportal ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){: new_window} und melden Sie sich bei Ihrem Konto an.
2.	Wählen Sie in der Navigation des Kundenportals die Optionen **Netz > Gateway-Appliances** aus.
3.	Klicken Sie in der Liste mit den **Gateway-Appliances** auf **Gateway bestellen**.
4.	Wählen Sie Ihr bevorzugtes Rechenzentrum im Dropdown-Menü auf der Seite **Bestellen** aus und wählen Sie den gewünschten Typ der Server-Hardware, in der die Komponente Juniper vSRX bereitgestellt werden soll.

	Wenn Sie planen, einen Multi-Core-Server mit Dualprozessor zu verwenden, müssen Sie als Servertyp **Intel Xeon 5120** auswählen. {:note}

5.	Wählen Sie, falls gewünscht, auf der Seite **Bestellen** die Option **HA-Paar** aus und wählen Sie anschließend die Größe für den **Speicher** aus.
6. 	Klicken Sie als Nächstes unter **Betriebssystem** auf die Registerkarte **Juniper** und wählen Sie für einen Server mit Einzelprozessor die Option **Juniper vSRX 15.x (bis 1 Gb/s) Standard** bzw. für einen Server mit Dualprozessor die Option **Juniper vSRX 15.x (bis zu 10 Gb/s) Standard** aus.
7. 	Wählen Sie zuletzt die gewünschte Uplink-Geschwindigkeit des Netzes aus.
8.	Überprüfen Sie Ihre Auswahl und klicken Sie anschließend auf **Zur Bestellung hinzufügen**. Ihre Bestellung wird automatisch geprüft.
9.	Wenn Sie auf der Seite **Kasse** im ausgewählten Rechenzentrum bereits über eigene VLANs verfügen, wählen Sie die Back-End-VLANs aus, die Sie schützen möchten. Achten Sie auf Folgendes:
	* Geben Sie Ihrem Server einen Hostnamen und einen Domänennamen.
	* Wählen Sie, falls gewünscht, einen SSH-Schlüssel für die Zugriffsauthentifizierung aus.
	* Wählen Sie alle Kästchen für die IBM Cloud-Servicebedingungen und die Bedingungen für die Software anderer Anbieter aus.
10. Klicken Sie auf **Bestellung abschicken**.

## Weitere Schritte
Sobald Ihre Bestellung genehmigt wurde, beginnt die Bereitstellung Ihrer vSRX-Komponente automatisch. Wenn der Bereitstellungsprozess abgeschlossen ist, wird das Gateway in der Liste mit den **Gateway-Appliances** angezeigt.

Klicken Sie auf den Namen des Gateways, um die Seite mit den **Gateway-Details** zu öffnen. Sie finden dort die IP-Adressen, den Benutzernamen für die Anmeldung und die Kennwörter der Einheit.

<img src="images/after_order.png" alt="Zeichnung" style="width: 700px;"/>
