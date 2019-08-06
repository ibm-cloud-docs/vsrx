---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: basics, performing, accessing, ssh, device, gateway, configuration, mode, juniper, ui, dns, htp, password

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# Esecuzione dei principi di base di {{site.data.keyword.vsrx_full}}
{: #performing-ibm-cloud-juniper-vsrx-basics}

Il gateway {{site.data.keyword.vsrx_full}} può essere configurato utilizzando una sessione della console remota tramite SSH o eseguendo l'accesso alla GUI di gestione web Juniper.

La configurazione di vSRX al di fuori della sua shell e interfaccia può produrre risultati non previsti e non è consigliata.
{: note}

## Accesso al dispositivo utilizzando SSH
{: #accessing-the-device-using-ssh}

Puoi accedere al vSRX utilizzando SSH tramite un indirizzo IP pubblico o tramite un indirizzo IP privato se sei in una VPN SoftLayer:

1. Vai alla schermata Gateway Appliance Details e ottieni l'IP del gateway pubblico o privato.

  <img src="images/gw-sa-details.png" alt="disegno" style="width: 700px;"/>

2. Fai clic sull'icona "a forma di occhio" per visualizzare la password dell'utente amministratore.

3. Esegui il comando `ssh admin@<gateway-ip>` e immetti quindi la password dell'utente amministratore.

Se non visualizzi l'icona "a forma di occhio", potresti non avere l'autorizzazione per visualizzare la password. Controlla le tue autorizzazioni di accesso con il proprietario dell'account.
{: note}

## Accesso alla modalità di configurazione
{: accessing-the-configuration-mode}

Una volta che è stata aperta una shell nel vSRX, puoi entrare nella modalità di configurazione eseguendo il comando `config`. Utilizzando i seguenti comandi, puoi fare molte cose in questa modalità:

* `show` - Visualizza le configurazioni  
* `show | compare` - Visualizza le modifiche preparate
* `set` - Prepara le modifiche
* `commit check` - Verifica la sintassi della configurazione

Se sei soddisfatto delle tue modifiche, puoi eseguirne il commit alla configurazione attiva eseguendo i comandi `commit` e poi `save`.  

Per uscire dalla modalità di configurazione esegui il comando `exit`.

## Accesso al dispositivo utilizzando l'IU di gestione web Juniper
{: #accessing-the-device-using-the-juniper-web-management-ui}

La GUI di gestione web Juniper è stata configurata per impostazione predefinita, con il certificato autofirmato generato da vSRX. È abilitato solo https sulla porta 8443. Puoi accedere all'indirizzo `https://gateway-ip:8443`.

![Dettagli HA applicazione gateway](images/vSRX-webui.png)

## Creazione degli utenti di sistema
{: #creating-system-users}

Per impostazione predefinita, {{site.data.keyword.vsrx_full}} è configurato con l'accesso SSH per il nome utente `admin`. Possono essere aggiunti ulteriori utenti con le proprie serie di priorità. Ad esempio:

```
set system login user ops class operator authentication encrypted-password <CYPHER>
```

In questo esempio, `ops` è il nome utente e `operator` è il livello di autorizzazione/classe assegnato all'utente.

Possono inoltre essere definite classi personalizzate invece di quelle predefinite.

## Definizione del nome host vSRX
{: #defining-the-vsrx-hostname}

Puoi configurare o modificare il nome host vSRX utilizzando il seguente comando:

```
set system host-name <hostname>
```

## Configurazione di DNS e NTP
{: #configuring-dns-and-ntp}

Per configurare la risoluzione del server dei nomi e NTP, immetti il seguente comando:

```
set system name-server <DNS server>
set system ntp <NTP server>
```

## Modifica della password root
{: #changing-the-root-password}

Puoi modificare la password root immettendo il seguente comando:

```
set system root-authentication plain-text-password
```

Questo comando ti richiede di inserire una nuova password, che viene codificata e archiviata nella configurazione e non è visibile.
