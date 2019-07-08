---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: reloading, os, upgrading, kvm, ha, standalone

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Ricaricamento del sistema operativo
{: #reloading-the-os}

Il processo di ricaricamento del sistema operativo viene utilizzato per ricreare un server del gateway. Il processo esegue le seguenti azioni:

* Ricarica il sistema operativo dell'host del server
* Installa KVM nel sistema operativo
* Crea una VM vSRX nel KVM
* Riconfigura il vSRX con la configurazione predefinita per IBM® Cloud

Il completamento del processo normalmente richiede 1 ora e 40 minuti. I gateway autonomi saranno fuori servizio durante questo periodo. Per i gateway ad elevata disponibilità (HA) Juniper, quando ricarichi il SO su uno dei tuoi server, vSRX eseguirà il failover su un altro server nel cluster e continuerà ad elaborare il traffico di dati. Una volta che il ricaricamento è stato completato, il server si riunirà al cluster.

Per un ricaricamento o una ricreazione del cluster corretti su un vSRX HA:

* La password root per il gateway vSRX di cui è stato eseguito il provisioning deve corrispondere alla password root definita nel portale vSRX. La password nel portale è stata definita quando è stato eseguito il provisioning iniziale del gateway e potrebbe non corrispondere alla password del gateway corrente. Se la password è stata modificata dopo il provisioning iniziale, utilizza SSH per connetterti al gateway vSRX e modificare la password root in modo che corrisponda. Una volta eseguita l'operazione sulle password, puoi procedere con l'operazione di ricaricamento del sistema operativo o di ricreazione del cluster.

  <img src="images/gw-vsrx-password.png" alt="disegno" style="width: 700px;"/>

* **NON** eseguire un ricaricamento del sistema operativo su entrambi i server del gateway ad alta disponibilità (HA, Highly Available) contemporaneamente.

L'esecuzione di un ricaricamento del sistema operativo su entrambi i server del gateway HA contemporaneamente distruggerà il cluster vSRX e metterà il gateway fuori uso. Se il cluster vSRX viene distrutto, devi utilizzare l'opzione **Rebuild Cluster** (dettagliata di seguito) per rieseguire il provisioning del vSRX e ricreare il cluster HA.
{: important}

## Esecuzione di un ricaricamento SO
{: #performing-an-os-reload}

Per ricaricare il SO per un server gateway, esegui la seguente procedura:

1. [Accedi alla schermata Gateway Appliances](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) nel portale del cliente e passa alla pagina dei dettagli del gateway selezionando il nome del gateway desiderato.

  <img src="images/gw-sa-details.png" alt="disegno" style="width: 700px;"/>

2. Fai clic sul nome del server nel pannello Hardware.

  ![Server hardware](images/os_hardware.png)

3. Nella pagina del dispositivo, fai clic su **OS Reload** nel menu a discesa Action per accedere alla pagina Server Configuration.

  ![Dettagli del dispositivo](images/os_device_page.png)

4. Nella pagina Server Configuration, puoi configurare e avviare il ricaricamento. Se stai eseguendo il ricaricamento da un SO diverso, fai clic su **Edit** accanto a **Operating System**, seleziona **Juniper** e seleziona quindi una delle opzioni Juniper vSRX 15.x Standard. Quando hai terminato di modificare le tue impostazioni, seleziona **Reload Above Configuration** per continuare.

5. Viene visualizzata la schermata dei dettagli del ricaricamento SO. Controlla le impostazioni che hai scelto e fai clic su **Edit Settings** se sono necessarie delle modifiche. In caso contrario, fai clic su **Next** per procedere.

6. Nella schermata di conferma del ricaricamento SO, accetta i termini del Master Service Agreement e quindi avvia il processo di ricaricamento SO facendo clic su **Confirm OS Reload**. Se non vuoi procedere con il ricaricamento, fai clic su **Cancel**.

## Ricreazione di un cluster vSRX HA
{: #rebuilding-an-ha-vsrx-cluster}

Per ricreare uno dei tuoi cluster vSRX HA, esegui la seguente procedura:

1. [Accedi alla schermata Gateway Appliances](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) nel portale del cliente e passa alla pagina dei dettagli del gateway selezionando il nome del gateway HA desiderato.

2. Fai clic sull'elenco a discesa **Actions** e seleziona **Rebuild Cluster**.

3. Leggi attentamente il messaggio di avvertenza. L'operazione per ricreare un cluster è distruttiva. Se desideri procedere, salva la tua configurazione vSRX prima di fare clic su **Rebuild** per avviare il processo.

  ![Conferma ricreazione del cluster](images/rebuild_cluster_confirm.png)
