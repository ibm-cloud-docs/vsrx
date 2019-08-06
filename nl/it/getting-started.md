---

copyright:
  years: 2018
lastupdated: "2019-05-03"

keywords: vsrx, ordering, gateway, appliance

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

# Introduzione a {{site.data.keyword.vsrx_full}} Gateway
{: #getting-started}

Per iniziare ad utilizzare {{site.data.keyword.vsrx_full}} Gateway, determina prima se il tuo account è collegato a IBM Cloud.

Per scoprire se hai un account collegato, passa al [Portale del cliente ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/){: new_window} nel tuo browser e accedi. Se il tuo account è collegato, non vedrai un pulsante **Ulteriori informazioni su Bluemix** in alto a destra.

## Procedura per l'ordine
{: #steps-for-ordering}

Puoi ordinare la tua applicazione gateway, utilizzando uno di questi metodi:

Per un elenco delle limitazioni note con {{site.data.keyword.vsrx_full}} Gateway, fai riferimento all'[argomento Limitazioni note](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx).
{: note}

### Fare un ordine con un account collegato
{: #ordering-with-a-linked-account}

Se il tuo account è collegato, segui questa procedura:

1. Dal tuo browser, apri la pagina Gateway Appliances nel [Catalogo Cloud ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/gen1/infrastructure/provision/gateway){: new_window} e accedi al tuo account.

  Puoi anche ottenere questa pagina eseguendo l'accesso alla [Console IU di IBM Cloud ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com) e selezionando **Infrastruttura classica > Rete > Applicazione gateway**.
In alternativa, dal [Catalogo IBM ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/catalog), seleziona la categoria **Rete** e scegli quindi il tile **Applicazione gateway**.

2. Scegli **Juniper vSRX (fino a 1 Gbps)** o **Juniper vSRX (fino a 10 Gbps)** in **Fornitore del gateway**.

3. Dalla sezione **Applicazione gateway**, immetti le tue informazioni relative a **Nome host** e nome **Dominio**. Questi campi saranno precompilati con le informazioni predefinite, quindi assicurati che i valori siano corretti.

	<img src="images/linked_order.png" alt="disegno" style="width: 700px;"/>

4. Seleziona l'opzione **Alta disponibilità**, se la desideri, e seleziona quindi l'**Ubicazione** del data center desiderata e il **Pod** specifico che desideri dal menu a discesa.

  Verranno qui visualizzati solo i pod che già hanno una VLAN associata. Se desideri eseguire il provisioning dell'Applicazione gateway in un pod che non vedi elencato, creare prima una VLAN lì
  {: note}

	<img src="images/linked_server.png" alt="disegno" style="width: 600px;"/>

4. Dalla sezione **Configurazione**, scegli il tuo processore selezionando le tue chiavi SSH e RAM (se vuoi farne uso per autenticare l'accesso al tuo nuovo gateway).

  Il processore appropriato viene scelto per te in base alla versione di licenza che hai selezionato nel passo due. Puoi tuttavia scegliere delle configurazioni RAM differenti.
  {: note}

5. Dalla sezione **Dischi di archiviazione**, scegli le opzioni che soddisfano i tuoi requisiti di archiviazione.

  Sono disponibili le opzioni RAID0 e RAID1 per una protezione aggiunta contro la perdita di dati poiché sono delle "riserve a caldo" (componenti di backup che possono essere attivati immediatamente quando si verifica il malfunzionamento di un componente primario).
  {: note}

  Puoi avere fino a quattro dischi per ogni vSRX. La "dimensione del disco" con una configurazione RAID è la dimensione del disco utilizzabile, in quanto delle configurazioni RAID viene eseguito il mirroring.
  {: note}

  Riserva più spazio rispetto alle impostazioni predefinite del disco se pensi di eseguire le diagnostiche di rete che generano i log dettagliati.
  {: tip}

6. Dalla sezione **Interfaccia di rete**, seleziona le tue **Velocità porta di uplink**. La selezione predefinita è una singola interfaccia ma ci sono anche opzioni ridondanti e solo private. Scegli quella che meglio si adatta alle tue esigenze.

  La sezione **Moduli aggiuntivi** dell'interfaccia di rete ti consente di selezionare un indirizzo IPv6 se necessario e ti mostra le eventuali opzioni predefinite incluse aggiuntive.

8. Esamina le tue selezioni, controlla di aver letto gli accordi di servizio di terze parti e fai quindi clic su **Crea**. L'ordine viene verificato automaticamente.

Dopo che il tuo ordine è stato approvato, il provisioning del tuo {{site.data.keyword.vsrx_full}} Gateway viene avviato automaticamente. Quando il processo di provisioning viene completato, il nuovo vSRX comparirà nella pagina di elenco Gateway Appliances. Fai clic sul nome del gateway per aprire la pagina Gateway Details. Troverai gli indirizzi IP, la password e il nome di accesso del dispositivo.  

Ricordati che, dopo aver ordinato e configurato il tuo gateway dal catalogo IBM Cloud, devi anche configurare il dispositivo stesso con le stesse impostazioni.
{: tip}

### Fare un ordine con un account non collegato
{: #ordering-with-a-unlinked-account}

Se il tuo account non è collegato, segui questa procedura:

1.	Apri il [Portale del cliente ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/){: new_window} e accedi al tuo account.
2.	Nella navigazione del portale del cliente, seleziona **Network > Gateway Appliances**.
3.	Dall'elenco **Gateway Appliances**, fai clic su **Order Gateway**.
4.	Dalla pagina **Order**, seleziona il tuo data center desiderato dal menu a discesa, quindi scegli il tipo desiderato di hardware server su cui sarà eseguito il provisioning di Juniper vSRX.

	Se pensi di utilizzare un Dual Processor Multi-Core Server, devi selezionare **Intel Xeon 5120** come tipo di server.
  {: note}

5.	Nella pagina **Order**, seleziona l'opzione **High Availability Pair** se desiderato, quindi seleziona la dimensione di **Memory**.
6. 	Fai quindi clic sulla scheda **Juniper** in **Operating System**, seleziona **Juniper vSRX (up to 1 Gbps) Standard** per un server con un singolo processore oppure **Juniper vSRX (up to 10 Gbps) Standard** per un server con due processori.
7. 	Infine, seleziona la velocità di uplink di rete desiderata.
8.	Controlla le tue selezioni, quindi fai clic su **Add to Order**. Il tuo ordine sarà verificato automaticamente.
9.	Nella pagina **Checkout**, se gestisci già delle VLAN nel data center selezionato, seleziona le VLAN di backend che vuoi proteggere. Assicurati di:
	* Fornisci un nome host e un nome dominio per il tuo server
	* Seleziona una chiave SSH per l'autenticazione dell'accesso, se lo desideri.
	* Spunta tutte le caselle per i termini del servizio IBM Cloud e per i termini del software di terze parti.
10. Fai clic su **Submit Order**.

## Operazioni successive
{: #what-s-next-}

Dopo l'approvazione del tuo ordine, il provisioning del tuo vSRX si avvia automaticamente. Quando il processo di provisioning viene completato, il gateway verrà visualizzato nell'elenco **Gateway Appliances**.

Fai clic sul nome del gateway per aprire la pagina **Gateway Details**. Troverai gli indirizzi IP, il nome utente di accesso e le password del dispositivo.

<img src="images/after_order.png" alt="disegno" style="width: 700px;"/>
