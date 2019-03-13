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

# Mit Firewalls arbeiten
Die Komponente Juniper vSRX-Gateway für IBM® Cloud verwendet das Konzept der Sicherheitszonen, bei dem jede vSRX-Schnittstelle zum Handhaben von statusabhängigen Firewalls einer 'Zone' zugeordnet ist. Statusunabhängige Firewalls werden von Firewallfiltern gesteuert.

Zum Zulassen und Blockieren von Datenverkehr zwischen diesen definierten Zonen werden Richtlinien verwendet und die hier definierten Regeln sind statusabhängig.

In IBM Cloud sind vSRX-Komponenten so konzipiert, dass sie vier unterschiedliche Sicherheitszonen aufweisen:

| Zone                     | Eigenständige Schnittstelle |Hochverfügbarkeitsschnittstelle|
| :---                     |        :----:        |         ---: |
| SL-Private (ohne Tag)    | ge-0/0/0.0           | reth0.0      |
| SL-Public (ohne Tag)     | ge-0/0/1.0           | reth1.0      |
| Customer-Private (mit Tag versehen)| ge-0/0/0.1           | reth2.1      |
| Customer-Public (mit Tag versehen) | ge-0/0/1.1           | reth3.1      |

## Zonenrichtlinien
Führen Sie das folgende Verfahren aus, um eine statusabhängige Firewall zu konfigurieren:

1. Erstellen Sie Sicherheitszonen und ordnen Sie die entsprechenden Schnittstellen zu:

	Eigenständiges Szenario:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces ge-0/0/1.1
	```
	Hochverfügbarkeitsszenario:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces reth2.1
	```
2. Definieren Sie die Richtlinie und die Regeln, die zwischen zwei verschiedenen Zonen gelten sollen.

	Im folgenden Beispiel wird der Ping-Datenverkehr von der Zone `Customer-Private` zur Zone `Customer-Public` dargestellt:

	```
	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP match source-address any destination-address any application junos-icmp

	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP then permit
	```

Im Folgenden finden Sie einige Attribute, die Sie in Ihren Richtlinien definieren können:

* Quellenadressen
* Zieladressen
* Anwendungen
* Aktion (permit/deny/reject/count/log)

Da es sich um eine statusabhängige Operation handelt, ist es nicht erforderlich, Rückgabepakete zuzulassen (in diesem Fall antwortet das Echo).

Verwenden Sie die folgenden Befehle, um Datenverkehr zuzulassen, der an die Komponente vSRX übertragen werden soll:

Bei eigenständiger Lösung:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.0 host-inbound-traffic system-services all
```
Bei Hochverfügbarkeitslösung:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.0 host-inbound-traffic system-services all
```

Verwenden Sie den folgenden Befehl, um Protokolle wie z. B. OSPF (Open Shortest Path First) oder BGP zuzulassen:

Bei eigenständiger Lösung:
```
set security zones security-zone trust interfaces ge-0/0/0.0 host-inbound-traffic protocols all
```
Bei Hochverfügbarkeitslösung:
```
set security zones security-zone trust interfaces reth2.0 host-inbound-traffic protocols all
```

## Firewallfilter
Standardmäßig lässt die Komponente Juniper vSRX für IBM Cloud das Pingsignal, SSH (Secure Shell) und HTTPS zu und löscht den gesamten übrigen Datenverkehr, indem der Filter `PROTECT-IN` auf die Schnittstelle `lo` angewendet wird.

Führen Sie das folgende Verfahren aus, um eine neue statusunabhängige Firewall zu konfigurieren:

1. Erstellen Sie den Firewallfilter und die Laufzeit (der folgende Filter lässt nur ICMP (Internet Control Message Protocol) zu und löscht den gesamten übrigen Datenverkehr).
	```
	set firewall filter ALLOW-PING term ICMP from protocol icmp
	set firewall filter ALLOW-PING term ICMP then accept
	```

2. Wenden Sie die Filterregel auf die Schnittstelle an (mit dem folgenden Befehl wird der Filter auf den gesamten Datenverkehr des privaten Netzes angewendet).
	```
	set interfaces ge-0/0/0 unit 0 family inet filter input ALLOW-PING
	```
