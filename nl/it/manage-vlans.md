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

# Gestione delle VLAN
Puoi eseguire varie azioni dalla [schermata Gateway Appliance Details](access-gateway-details.html).

## Associa una VLAN a un'applicazione gateway

Una VLAN deve essere associata a un'applicazione gateway prima di poter essere instradata. L'associazione della VLAN è il collegamento di una VLAN eleggibile a un gateway di rete in modo che possa essere instradata a un'applicazione gateway. Questa associazione non instrada automaticamente la VLAN all'applicazione gateway; la VLAN continua ad utilizzare i router del cliente di frontend e di backend finché non viene instradata.

Le VLAN possono essere associate a solo un gateway alla volta e non devono avere un firewall. Attieniti alla seguente procedura per associare una VLAN a un gateway di rete.

**NOTA:** se non ci sono VLAN disponibili da associare, dovrai [ordinarle](../vlans/order-vlan.html).

1. [Accedi alla schermata Gateway Appliance Details](access-gateway-details.html) nel portale del cliente.
2. Seleziona la scheda delle VLAN.
3. Fai clic su **Associate VLAN** e seleziona una VLAN dal menu a discesa.
4. Fai clic su **Save** e conferma la tua selezione. L'azione di associazione della VLAN non la instrada tramite il firewall.

Dopo aver associato una VLAN all'applicazione gateway, viene visualizzata nella sezione Associated VLANs della schermata Gateway Appliance Details. Da questa sezione, la VLAN può essere instradata al gateway o può esserne annullata l'associazione al gateway. È possibile associare ulteriori VLAN eleggibili a un'applicazione gateway in qualsiasi momento ripetendo i precedenti passi.

## Instrada una VLAN associata

Le VLAN associate sono collegate a un'applicazione gateway, ma il traffico in entrata ed uscita della VLAN non riguarda il gateway finché non è stata instradata la VLAN. Dopo l'instradamento di una VLAN associata, tutto il traffico di frontend e backend viene instradato tramite l'applicazione gateway invece che mediante i router del cliente. 

Esegui la seguente procedura per instradare una VLAN associata: 

1. [Accedi alla schermata Gateway Appliance Details](access-gateway-details.html) nel portale del cliente.
2. Seleziona la scheda delle VLAN.
3. Seleziona le VLAN desiderate attivando la casella di spunta. 
4. Fai clic su **Route Through** e conferma la tua selezione. 

