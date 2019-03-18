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

# Informazioni su IBM Cloud Juniper vSRX
{: #about-ibm-cloud-juniper-vsrx}

IBM® Cloud Juniper vSRX ti consente di instradare in modo selettivo il traffico di rete privato e pubblico tramite un firewall a livello aziendale completo che si avvale della tecnologia delle funzioni software JunOS, come gli stack di instradamento completo, la condivisione del traffico e QoS, l'instradamento basato sulle politiche e la VPN. vSRX fornisce le prestazioni, la facilità di configurazione e i vantaggi sulla manutenzione con la semplicità dell'esecuzione su un server bare metal. L'hardware è dimensionato per gestire il carico di instradamento/sicurezza per più VLAN e può essere ordinato con link di rete e array RAID ridondanti. Tutte le funzioni di vSRX sono gestite dal cliente.

IBM Cloud vSRX viene offerto in due modalità differenti: cluster ad elevata disponibilità (HA, High Availability) o autonomo.

**NOTA:** puoi trovare ulteriore documentazione su IBM Cloud Juniper vSRX nell'argomento [Documentazione supplementare](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation).

## Firewall
vSRX viene utilizzato per proteggere il tuo ambiente da minacce esterne e interne filtrando il traffico privato e pubblico. I clienti stessi possono gestire vSRX definendo politiche e regole per consentire o negare (tra le altre azioni) il traffico di rete in entrata e in uscita, proteggendo le proprie applicazioni da utenti interni ed esterni. Sono supportati sia gli stack IPv4 che IPv6 in una modalità con stato.

## Gateway VPN (Virtual Private Network)
Collega il tuo ufficio o data center in loco a IBM Cloud utilizzando il tunneling VPN eseguendo il provisioning del tuo vSRX come un dispositivo gateway di rete. Puoi utilizzare un tunnel VPN site-to-site IPsec per la comunicazione sicura dal tuo data center aziendale o dal tuo ufficio alla tua rete IBM Cloud. È supportato anche Remote access IPSEC VPN.

Per una guida di configurazione dettagliata sulla VPN, fai riferimento ai link forniti nell'argomento [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn).

## NAT (Network Address Translation)
Con l'applicazione gateway vSRX, puoi eseguire il provisioning dei server del database e dell'applicazione senza le interfacce di rete pubbliche mentre continui a consentire ai tuoi server di accedere a internet utilizzando Source NAT. Per una sicurezza avanzata, puoi anche nascondere i tuoi server dietro il dispositivo gateway con Destination NAT.

## Instradamento a livello aziendale
Per le applicazioni a più livelli su reti isolate diverse, vSRX ti consente di creare la connettività tra queste reti con maggiore flessibilità. Puoi configurare l'instradamento dinamico utilizzando BGP, che ti consente di annunciare il tuo spazio IP pubblico ai router IBM Cloud. BGP offrirà inoltre maggiore flessibilità per le configurazioni della rete privata personalizzata quando utilizzi un mix di soluzioni direct link e tunnel.

## Concetti sulle VLAN e sul ruolo dell'applicazione gateway
Una VLAN (LAN virtuale) è un meccanismo che suddivide une rete fisica in molti segmenti virtuali. Per comodità, il traffico da più VLAN selezionate può essere fornito tramite un solo cavo di rete, un processo comunemente chiamato "trunking."

vSRX è gestito in due diverse interfacce: i server vSRX e l'apparecchiatura dell'applicazione gateway. L'applicazione gateway fornisce un'interfaccia (GUI e API) per selezionare le VLAN che vuoi associare al tuo vSRX. L'associazione di una VLAN a un'applicazione gateway reinstrada (o "esegue il trunking") tale VLAN e tutte le sue sottoreti al tuo vSRX, fornendoti il controllo sul filtro, l'inoltro e la protezione. I server in una VLAN associata possono essere raggiunti solo da altre VLAN che passano attraverso il tuo vSRX; non è possibile aggirare il vSRX a meno che non escludi o annulli l'associazione alla VLAN.

Per impostazione predefinita, una nuova applicazione gateway viene associata a due VLAN "di transito" non rimovibili, una per ognuna delle tue reti _pubblica_ e _privata_. Queste reti normalmente sono utilizzate per la gestione e possono essere protette separatamente dai comandi vSRX.

vSRX può gestire solo le VLAN associate a esso tramite l'applicazione gateway.

Per informazioni su come gestire le VLAN dalla schermata **Gateway Appliances Details**, fai riferimento all'argomento [Gestione delle VLAN](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans).
