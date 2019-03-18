---

copyright:
  years: 2018
lastupdated: "2018-11-06"

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

# Gateway zurückfordern
{: #reclaiming-a-gateway}

Führen Sie das folgende Verfahren aus, um Ihr Gateway zurückzufordern:

1. [Rufen Sie die Anzeige für die Gateway-Appliances auf](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances), die sich im Kundenportal befindet, und navigieren Sie zur Seite mit den Gateway-Details, indem Sie den Namen des gewünschten Gateways auswählen.

2. Klicken Sie in der Hardwareanzeige auf den Servernamen.

	![Hardware-Server](images/os_hardware.png)

	Stellen Sie vor Zurückfordern eines Gateways sicher, dass die Zuordnung aller geschützten VLANs zum Gateway [aufgehoben](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans) wurde.

3. Klicken Sie auf der Seite der Einheit im Dropdown-Menü 'Aktion' auf **Einheit abbrechen**, um auf die Seite mit der Serverkonfiguration zuzugreifen.  

4. Beginnen Sie den Rückforderungsprozess in der Bestätigungsanzeige 'Einheit abbrechen', indem Sie auf **Weiter** klicken. Wenn Sie nicht mit dem Rückforderungsprozess fortfahren wollen, klicken Sie auf **Schließen**.

Bei Hochverfügbarkeitspaaren müssen diese Aktionen auf beiden Einheiten ausgeführt werden.
