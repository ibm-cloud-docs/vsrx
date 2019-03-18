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

# Mit Failover arbeiten
{: #working-with-failover}

**Anmerkung:** Dieser Abschnitt ist nur zutreffend, wenn Ihre Juniper vSRX-Gateway-Einheiten im Hochverfügbarkeitsmodus bereitgestellt wurden.

In diesem Abschnitt wird beschrieben, wie ein Failover von Ihrer Gateway-Einheit auf eine Backup-Einheit eingeleitet wird, sodass nach dem Failover der gesamte Datenverkehr auf Steuer- und Datenebene über die sekundäre Gateway-Einheit geleitet wird.

Führen Sie dazu das folgende Verfahren aus:

1. Melden Sie sich an Ihrer primären vSRX-Gateway-Einheit an.

2. Rufen Sie den CLI-Modus auf, indem Sie in der Konsoleneingabeaufforderung den Befehl `cli` eingeben. Wenn Sie den CLI-Modus aufgerufen haben, zeigt die Konsole die Rolle des Knotens an, entweder 'primär' (`primary`) oder 'sekundär' (`secondary`).

	Stellen Sie sicher, dass Sie sich im primären Knoten (`primary`) befinden. Ist dies nicht der Fall, müssen Sie die Eingabe verlassen und sich bei der anderen vSRX-Gateway-Einheit des Paars anmelden.

2. Führen Sie in der primären vSRX-Gateway-Einheit folgenden Befehl aus:

	```
	show chassis cluster status
	```
	Die Ausgabe sollte der folgenden ähneln:

	```
	Monitor Failure codes:
		CS  Cold Sync monitoring        FL  Fabric Connection monitoring
		GR  GRES monitoring             HW  Hardware monitoring
		IF  Interface monitoring        IP  IP monitoring
		LB  Loopback monitoring         MB  Mbuf monitoring
		NH  Nexthop monitoring          NP  NPC monitoring
		SP  SPU monitoring              SM  Schedule monitoring
		CF  Config Sync monitoring

	Cluster ID: 2
	Node   Priority Status         Preempt Manual   	Monitor-failures

	Redundancy group: 0 , Failover count: 1
	node0  100      primary        no      no       None
	node1  1        secondary      no      no       None
	Redundancy group: 1 , Failover count: 1
	node0  100      primary        yes     no       None
	node1  1        secondary      yes     no       None

	{primary:node0}
	```

	Stellen Sie sicher, dass für beide Redundanzgruppen derselbe Knoten als primärer Knoten festgelegt ist (`primary`). In unterschiedlichen Redundanzgruppen können unterschiedliche Knoten als primäre Knoten (`primary`) festgelegt werden.

3. Leiten Sie das Failover ein, indem Sie in der Konsoleneingabeaufforderung folgenden Befehl eingeben:

	```
	request chassis cluster failover redundancy-group <Nummer der Redundanzgruppe> node <Knotennummer>
	```

	Wählen Sie in der Ausgabe des Befehls in Schritt zwei die entsprechende Redundanzgruppennummer und Knotennummer aus. Wenn ein Failover für beide Redundanzgruppen ausgeführt werden soll, müssen Sie den oben stehenden Befehl zweimal, d. h. einmal für jede Gruppe, ausführen.

4. Nachdem das Failover abgeschlossen ist, müssen Sie die Konsolenausgabe überprüfen. Dort sollte nun `secondary` (sekundär) aufgelistet sein.

5. Melden Sie sich an dem anderen vSRX-Gateway Ihres Paars an. Rufen Sie erneut den CLI-Modus auf, indem Sie den Befehl `cli` ausführen; überprüfen Sie anschließend, dass in der Konsolenausgabe 'primär' (`primary`) angezeigt wird.

**Anmerkung:** Wenn Sie den CLI-Modus in Ihrer Juniper vSRX-Gateway-Einheit aufrufen, wird die Ausgabe in der Steuerebenenperspektive als 'primär' (`primary`) angezeigt. Überprüfen Sie stets die Ausgabe für `show chassis cluster status`, um zu ermitteln, welche Gateway-Einheit in der Datenebenenperspektive primär ist. Lesen Sie den Abschnitt zur [vSRX-Standardkonfiguration](/docs/infrastructure/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration), um mehr über Redundanzgruppen sowie über Steuer- und Datenebenen zu erfahren.
