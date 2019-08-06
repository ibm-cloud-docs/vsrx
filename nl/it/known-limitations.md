---

copyright:
  years: 2018
lastupdated: "2018-11-06"

keywords: limitations, problems

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

# Limitazioni note per {{site.data.keyword.vsrx_full}}
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

Limitazioni correnti per {{site.data.keyword.cloud}} {{site.data.keyword.vsrx_full}}:

* Juniper vSRX Gateway viene distribuito con la virtualizzazione della rete utilizzando Linux Bridge. La virtualizzazione della rete basata su Linux Bridge può utilizzare solo una velocità effettiva limitata e mai quella della linea.

* Non c'è supporto per l'upgrade dalla modalità autonoma alla modalità ad elevata disponibilità.

* {{site.data.keyword.vsrx_full}} Gateway viene distribuito con le opzioni del sistema operativo Junos versione `15.1` o `18.4`. Al momento, non c'è supporto per l'upgrade/downgrade a una versione diversa.

* A causa della licenza di valutazione di 60 giorni, il kernel potrebbe generare dei messaggi di errore (ERROR), anche quando c'è un'altra licenza (valida) sul sistema. Per evitare questo problema, devi rimuovere le eventuali licenze di valutazione di 60 giorni. A tale scopo, attieniti alla seguente procedura:

1. Accedi al tuo dispositivo gateway vSRX.

2. Entra nella modalità della CLI eseguendo il comando `cli` quando richiesto dalla console.

3. Esegui il comando per ottenere l'identificativo licenza:

```
show system license
```
L'output dovrebbe essere simile al seguente:

```
License usage:
                                 Licenses     Licenses    Licenses    Expiry
  Feature name                       used    installed      needed
  logical-system                        0            3           0    permanent
  Virtual Appliance                     1            1           0    2021-10-18 00:00:00 UTC
  remote-access-ipsec-vpn-client        0            2           0    permanent

Licenses installed:
  License identifier: E2018101804
  License version: 4
  Software Serial Number: SUB00024128768
  Customer ID: IBM_SL_10G
  Features:
    Virtual Appliance - Virtual Appliance
      date-based, 2018-10-18 00:00:00 UTC - 2021-10-18 00:00:00 UTC
```

4. Copia l'identificativo della licenza che vuoi eliminare ed esegui il comando:

```
request system license delete <license identifier>
```
