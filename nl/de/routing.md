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

# Mit Routing arbeiten
Die Komponente Juniper vSRX für IBM® Cloud basiert auf `JunOS`, wodurch Sie Zugriff auf den vollständigen Routing-Stack von Juniper haben.

##Statisches Routing
Führen Sie die folgenden Befehle aus, um statische Routen zu konfigurieren:

###Standardroute festlegen
```
set routing-options static route 0/0 next-hop <Gateway-IP>
```

### Statische Route erstellen
```
set routing-options static route <PRÄFIX/MASKE> next-hop <Gateway-IP>
```  

###OSPF-Basisrouting
Führen Sie zum Einrichten des OSPF-Basisroutings (OSPF – Open Shortest Path First), das nur Bereich 0 verwendet, folgende Befehle aus und verwenden Sie dabei die md5-Authentifizierung:

```
set protocols ospf area 0 interface ge-0/0/1.0 authentication md5 0 key <SCHLÜSSEL>
```

### BGP-Basisrouting
Definieren Sie zum Einrichten des BGP-Basisroutings (BGP – Border Gateway Protocol) zunächst das lokale autonome System (AS):

```
set routing-options autonomous-system 65001
```

Konfigurieren Sie anschließend den BGP-Nachbarn und seine Sitzungsattribute:

```
set protocols bgp group CUSTOMER local-address 1.1.1.1
set protocols bgp group CUSTOMER family inet unicast
set protocols bgp group CUSTOMER family inet6 unicast
set protocols bgp group CUSTOMER peer-as 65002
set protocols bgp group CUSTOMER neighbor 2.2.2.2
```

In diesem Beispiel wurde BGP für Folgendes konfiguriert:

* Damit die Quellen-IP-Adresse `1.1.1.1` zum Erstellen der Sitzung verwendet wird
* Damit sowohl die Internet Protocol Version 4-Unicast-Familie als auch die Internet Protocol Version 6-Unicast-Familie verhandelt wird
* Damit mit einem Nachbarn gleichgeordnet wird, der zu `AS 65002` gehört
* Peer-Nachbar-IP `2.2.2.2`

Zusätzliche Konfigurationen finden Sie [hier](https://www.juniper.net/documentation/en_US/junos11.4/information-products/topic-collections/config-guide-routing/config-guide-routing.pdf).
