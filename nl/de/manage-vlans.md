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

# IBM VLANs verwalten
{: #managing-ibm-vlans}

Über die [Anzeige 'Details zu Gateway-Appliances'](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) können Sie eine Vielzahl von Aktionen ausführen.

## VLAN einer Gateway-Appliance zuordnen

VLANs müssen einer Gateway-Appliance zugeordnet werden, bevor für sie ein Routing ausgeführt werden kann. Die Zuordnung eines VLANs bedeutet, dass ein infrage kommendes VLAN mit einem Netzgateway verknüpft wird, damit eine Weiterleitung an eine Gateway-Appliance möglich ist. Durch diese Zuordnung wird das VLAN nicht automatisch an eine Gateway-Appliance weitergeleitet; das VLAN fährt fort, Front-End- und Back-End-Kundenrouter zu verwenden, bis eine Weiterleitung erfolgt.

VLANs können nur jeweils einem Gateway zugeordnet werden und dürfen keine Firewall aufweisen. Führen Sie das folgende Verfahren aus, um einem Netzgateway ein VLAN zuzuordnen.

1. [Rufen Sie die Anzeige 'Details zu Gateway-Appliances' auf](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details), die sich im Kundenportal befindet.
2. Wählen Sie die Registerkarte 'VLAN' aus.
3. Klicken Sie auf **VLAN zuordnen** und wählen Sie ein VLAN in der Dropdown-Liste aus.
4. Klicken Sie auf **Speichern** und bestätigen Sie Ihre Auswahl. Durch die Zuordnungsaktion für das VLAN wird das VLAN nicht durch die Firewall weitergeleitet.

Nach der Zuordnung eines VLANs zur Gateway-Appliance wird das VLAN im Abschnitt für zugeordnete VLANs der Anzeige 'Details zu Gateway-Appliances' angezeigt. In diesem Abschnitt kann das VLAN an das Gateway weitergeleitet werden oder die Zuordnung zum Gateway kann aufgehoben werden. Weitere infrage kommende VLANs können einer Gateway-Appliance jederzeit zugeordnet werden, indem die oben genannten Schritte wiederholt werden.

## Zugeordnetes VLAN weiterleiten

Zugeordnete VLANs sind mit einer Gateway-Appliance verknüpft, jedoch trifft ein- und ausgehender Datenverkehr des VLANs das Gateway erst dann, wenn das VLAN weitergeleitet wurde. Wenn ein zugeordnetes VLAN weitergeleitet wurde, wird der gesamte Front-End- und Back-End-Datenverkehr nicht mehr über die Kundenrouter, sondern über die Gateway-Appliance weitergeleitet.

Führen Sie das folgende Verfahren aus, um ein zugeordnetes VLAN weiterzuleiten:

1. [Rufen Sie die Anzeige 'Details zu Gateway-Appliances' auf](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details), die sich im Kundenportal befindet.
2. Wählen Sie die Registerkarte 'VLAN' aus.
3. Wählen Sie mindestens ein gewünschtes VLAN aus, indem Sie das Kontrollkästchen auswählen.
4. Klicken Sie auf **Weiterleiten über** und bestätigen Sie Ihre Auswahl.

Nach der Weiterleitung eines VLANs wird der gesamte Front-End- und Back-End-Datenverkehr aus den Kundenroutern in das Netzgateway verschoben. Zusätzliche Kontrollmechanismen für den Datenverkehr und die Gateway-Appliance selbst können über den Zugriff auf das Verwaltungstool des Gateways eingerichtet werden. Das Routing über das Netzgateway kann jederzeit durch [Umgehen der Gateway-Appliance](#bypass-gateway-appliance-routing-for-a-vlan) beendet werden.

## Gateway-Appliance-Weiterleitung für ein VLAN umgehen

Wenn ein VLAN weitergeleitet wurde, wird der gesamte Front-End- und Back-End-Datenverkehr über das Netzgateway geführt. Die Gateway-Appliance kann jederzeit umgangen werden, sodass der Datenverkehr an die Front-End- und Back-End-Kundenrouter (FCR und BCR) zurückkehrt.

Bei Umgehen eines VLANs bleibt das VLAN weiterhin dem Netzgateway zugeordnet. Soll die Zuordnung des VLANs zur Gateway-Appliance aufgehoben werden, erfahren Sie in [Zuordnung zwischen VLAN und Gateway-Appliance aufheben](#disassociate-a-vlan-from-a-gateway-appliance) mehr zu der entsprechenden Vorgehensweise.

Führen Sie das folgende Verfahren aus, um das Gateway-Routing für ein VLAN zu umgehen:

1. [Rufen Sie die Anzeige 'Details zu Gateway-Appliances' auf](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details), die sich im Kundenportal befindet.
2. Wählen Sie die Registerkarte 'VLAN' aus.
3. Wählen Sie mindestens ein gewünschtes VLAN aus, indem Sie das Kontrollkästchen auswählen.
4. Klicken Sie auf **Umgehen** und bestätigen Sie Ihre Auswahl.

Durch Umgehen des Netzgateways wird der gesamte Front-End- und Back-End-Datenverkehr über die FCR und BCR weitergeleitet, die dem VLAN zugeordnet sind. Das VLAN bleibt der Gateway-Appliance zugeordnet und seine Weiterleitung kann jederzeit wieder über die Gateway-Appliance erfolgen.

## Zuordnung zwischen VLAN und Gateway-Appliance aufheben

VLANs können über eine [Zuordnung](#associate-a-vlan-to-a-gateway-appliance) mit jeweils einer Gateway-Appliance verknüpft sein. Durch die Zuordnung kann das VLAN jederzeit an die Gateway-Appliance weitergeleitet werden. Wenn ein VLAN einer anderen Gateway-Appliance zugeordnet werden soll oder wenn das VLAN nicht mehr dem zugehörigen Gateway zugeordnet sein soll, ist es erforderlich, die Zuordnung aufzuheben. Durch die Aufhebung der Zuordnung wird die 'Verknüpfung' zwischen VLAN und Gateway-Appliance entfernt, wodurch es möglich wird, dass das VLAN, falls erforderlich, einem anderen Gateway zugeordnet wird.

Führen Sie das folgende Verfahren aus, um die Zuordnung eines VLANs zu einer Gateway-Appliance aufzuheben:

1. [Rufen Sie die Anzeige 'Details zu Gateway-Appliances' auf](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details), die sich im Kundenportal befindet.
2. Wählen Sie die Registerkarte 'VLAN' aus.
3. Wählen Sie mindestens ein gewünschtes VLAN aus, indem Sie das Kontrollkästchen auswählen.
4. Klicken Sie auf **Zuordnung aufheben** und bestätigen Sie Ihre Auswahl.

Nach der Aufhebung der Zuordnung zwischen VLAN und Gateway-Appliance kann das VLAN einem anderen Gateway zugeordnet werden. Das VLAN kann jederzeit auch wieder derselben Gateway-Appliance zugeordnet werden. Nach der Aufhebung der Zuordnung zwischen VLAN und Gateway-Appliance kann der Datenverkehr des VLANs nicht mehr über das Gateway weitergeleitet werden. VLANs müssen einer Gateway-Appliance zugeordnet sein, bevor sie an diese weitergeleitet werden können.

## Mehrere VLANs über dieselbe Netzschnittstelle weiterleiten
Der Betrieb der Komponente Juniper vSRX kann mit mehreren VLANs über dieselbe Netzschnittstelle erfolgen. Sie kann auch gleichzeitig Datenverkehr handhaben, der mit Tags versehen ist bzw. keine Tags aufweist. Dies wird auf der eigenständigen Einheit erreicht, indem als Schnittstellenkapselung `flexible-vlan-tagging` eingestellt wird; auf Einheiten mit Hochverfügbarkeit werden 'reth2' und 'reth3' als mit Tags versehene Schnittstellen verwendet. Dies wird im Rahmen der Standardkonfiguration ausgeführt und muss nicht geändert werden.  In den eigenständigen Einheiten ist Einheit 0 die nicht mit Tags versehene Unterschnittstelle; andere Einheiten, die ungleich null sind, sind mit Tags versehen.

Konfigurieren Sie mithilfe der folgenden Befehlsgruppe weitere mit Tags versehene Schnittstellen:

Bei eigenständiger Lösung:
```
set interfaces ge-0/0/0 unit 50 vlan-id 50
set interfaces ge-0/0/0 unit 50 family inet address <IP/MASKE>
```

Bei Hochverfügbarkeitslösung:
```
set interfaces reth2 unit 50 vlan-id 50
set interfaces reth2 unit 50 family inet address <IP/MASKE>
```

**Anmerkung:** Auch wenn Einheit 0 nicht mit Tags versehen ist, wird sie von `JunOS` benötigt, um auf die VLAN-ID zu verweisen, die als `native-vlan` konfiguriert wurde. Da `native-vlan-id` im Beispiel den Wert `10` aufweist, sollte Einheit 0 für die `vlan-id` auch den Wert `10` aufweisen. Auf diese Weise wird `JunOS` darüber benachrichtigt, dass Einheit 0 nicht mit Tags versehen sein darf.

## Beispiel einer VLAN-Konfiguration für vSRX

Unten finden Sie eine Beispielkonfiguration für vSRX, in der zwei private Schnittstellen und eine Kundenzone definiert sind.
Mithilfe dieser Beispielkonfiguration können 'Private VLAN1' und 'Private VLAN2' miteinander kommunizieren. Eigenständige vSRX-Schnittstellen sind als 'ge-0/0/0' (privat) und 'ge-0/0/1' (öffentlich) definiert; für eine Hochverfügbarkeitsinstanz sind sie als 'reth2' (privat mit Hochverfügbarkeit) und 'reth3' (öffentlich mit Hochverfügbarkeit) definiert.

<img src="images/Sample-Topology-VLAN-to-VLAN.png" alt="Zeichnung" style="width: 500px;"/>

```
# show interfaces

ge-0/0/0 {
   description PRIVATE_VLANs;
   flexible-vlan-tagging;
   native-vlan-id 1121;
   unit 0 {
       vlan-id 1121;
       family inet {
           address 10.184.108.158/26;
       }
   }
   unit 10 {
       vlan-id 1811;
       family inet {
           address 10.184.237.201/29;
       }
   }
   unit 20 {
       vlan-id 1812;
       family inet {
           address 10.185.48.9/29;
       }
   }
}


# show security zones security-zone CUSTOMER-PRIVATE
interfaces {
   ge-0/0/0.10 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
   ge-0/0/0.20 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
}
# show security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PRIVATE
policy Allow_C_C {
   match {
       source-address any;
       destination-address any;
       application any;
   }
   then {
       permit;
   }
}
```
