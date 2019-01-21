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

# Neue Schnittstelle, neue Zone und das Adressbuch für Teilnetz erstellen
Zuerst müssen Sie eine Schnittstelleneinheit für das VLAN erstellen und die Gateway-Adresse des Teilnetzes hinzufügen. Anschließend können Sie eine der neuen Einheit zugeordnete Sicherheitszone und den Eintrag `address-book` für das Teilnetz erstellen.  

**Anmerkung:** Blättern Sie nach rechts, um den gesamten Befehl anzuzeigen.

```
set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29
```
