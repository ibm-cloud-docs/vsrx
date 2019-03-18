---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Come consentire ping e SSH a una sottorete pubblica
{: #allowing-ssh-and-pinging-to-a-public-subnet}

In questa guida imparerai come configurare l'IBM® Cloud Juniper vSRX Standard con una nuova interfaccia, una zona e una rubrica. Poiché l'azione predefinita per tutto il traffico è drop, questa guida illustrerà come configurare i flussi del traffico che consentono tutto il traffico all'interno della nuova zona, tutto il traffico dalla nuova zona a internet e di consentire solo SSH e PING da internet a una sottorete nella nuova VLAN.

In questo esempio, vengono utilizzati i seguenti valori.
```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

**NOTA:** questa guida dettagliata presuppone una distribuzione ad elevata disponibilità del vSRX, con una sola VLAN pubblica e una sottorete.

## Cosa otterrai

In questa guida dettagliata imparerai come configurare il servizio:

Attività  | Descrizione
------------- | -------------
[Creare una nuova interfaccia, una zona e una sottorete della rubrica](/docs/infrastructure/vsrx?topic=vsrx-creating-the-new-interface-zone-and-address-book-subnet) | Creare la zona di sicurezza e l'unità di interfaccia contrassegnate per la nuova VLAN.
[Creazione dei tuoi nuovi flussi del traffico](/docs/infrastructure/vsrx?topic=vsrx-creating-your-new-traffic-flows) | Creare i nuovi flussi del traffico per consentire ping e SSH in entrata.
[Confermare l'output ed eseguire il commit delle modifiche](/docs/infrastructure/vsrx?topic=vsrx-confirming-the-output-and-commiting-the-changes) | Controllare l'output per confermare di cosa sarà eseguito il commit alla configurazione attiva.
