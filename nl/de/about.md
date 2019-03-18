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

# Informationen zu Juniper vSRX für IBM Cloud 
{: #about-ibm-cloud-juniper-vsrx}

Mit Juniper vSRX für IBM® Cloud ist das ausgewählte Routing von privatem und öffentlichem Netzverkehr über eine auf Unternehmensebene installierte und voll ausgestattete Firewall möglich, die auf Software-Features von JunOS basiert, wie beispielsweise vollständige Routing-Stacks, gemeinsame Nutzung von QoS und Datenverkehr, richtlinienbasiertes Routing und VPN. Die Komponente vSRX bietet Leistungs- und Wartungsvorteile sowie eine einfache Durchführbarkeit der Konfiguration, dennoch kann sie einfach auf einem Bare-Metal-Server ausgeführt werden. Die Hardware hat eine angepasste Größe, um die für das Routing und die Sicherheit erforderliche Arbeitslast mehrerer VLANs zu handhaben, und sie kann mit redundanten Netzlinks und redundanten RAID-Arrays bestellt werden. Alle vSRX-Funktionen werden vom Kunden verwaltet.

Die Komponente vSRX für IBM Cloud wird in zwei unterschiedlichen Modi angeboten: als eigenständige Lösung oder als Hochverfügbarkeitscluster (HA-Cluster).

**Anmerkung:** Weitere Dokumentation zur Komponente Juniper vSRX für IBM Cloud finden Sie im Abschnitt [Ergänzende Dokumentation](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation).

## Firewall
Mit einer Bereitstellung der Komponente vSRX schützen Sie Ihre Umgebung vor externen und internen Bedrohungen, da sowohl der private als auch der öffentliche Datenverkehr gefiltert wird. Kunden können die Komponente vSRX selbst verwalten, indem Sie Richtlinien und Regeln definieren, mit denen ein- oder ausgehender Netzverkehr zugelassen bzw. (neben anderen Aktionen) abgelehnt wird, wodurch die betroffenen Anwendungen gegen interne und externe Benutzer geschützt sind. Sowohl IPv4- als auch IPv6-Stacks werden statusabhängig unterstützt.

## Virtual Private Network-Gateway (VPN)
Verbinden Sie Ihr Rechenzentrum oder Ihre Niederlassung vor Ort mithilfe der VPN-Tunnelung mit IBM Cloud, indem Sie Ihre vSRX-Komponente als Netz-Gateway-Einheit bereitstellen. Für die sichere Kommunikation zwischen Ihrem Unternehmensrechenzentrum oder Ihrer Niederlassung und Ihrem IBM Cloud-Netz können Sie einen standortverbindenden IPsec-VPN-Tunnel (IPsec – Internet Protocol Security) verwenden. Auch der Fernzugriff über IPsec-VPN wird unterstützt.

Sie finden ein detailliertes Konfigurationshandbuch zu VPN über die Links im Abschnitt [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn).

## Netzadressumsetzung (NAT – Network Address Translation)
Mithilfe der Gateway-Appliance vSRX können Sie Anwendungs- und Datenbankserver ohne Schnittstellen zum öffentlichen Netz bereitstellen, während Sie Ihren Servern über die quellenseitige Netzadressumsetzung weiterhin den Zugriff auf das Internet ermöglichen. Für eine verbesserte Sicherheit können Sie Ihre Server über die zielseitige Netzadressumsetzung auch hinter der Gateway-Einheit verbergen.

## Auf Unternehmen abgestimmtes Routing
Mithilfe der Komponente vSRX ist es Ihnen bei mehrschichtigen Anwendungen in unterschiedlichen isolierten Netzen möglich, Verbindungen zwischen diesen Netzen mit einer größeren Flexibilität als bisher zu erstellen. Mithilfe von Border Gateway Protocol (BGP) können Sie das dynamische Routing einrichten; dadurch ist es Ihnen möglich, den IBM Cloud-Routern gegenüber einen eigenen IP-Bereich anzukündigen. BGP bietet außerdem eine größere Flexibilität für angepasste Konfigurationen privater Netze, wenn Tunnellösungen und Lösungen mit direkten Verbindungen kombiniert verwendet werden.

## VLAN-Konzepte und die Rolle der Gateway-Appliance
Ein VLAN (virtuelles LAN) ist ein Mechanismus, mit dem ein physisches Netz in viele virtuelle Segmente aufgliedert wird. Für mehr Komfort kann der Datenverkehr mehrerer ausgewählter VLANs über ein einziges Netzkabel übermittelt werden; dieser Prozess wird allgemein als 'Trunking' bezeichnet.

Die Komponente vSRX wird in zwei unterschiedlichen Schnittstellen verwaltet: in einem Paar aus vSRX-Server(n) und Gateway-Einheit. Die Gateway-Appliance bietet eine Schnittstelle (grafische Benutzerschnittstelle und Anwendungsprogrammierschnittstelle) zum Auswählen der VLANs, die Sie der Komponente vSRX zuordnen wollen. Durch Zuordnen eines VLANs zu einer Gateway-Appliance wird dieses VLAN zusammen mit allen seinen Teilnetzen an Ihre vSRX-Komponente umgeleitet (der Vorgang des 'Trunking'); dadurch erhalten Sie die Steuerung über Filterung, Weiterleitung und Zugriffsschutz. Auf Server in einem zugeordneten VLAN kann von anderen VLANs aus nur über Ihre vSRX-Komponente zugegriffen werden; es ist nicht möglich, die Komponente vSRX zu umgehen, es sei denn, Sie übergehen das VLAN oder heben seine Zuordnung auf.

Standardmäßig sind einer neuen Gateway-Appliance zwei nicht entfernbare 'Durchgangs'-VLANs (Transit-VLANs) zugeordnet, je eine für Ihr öffentliches (_public_) und Ihr privates (_private_) Netz. Diese Netze werden in der Regel für die Verwaltung verwendet und sie können mithilfe von vSRX-Befehlen separat geschützt werden.

Die Komponente vSRX kann nur VLANs verwalten, die ihr über die Gateway-Appliance zugeordnet wurden.

Informationen zur Verwaltung von VLANs über die Anzeige **Details zu Gateway-Appliances** finden Sie im Abschnitt [VLANs verwalten](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans).
