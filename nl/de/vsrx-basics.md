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

# Grundlegende Aufgaben mit Juniper vSRX für IBM Cloud ausführen
{: #performing-ibm-cloud-juniper-vsrx-basics}

Das Gateway Juniper vSRX für IBM® Cloud kann mithilfe einer fernen Konsolensitzung über SSH oder durch Anmelden bei der Web-Management-GUI von Juniper konfiguriert werden.

**Anmerkung:** Wenn die Komponente vSRX außerhalb der eigenen Shell und Schnittstelle konfiguriert wird, kann dies zu unerwarteten Ergebnissen führen; daher wird dies nicht empfohlen.

## Über SSH auf die Einheit zugreifen

Auf die Komponente vSRX können Sie mithilfe von SSH über eine öffentliche IP-Adresse oder über eine private IP-Adresse zugreifen (wenn Sie sich im SoftLayer-VPN befinden):

1. Wechseln Sie zur Anzeige mit den Details zu Gateway-Appliances und rufen Sie die IP-Adresse des öffentlichen oder des privaten Gateways auf.

  <img src="images/basics.png" alt="Zeichnung" style="width: 700px;"/>

2. Klicken Sie auf das Symbol mit dem Auge, um das Kennwort des Benutzers mit Verwaltungsaufgaben sichtbar zu machen.

3. Führen Sie den Befehl `ssh admin@<gateway-ip>` aus und geben Sie anschließend das Kennwort des Benutzers mit Verwaltungsaufgaben ein.

**Anmerkung:** Wenn Sie das Symbol mit dem Auge nicht sehen, verfügen Sie möglicherweise nicht über die Berechtigung zum Anzeigen des Kennworts. Überprüfen Sie Ihre Zugriffsberechtigungen mit dem Kontoeigner.

## Auf den Konfigurationsmodus zugreifen

Sobald eine Shell für die Komponente vSRX geöffnet wurde, können Sie den Konfigurationsmodus aktivieren, indem Sie den Befehl `config` ausführen. Mithilfe der folgenden Befehle können Sie in diesem Modus verschiedene Aktionen ausführen:

* `show` – Konfigurationen anzeigen  
* `show | compare` – Zwischengespeicherte Änderungen anzeigen
* `set` – Änderungen zwischenspeichern
* `commit check` – Syntax der Konfiguration überprüfen

Wenn Sie mit Ihren Änderungen zufrieden sind, können Sie sie in der aktiven Konfiguration festschreiben, indem Sie die Befehle `commit` und dann `save` ausführen.  

Führen Sie den Befehl `exit` aus, um den Konfigurationsmodus zu verlassen.

## Mithilfe der Web-Management-GUI von Juniper auf die Einheit zugreifen

Die Web-Management-GUI von Juniper wurde standardmäßig mit dem von der Komponente vSRX generierten, selbst signierten Zertifikat konfiguriert. An Port 8443 ist nur HTTPS aktiviert. Sie können über `https://gateway-ip:8443` zugreifen.

![Gateway-Appliance – Details zur Hochverfügbarkeit](images/vSRX-webui.png)

## Mithilfe der VIRSH-Konsole auf die Einheit zugreifen

Sie können auch über das Betriebssystem des Gateway-Servers auf die Komponente vSRX zugreifen:

1. Melden Sie sich an Ihrem Gateway-Server an, indem Sie den Befehl `ssh root@<server-ip>` ausführen.
2. Führen Sie den Befehl `virsh list` aus, um den Namen Ihrer vSRX-VM zu finden.
3. Führen Sie den Befehl `virsh console <your vSRX VM name>` aus.

## Systembenutzer erstellen

Die Komponente Juniper vSRX für IBM Cloud ist für den Benutzernamen `admin` mit SSH-Zugriff konfiguriert. Weitere Benutzer können mit einer eigenen Gruppe von Prioritäten hinzugefügt werden. Beispiel:

```
set system login user ops class operator authentication cipher encrypted-password <VERSCHLÜSSELUNG>
```

In diesem Beispiel ist `ops` der Benutzername und `operator` ist die Klasse/Berechtigungsebene, die dem Benutzer zugeordnet ist.

Es können auch angepasste Klassen – im Gegensatz zu vordefinierten Klassen – definiert werden.

## vSRX-Hostnamen definieren

Sie können den Hostnamen der Komponente vSRX mithilfe des folgenden Befehls festlegen oder ändern:

```
set system host-name <Hostname>
```

## Domain Name Server (DNS) und Network Time Protocol (NTP) konfigurieren

Führen Sie die folgenden Befehle aus, um die Namensserverauflösung und NTP zu konfigurieren:

```
set system name-server <DNS-Server>
set system ntp <NTP-Server>
```

## Rootkennwort ändern

Sie können das Rootkennwort ändern, indem Sie den folgenden Befehl ausführen:

```
set system root-authentication plain-text-password
```

Dadurch werden Sie aufgefordert, ein neues Kennwort einzugeben, das verschlüsselt ist, in der Konfiguration gespeichert wird und nicht sichtbar ist.
