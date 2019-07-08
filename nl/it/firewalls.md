---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords:

subcollection: vsrx, firewalls, working, policy, policies, rules, zones, standalone, ha

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

# Utilizzo dei firewall
{: #working-with-firewalls}

IBM® Cloud Juniper vSRX utilizza il concetto di zone di sicurezza, in cui ogni interfaccia vSRX è associata a una "zona" per la gestione dei firewall con stato. I firewall senza stato sono controllati dai filtri del firewall.

Vengono utilizzate le politiche per consentire o bloccare il traffico tra queste zone definite e le regole qui definite sono con stato.

In IBM Cloud, un vSRX è progettato per avere quattro zone di sicurezza differenti:

| Zona                     | Interfaccia autonoma | Interfaccia HA |
| :---                     |        :----:        |         ---: |
| SL-Private (non contrassegnato)    | ge-0/0/0.0 o ae0.0  | reth0.0      |
| SL-Public (non contrassegnato)     | ge-0/0/1.0 o ae1.0  | reth1.0      |
| Customer-Private (contrassegnato)| ge-0/0/0.1 o ae0.1  | reth2.1      |
| Customer-Public (contrassegnato) | ge-0/0/1.1 o ae1.1  | reth3.1      |

## Politiche della zona
{: #zone-policies}

Per configurare un firewall con stato, attieniti alla seguente procedura:

1. Crea le zone di sicurezza e assegna le rispettive interfacce:

	Scenario autonomo:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces ge-0/0/1.1
	```
	Scenario di elevata disponibilità:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces reth2.1
	```
2. Definisci la politica e le regole tra due zone differenti.

	Il seguente esempio illustra il traffico di ping dalla zona `Customer-Private` a `Customer-Public`:

	```
	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP match source-address any destination-address any application junos-icmp

	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP then permit
	```

Ci sono alcuni attributi che possono essere definiti nelle tue politiche:

* Indirizzi di origine
* Indirizzi di destinazione
* Applicazioni
* Azione (permit/deny/reject/count/log)

Poiché questa è un'operazione con stato, non è necessario consentire i pacchetti di ritorno (in questo caso, le risposte echo).

Utilizza i seguenti comandi per consentire il traffico indirizzato al vSRX:

Caso autonomo:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.0 host-inbound-traffic system-services all
```
Caso HA:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.0 host-inbound-traffic system-services all
```

Per consentire i protocolli, come ad esempio OSPF o BGP, utilizza il seguente comando:

Caso autonomo:
```
set security zones security-zone trust interfaces ge-0/0/0.0 host-inbound-traffic protocols all
```
Caso HA:
```
set security zones security-zone trust interfaces reth2.0 host-inbound-traffic protocols all
```

## Filtri del firewall
{: #firewall-filters}

Per impostazione predefinita, IBM Cloud Juniper vSRX consente ping, SSH e HTTPS a sé stesso e passa tutto l'altro traffico applicando il filtro `PROTECT-IN` all'interfaccia `lo`.

Per configurare un nuovo firewall senza stato, attieniti alla seguente procedura:

1. Crea il termine e il filtro del firewall (il seguente filtro consentirà solo ICMP e passerà tutto l'altro traffico)
	```
	set firewall filter ALLOW-PING term ICMP from protocol icmp
	set firewall filter ALLOW-PING term ICMP then accept
	```

2. Applica la regola del filtro all'interfaccia (il seguente comando applicherà il filtro a tutto il traffico di rete privato)
	```
	set interfaces ge-0/0/0 unit 0 family inet filter input ALLOW-PING
	```
