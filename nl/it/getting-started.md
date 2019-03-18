---

copyright:
  years: 2018
lastupdated: "2018-11-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Introduzione a IBM Cloud Juniper vSRX Gateway
{: #getting-started-with-ibm-cloud-juniper-vsrx-gateway}

Per iniziare ad utilizzare IBM® Cloud Juniper vSRX Gateway, determina prima se il tuo account è collegato a IBM Cloud.

## Prima di cominciare

Per scoprire se hai un account collegato, passa al [Portale del cliente ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/){: new_window} nel tuo browser e accedi. Se il tuo account non è collegato, visualizzerai il pulsante **Learn more about Bluemix!** in alto a destra.

## Procedura per l'ordine

Puoi ordinare la tua applicazione gateway, utilizzando uno di questi metodi:

Per un elenco delle limitazioni note con IBM Cloud Juniper vSRX Gateway, fai riferimento all'[argomento Limitazioni note](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx).
{:note}

### Fare un ordine con un account collegato
Se il tuo account è collegato, segui questa procedura:

1.	Apri l'[IBM Cloud Console![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.bluemix.net/){: new_window} e accedi al tuo account.
2.	Nella navigazione di sinistra, seleziona **Infrastructure > Network > Gateway Appliances**.
3.	Dall'elenco **Gateway Appliances**, fai clic su **Create a Gateway**.
4. Dalla pagina **Order**, scegli un'**Hostname** e un **Domain**.
5. Seleziona l'opzione **High Availability Pair**, se desiderato.

	<img src="images/linked_order.png" alt="disegno" style="width: 700px;"/>

5. Successivamente, seleziona la tua **Location** e il **Pod** associato e quindi scegli il tuo **Server** e la quantità desiderata di **RAM**.

	Se pensi di utilizzare un Dual Processor Multi-Core Server, devi selezionare **Intel Xeon 5120** come tipo di server. {:note:}

	<img src="images/linked_server.png" alt="disegno" style="width: 600px;"/>

6. Seleziona una chiave SSH se vuoi utilizzarla per autenticare l'accesso al tuo nuovo gateway.
7. In **Image**, seleziona **Juniper vSRX 15.x (up to 1 Gbps) Standard** per un server con un solo processore o **Juniper vSRX 15.x (up to 10 Gbps) Standard** per un server con due processori.
8. Seleziona tutti i componenti aggiuntivi facoltativi e tutti gli **Storage Disks** aggiuntivi e scegli il tuo **Uplink Port Speed** desiderato.
8. Controlla le tue selezioni nell'**Order Summary**, quindi leggi e accetta i termini del software di terze parti.
9. Infine, fai clic su **Provision**.

### Fare un ordine con un account non collegato
Se il tuo account non è collegato, segui questa procedura:

1.	Apri il [Portale del cliente ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://control.softlayer.com/){: new_window} e accedi al tuo account.
2.	Nella navigazione del portale del cliente, seleziona **Network > Gateway Appliances**.
3.	Dall'elenco **Gateway Appliances**, fai clic su **Order Gateway**.
4.	Dalla pagina **Order**, seleziona il tuo data center desiderato dal menu a discesa, quindi scegli il tipo desiderato di hardware server su cui sarà eseguito il provisioning di Juniper vSRX.

	Se pensi di utilizzare un Dual Processor Multi-Core Server, devi selezionare **Intel Xeon 5120** come tipo di server. {:note}

5.	Nella pagina **Order**, seleziona l'opzione **High Availability Pair** se desiderato, quindi seleziona la dimensione di **Memory**.
6. 	Successivamente, fai clic sulla scheda **Juniper** in **Operating System**, seleziona **Juniper vSRX 15.x (up to 1 Gbps) Standard** per un server con un solo processore o **Juniper vSRX 15.x (up to 10 Gbps) Standard** per un server con due processori.
7. 	Infine, seleziona la velocità di uplink di rete desiderata.
8.	Controlla le tue selezioni, quindi fai clic su **Add to Order**. Il tuo ordine sarà verificato automaticamente.
9.	Nella pagina **Checkout**, se gestisci già delle VLAN nel data center selezionato, seleziona le VLAN di backend che vuoi proteggere. Assicurati di:
	* Fornire un nome host e un nome del dominio al tuo server
	* Selezionare una chiave SSH per l'autenticazione dell'accesso, se desiderato
	* Spunta tutte le caselle per i termini del servizio IBM Cloud e per i termini del software di terze parti
10. Fai clic su **Submit Order**.

## Operazioni successive
Dopo l'approvazione del tuo ordine, il provisioning del tuo vSRX si avvia automaticamente. Quando il processo di provisioning viene completato, il gateway verrà visualizzato nell'elenco **Gateway Appliances**.

Fai clic sul nome del gateway per aprire la pagina **Gateway Details**. Troverai gli indirizzi IP, il nome utente di accesso e le password del dispositivo.

<img src="images/after_order.png" alt="disegno" style="width: 700px;"/>
