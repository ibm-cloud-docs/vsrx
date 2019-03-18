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

# Ricaricamento e migrazione del sistema operativo (SO)
{: #reloading-an-migrating-the-os}

Il processo di ricaricamento del sistema operativo (SO) viene utilizzato per ricreare un server gateway. Il processo esegue le seguenti azioni:

* Ricarica il sistema operativo dell'host del server
* Installa KVM nel sistema operativo
* Crea una VM vSRX nel KVM
* Riconfigura il vSRX con la configurazione predefinita per IBM® Cloud

Il completamento del processo normalmente richiede 1 ora e 40 minuti. I gateway autonomi saranno fuori servizio durante questo periodo. Per i gateway ad elevata disponibilità (HA) Juniper, quando ricarichi il SO su uno dei tuoi server, vSRX eseguirà il failover su un altro server nel cluster e continuerà ad elaborare il traffico di dati. Una volta che il ricaricamento è stato completato, il server si riunirà al cluster.

**ATTENZIONE:** se stai già eseguendo un cluster HA vSRX Juniper, non eseguire un ricaricamento SO su entrambi i server del gateway HA contemporaneamente. In questo modo si distruggerà il cluster vSRX e comporterà che il gateway vada fuori servizio. Se il cluster vSRX viene distrutto, devi utilizzare l'opzione **Rebuild Cluster** (dettagliata di seguito) per rieseguire il provisioning del vSRX e ricreare il cluster HA.

## Esecuzione di un ricaricamento SO
Per ricaricare il SO per un server gateway, esegui la seguente procedura:

1. [Accedi alla schermata Gateway Appliances](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) nel portale del cliente e passa alla pagina dei dettagli del gateway selezionando il nome del gateway desiderato.

2. Fai clic sul nome del server nel pannello Hardware.
![Server Hardware](images/os_hardware.png)

3. Nella pagina del dispositivo, fai clic su **OS Reload** nel menu a discesa Action per accedere alla pagina Server Configuration.
![Dettagli dispositivo](images/os_device_page.png)

4. Nella pagina Server Configuration, puoi configurare e avviare il ricaricamento. Se stai eseguendo il ricaricamento da un SO diverso, fai clic su **Edit** accanto a **Operating System**, seleziona **Juniper** e seleziona quindi una delle opzioni Juniper vSRX 15.x Standard. Quando hai terminato di modificare le tue impostazioni, seleziona **Reload Above Configuration** per continuare.

5. Viene visualizzata la schermata dei dettagli del ricaricamento SO. Controlla le impostazioni che hai scelto e fai clic su **Edit Settings** se sono necessarie delle modifiche. In caso contrario, fai clic su **Next** per procedere.

6. Nella schermata di conferma del ricaricamento SO, accetta i termini del Master Service Agreement e quindi avvia il processo di ricaricamento SO facendo clic su **Confirm OS Reload**. Se non vuoi procedere con il ricaricamento, fai clic su **Cancel**.

## Migrazione da un server Vyatta/VRA a un Juniper vSRX utilizzando il ricaricamento SO
Se stai ricaricando un server Vyatta autonomo, allora sarà eseguito il provisioning di un Juniper vSRX autonomo una volta completato il ricaricamento SO. Saranno utilizzati gli stessi indirizzi IP del gateway e sarà reimpostata la password dell'utente root sul server host (nonché la password degli utenti root e amministratore nel vSRX).

Se stai ricaricando dei server Vyatta ad elevata disponibilità, devi eseguire un ricarimento del sistema operativo su entrambi i server hardware. Questo comando installa Ubuntu 16.04. Successivamente, utilizza l'opzione Rebuild Cluster (dettagliata nella seguente sezione) per eseguire il provisioning del vSRX e creare il cluster HA. Come con un vSRX autonomo, saranno utilizzati gli stessi indirizzi IP del gateway e sarà reimpostata la password dell'utente root sul server host (nonché la password degli utenti root e amministratore nel vSRX).

**ATTENZIONE:** non eseguire un ricaricamento SO su solo uno dei server del cluster HA Vyatta. L'utilizzo di due sistemi operativi diversi su un solo cluster HA gateway non è supportato.

## Ricreazione di un cluster vSRX HA
Per ricreare uno dei tuoi cluster vSRX HA, esegui la seguente procedura:

1. [Accedi alla schermata Gateway Appliances](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) nel portale del cliente e passa alla pagina dei dettagli del gateway selezionando il nome del gateway HA desiderato.

2. Fai clic su **Rebuild Cluster** nel pannello vSRX.
![Ricrea cluster](images/rebuild_cluster.png)

3. Leggi attentamente il messaggio di avvertenza. L'operazione per ricreare un cluster è distruttiva. Se desideri procedere, salva la tua configurazione vSRX prima di fare clic su **Rebuild** per avviare il processo.
![Conferma ricreazione cluster](images/rebuild_cluster_confirm.png)
