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

# SSH und Pingbefehl an öffentliches Teilnetz zulassen
{: #allowing-ssh-and-pinging-to-a-public-subnet}

In diesem Leitfaden erfahren Sie, wie die Komponente Juniper vSRX Standard für IBM® Cloud mit einer neuen Schnittstelle, neuen Zone und einem Adressbuch konfiguriert wird. Da die Standardaktion für jeglichen Datenverkehr 'drop' ist (löschen), wird in diesem Leitfaden gezeigt, wie Datenflüsse eingerichtet werden, die a) innerhalb der neuen Zone jeglichen Datenverkehr zulassen, b) die jeglichen Datenverkehr aus der neuen Zone an das Internet zulassen und c) die nur SSH und Ping vom Internet an ein Teilnetz im neuen VLAN zulassen.

In diesem Beispiel werden folgende Werte verwendet.
```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

**Anmerkung:** Diese Schritt-für-Schritt-Anleitung setzt voraus, dass eine Hochverfügbarkeitslösung der vSRX-Komponente bereitgestellt wurde, die ein einzelnes öffentliches VLAN und ein Teilnetz aufweist.

## Ergebnis

In dieser Schritt-für-Schritt-Anleitung erlernen Sie, wie der Service konfiguriert wird:

Task  | Beschreibung
------------- | -------------
[Neue Schnittstelle, neue Zone und Adressbuch für Teilnetz erstellen](/docs/infrastructure/vsrx?topic=vsrx-creating-the-new-interface-zone-and-address-book-subnet) | Mit Tags versehene Schnittstelleneinheit und Sicherheitszone für das neue VLAN erstellen.
[Neue Datenflüsse erstellen](/docs/infrastructure/vsrx?topic=vsrx-creating-your-new-traffic-flows) | Neue Datenflüsse erstellen, um eingehende Pingbefehle und SSH zuzulassen.
[Ausgabe bestätigen und Änderungen festschreiben](/docs/infrastructure/vsrx?topic=vsrx-confirming-the-output-and-commiting-the-changes) | Ausgabe überprüfen, um zu bestätigen, was für die aktive Konfiguration festgeschrieben wird.
