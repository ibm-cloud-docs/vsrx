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

# Gestion de réseaux locaux virtuels
Vous pouvez effectuer toute une série d'actions à partir de l'[écran des détails du dispositif de passerelle](access-gateway-details.html).

## Associer un VLAN à un dispositif de passerelle

Un VLAN doit être associé à un dispositif de passerelle pour permettre son routage. La procédure d'association consiste à lier un VLAN éligible à une passerelle réseau afin que le réseau local virtuel puisse être acheminé vers un dispositif de passerelle. Cette procédure ne permet pas de router automatiquement le VLAN vers un dispositif de passerelle ; le VLAN continue à utiliser les routeurs client frontaux et principaux jusqu'à ce qu'il soit redirigé.

Les VLAN peuvent être associés à une seule passerelle à la fois et ne doivent pas avoir de pare-feu. Pour associer un VLAN à une passerelle réseau, procédez comme suit :

**Remarque :** Si aucun VLAN n'est disponible pour une telle association, vous devrez alors en [commander](../vlans/order-vlan.html) un.

1. [Accédez à l'écran des détails du dispositif de passerelle](access-gateway-details.html) dans le portail client.
2. Sélectionnez l'onglet des VLAN.
3. Cliquez sur **Associer le VLAN** et choisissez un réseau local virtuel dans la liste déroulante.
4. Cliquez sur **Enregistrer** et validez votre sélection. Cette association ne fait pas passer le réseau local virtuel par le pare-feu.

Après avoir associé un VLAN au dispositif de passerelle, il apparaît dans la section VLAN associés de l'écran des détails du dispositif de passerelle. Dans cette section, le VLAN peut être routé vers la passerelle ou être dissocié de la passerelle. D'autres VLAN éligibles peuvent être associés à un dispositif de passerelle à tout moment en répétant la procédure ci-dessus.

## Acheminer un VLAN associé

Les VLAN associés sont liés à un dispositif de passerelle, mais le trafic entrant et sortant du VLAN n'atteint pas la passerelle tant que le VLAN n'a pas été routé. Une fois qu'un VLAN associé a été routé, l'ensemble du trafic, frontal et dorsal, est acheminé via le dispositif de passerelle, par opposition aux routeurs client.

Pour router un VLAN associé, procédez comme suit :

1. [Accédez à l'écran des détails du dispositif de passerelle](access-gateway-details.html) dans le portail client.
2. Sélectionnez l'onglet des VLAN.
3. Cochez le ou les VLAN de votre choix.
4. Cliquez sur **Route à Travers** et confirmez votre sélection.

Après le routage d'un VLAN, tout le trafic frontal et dorsal passe des routeurs client à la passerelle réseau. D'autres commandes liées au trafic et au dispositif de passerelle même peuvent être exécutées en accédant à l'outil de gestion de la passerelle. Le routage via la passerelle réseau peut être interrompu à tout moment en [contournant le dispositif de passerelle](#bypass-gateway-appliance-routing-for-a-vlan).

## Ignorer le routage du dispositif de passerelle pour un VLAN

Une fois le VLAN routé, tout le trafic frontal et dorsal passe par la passerelle réseau. A tout moment, le dispositif de passerelle peut être contourné de sorte que le trafic soit réorienté sur les routeurs client FCR et BCR.

Le contournement du VLAN permet au VLAN de rester associé à la passerelle réseau. Si le VLAN ne doit plus être associé au dispositif de passerelle, reportez-vous à la section [Dissocier un VLAN d'un dispositif de passerelle](#disassociate-a-vlan-from-a-gateway-appliance).

Pour ignorer le routage de la passerelle d'un VLAN, procédez comme suit :

1. [Accédez à l'écran des détails du dispositif de passerelle](access-gateway-details.html) dans le portail client.
2. Sélectionnez l'onglet des VLAN.
3. Cochez le ou les VLAN de votre choix.
4. Cliquez sur **Route Autour** et confirmez votre sélection.

Après le contournement de la passerelle réseau, tout le trafic frontal et dorsal circule via les routeurs FCR et BCR associés au VLAN. Le VLAN reste associé au dispositif de passerelle et peut être rerouté vers ce dispositif à tout moment.

## Dissocier un VLAN d'un dispositif de passerelle

Les VLAN peuvent être liés à un dispositif de passerelle à la fois par [association](#associate-a-vlan-to-a-gateway-appliance). Une association permet au VLAN d'être routé vers le dispositif de passerelle à tout moment. Si un VLAN doit être associé à un autre dispositif de passerelle ou s'il ne doit plus être associé à sa passerelle, une dissociation est requise. La dissociation supprime le "lien" du VLAN au dispositif de passerelle, permettant ainsi au VLAN d'être associé à une autre passerelle, si nécessaire.

Pour dissocier un VLAN d'un dispositif de passerelle, procédez comme suit :

1. [Accédez à l'écran des détails du dispositif de passerelle](access-gateway-details.html) dans le portail client.
2. Sélectionnez l'onglet des VLAN.
3. Cochez le ou les VLAN de votre choix.
4. Cliquez sur **Dissocier** et confirmez votre sélection.

Après avoir dissocié un VLAN d'un dispositif de passerelle, le VLAN peut être associé à une autre passerelle. Le VLAN peut également être réassocié au dispositif de passerelle à tout moment. Après avoir dissocié un VLAN d'un dispositif de passerelle, le trafic du VLAN ne peut pas être routé via la passerelle. Les VLAN doivent être associés à un dispositif de passerelle pour pouvoir être routés.

## Router plusieurs VLAN sur la même interface réseau
IBM® Cloud Juniper vSRX peut fonctionner avec plusieurs VLAN sur la même interface réseau. Il permet également de traiter le trafic balisé et non balisé en même temps. Pour cela, il utilise le périphérique autonome en définissant l'encapsulation d'interface sur `flexible-vlan-tagging`, ou sur les périphériques haute disponibilité en utilisant reth2 et reth3 comme interfaces balisées. Ceci est fait dans le cadre de la configuration par défaut et n'a pas besoin d'être modifié. Sur les périphériques autonomes, l'unité 0 correspond à la sous-interface non balisée, et les autres unités sont balisées.

Exécutez les commandes suivantes pour configurer des interfaces balisées supplémentaires :

Cas autonome :
```
set interfaces ge-0/0/0 unit 50 vlan-id 50
set interfaces ge-0/0/0 unit 50 family inet address <IP/MASK>
```

Cas haute disponibilité :

```
set interfaces reth2 unit 50 vlan-id 50
set interfaces reth2 unit 50 family inet address <IP/MASK>
```

**Remarque :** Bien que l'unité 0 ne soit pas balisée, `JunOS` en a besoin pour référencer l'ID du VLAN qui est configuré comme `native-vlan`. Dans notre exemple, `native-vlan-id` étant `10`, l'unité 0 doit avoir une valeur `vlan-id` de `10` également. De cette manière, `JunOS` sait que l'unité 0 doit être non balisée.

## Exemple de configuration VLAN pour vSRX

Vous trouverez ci-dessous un exemple de configuration pour vSRX qui définit deux interfaces privées et une zone client.
Avec cet exemple de configuration, Private VLAN1 et Private VLAN2 peuvent communiquer l'un avec l'autre. Les interfaces vSRX autonomes sont définies en tant que ge-0/0/0 (private) et ge-0/0/1 (public), et pour l'instance haute disponibilité, elles sont définies en tant que reth2 (HA private) et reth3 (HA public).

<img src="images/Sample-Topology-VLAN-to-VLAN.png" alt="dessin" style="width: 500px;"/>

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