Dopo l'instradamento di una VLAN, tutto il traffico di frontend e backend viene spostato dai router del cliente al gateway di rete. Possono essere eseguiti ulteriori controlli correlati al traffico e all'applicazione gateway stessa, accedendo allo strumento di gestione del gateway. L'instradamento tramite il gateway di rete può essere sospeso in qualsiasi momento [escludendo l'applicazione gateway](#bypass-gateway-appliance-routing-for-a-vlan). 

## Escludi l'instradamento dell'applicazione gateway per una VLAN 

Dopo l'instradamento di una VLAN, tutto il traffico di frontend e backend passa tramite il gateway di rete. In qualsiasi momento, l'applicazione gateway può essere esclusa in modo che il traffico ritorni ai router del cliente di frontend e backend (FCR e BCR). 

L'esclusione di una VLAN le consente di rimanere associata al gateway di rete. Se la VLAN non deve essere più associata all'applicazione gateway, fai riferimento a [Annullare l'associazione di una VLAN a un'applicazione gateway](#disassociate-a-vlan-from-a-gateway-appliance). 

Esegui la seguente procedura per escludere l'instradamento gateway per una VLAN: 

1. [Accedi alla schermata Gateway Appliance Details](access-gateway-details.html) nel portale del cliente.
2. Seleziona la scheda delle VLAN.
3. Seleziona le VLAN desiderate attivando la casella di spunta. 
4. Fai clic su **Route Around** e conferma la tua selezione. 

Dopo aver escluso il gateway di rete, tutto il traffico di frontend e backend viene instradato tramite i FCR e BCR associati alla VLAN. La VLAN rimarrà associata all'applicazione gateway e può essere instradata nuovamente ad essa in qualsiasi momento. 

## Annullare l'associazione di una VLAN a un'applicazione gateway 

Le VLAN possono essere collegate a un'applicazione gateway alla volta tramite l'[associazione](#associate-a-vlan-to-a-gateway-appliance). L'associazione consente alla VLAN di essere instradata all'applicazione gateway in qualsiasi momento. Se una VLAN deve essere associata a un'altra applicazione gateway o se non deve essere più associata al proprio gateway, è necessario un annullamento dell'associazione. L'annullamento dell'associazione rimuove il "link" dalla VLAN all'applicazione gateway, permettendole di essere associata a un altro gateway, se necessario. 

Esegui la seguente procedura per annullare l'associazione di una VLAN a un'applicazione gateway: 

1. [Accedi alla schermata Gateway Appliance Details](access-gateway-details.html) nel portale del cliente.
2. Seleziona la scheda delle VLAN.
3. Seleziona le VLAN desiderate attivando la casella di spunta. 
4. Fai clic su **Disassociate** e conferma la tua selezione. 

Dopo aver annullato l'associazione di una VLAN a un'applicazione gateway, la VLAN può essere associata a un altro gateway. La VLAN può anche essere riassociata all'applicazione gateway in qualsiasi momento. Dopo aver annullato l'associazione di una VLAN a un'applicazione gateway, il traffico della VLAN non può essere instradato tramite il gateway. Le VLAN devono essere associate a un'applicazione gateway prima di poter essere instradate. 

## Instrada più VLAN nella stessa interfaccia di rete 
IBM® Cloud Juniper vSRX può utilizzare più VLAN nella stessa interfaccia di rete. Può inoltre gestire il traffico contrassegnato o non contrassegnato contemporaneamente. Questo è possibile sul dispositivo autonomo impostando l'incapsulamento dell'interfaccia su `flexible-vlan-tagging` o sui dispositivi ad elevata disponibilità utilizzando reth2 e reth3 come interfacce contrassegnate. Questo viene fatto come parte della configurazione predefinita e non è necessario che venga modificato.  Sui dispositivi autonomi, Unit 0 è l'interfaccia secondaria che non è contrassegnata; sugli altri dispositivi, vengono contrassegnate le unità non zero.

Utilizza la seguente serie di comandi per configurare ulteriori interfacce contrassegnate:

Caso autonomo:
```
set interfaces ge-0/0/0 unit 50 vlan-id 50
set interfaces ge-0/0/0 unit 50 family inet address <IP/MASK>
```

Caso HA:
```
set interfaces reth2 unit 50 vlan-id 50
set interfaces reth2 unit 50 family inet address <IP/MASK>
```

**NOTA:** anche se l'unit 0 non è contrassegnata, `JunOS` ne ha bisogno per fare riferimento all'ID VLAN configurato come `native-vlan`. Nell'esempio, poiché `native-vlan-id` è `10`, anche l'unit 0 deve avere il `vlan-id` di `10`. In questo modo, `JunOS` viene informato che l'unit 0 non deve essere contrassegnata.

## Configurazione VLAN di esempio per vSRX

La seguente è una configurazione di esempio per vSRX che definisce due interfacce private e una zona del cliente.
Con questa configurazione di esempio, Private VLAN1 e Private VLAN2 possono comunicare tra loro. Le interfacce vSRX autonome sono definite come ge-0/0/0 (privata) e ge-0/0/1 (pubblica) e per l'istanza ad elevata disponibilità, sono definite come reth2 (privata HA) e reth3 (pubblica HA).

<img src="images/Sample-Topology-VLAN-to-VLAN.png" alt="disegno" style="width: 500px;"/>

```
# show interfaces

ge-0/0/0 {
   description PRIVATE_VLANs;
   flexible-vlan-tagging;
   native-vlan-id 1121;
   unit 0 {
       vlan-id 1121;
       family inet {
           address 10.184.108.158/26;
       }
   }
   unit 10 {
       vlan-id 1811;
       family inet {
           address 10.184.237.201/29;
       }
   }
   unit 20 {
       vlan-id 1812;
       family inet {
           address 10.185.48.9/29;
       }
   }
}


# show security zones security-zone CUSTOMER-PRIVATE
interfaces {
   ge-0/0/0.10 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
   ge-0/0/0.20 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
}
# show security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PRIVATE
policy Allow_C_C {
   match {
       source-address any;
       destination-address any;
       application any;
   }
   then {
       permit;
   }
}
```
