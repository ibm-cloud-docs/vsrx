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

# Utilizzo del failover
{: #working-with-failover}

**NOTA:** questa sezione viene applicata solo se viene eseguito il provisioning dei tuoi dispositivi gateway Juniper vSRX nella modalità ad elevata disponibilità.

Questo argomento descrive come avviare il failover dal tuo dispositivo gateway primario a un dispositivo di backup, in modo che tutto il traffico del piano di dati e di controllo venga instradato tramite il dispositivo gateway secondario dopo il failover.

A tale scopo, attieniti alla seguente procedura:

1. Accedi al tuo dispositivo gateway vSRX primario.

2. Entra nella modalità della CLI eseguendo il comando `cli` quando richiesto dalla console. Una volta entrato nella modalità della CLI, la console visualizza il ruolo del nodo, `primary` o `secondary`.

	Assicurati di essere nel nodo primario (`primary`). Se non è così, esci e accedi all'altro dispositivo gateway vSRX della coppia.

2. Nel dispositivo gateway vSRX primario, esegui il comando:

	```
	show chassis cluster status
	```
	L'output dovrebbe essere simile al seguente:

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

	Assicurati che per entrambi i gruppi di ridondanza, sia impostato lo stesso nodo come `primary`. È possibile che nodi diversi siano impostati come ruolo `primary` in diversi gruppi di ridondanza.

3. Avvia il failover immettendo il seguente comando nel prompt della console:

	```
	request chassis cluster failover redundancy-group <redundancy group number> node <node number>
	```

	Seleziona il numero del nodo e del gruppo di ridondanza appropriato dall'output del comando nel passo due. Per eseguire il failover di entrambi i gruppi di ridondanza, esegui due volte il comando precedente, una per ogni gruppo.

4. Dopo il completamento del failover, verifica l'output della console. Dovrebbe essere ora elencato come `secondary`.

5. Accedi all'altro gateway vSRX della tua coppia. Entra nella modalità della CLI eseguendo nuovamente il comando `cli` e verifica quindi che l'output della console sia visualizzato come `primary`.

**NOTA:** quando entri nella modalità della CLI nel tuo dispositivo gateway Juniper vSRX, l'output sarà visualizzato come `primary` dalla prospettiva del piano di controllo. Controlla sempre l'output di `show chassis cluster status` per determinare quale dispositivo gateway è il primario dalla prospettiva del piano di dati. Fai riferimento alla [Configurazione predefinita di vSRX](/docs/infrastructure/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration) per ulteriori informazioni sui gruppi di ridondanza, nonché sui piani di dati e di controllo.
