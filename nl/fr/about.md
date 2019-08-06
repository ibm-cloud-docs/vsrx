---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: about, vsrx, overview, details, firewall, vpn, nat, routing, vlan

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

# A propos d'{{site.data.keyword.vsrx_full}}
{: #about-ibm-cloud-juniper-vsrx}

{{site.data.keyword.vsrx_full}} vous permet d'acheminer de façon ciblée le trafic réseau privé et public via un pare-feu complet de niveau entreprise doté de fonctionnalités logicielles JunOS, telles que des piles de routage, une qualité de service et un partage du réseau, un routage basé sur des règles et un réseau privé virtuel. vSRX associe les performances et la facilité de configuration et de maintenance à la simplicité d'exécution sur un serveur bare metal. Le matériel est dimensionné pour gérer la charge de routage et de sécurité pour plusieurs réseaux locaux virtuels et peut être organisé avec des liens vers des réseaux redondants et des grappes RAID redondantes. Toutes les fonctionnalités de vSRX sont gérées par le client.

{{site.data.keyword.vsrx_full}} est proposé dans deux modes différents : cluster en mode autonome ou haute disponibilité.

Vous trouverez des informations complémentaires sur {{site.data.keyword.vsrx_full}} dans la rubrique [Documentation supplémentaire](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation).
{: note}

## Pare-feu
{: #firewall}

Déployez vSRX pour protéger votre environnement contre les menaces externes et internes en filtrant le trafic privé et le trafic public. Les clients peuvent gérer eux-mêmes vSRX en définissant des politiques et des règles autorisant ou interdisant (entre autres actions) le trafic réseau entrant ou sortant, protégeant ainsi leurs applications des approches internes et externes. Les piles IPv4 et IPv6 sont toutes deux prises en charge de manière dynamique.

## Passerelle de réseau privé virtuel (VPN)
{: #virtual-private-network-vpn-gateway}

Connectez votre centre de données local ou votre bureau IBM Cloud à l'aide d'un tunnel VPN en mettant à disposition votre vSRX en tant que périphérique de passerelle réseau. Vous pouvez utiliser un tunnel VPN IPsec de site à site pour sécuriser la communication de votre centre de données d'entreprise ou de votre bureau vers votre réseau IBM Cloud. Le VPN IPsec d'accès à distance est également pris en charge.

Pour obtenir des informations détaillées sur la configuration d'un VPN, veuillez vous reporter aux liens fournis dans la rubrique [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn).

## Conversion d'adresses réseau (NAT)
{: #network-address-translation-nat-}

Grâce au dispositif de passerelle vSRX, vous pouvez installer des serveurs d'applications et de bases de données sans interface de réseau public, tout en permettant à vos serveurs d'accéder à Internet via la _conversion NAT source_. Pour une sécurité renforcée, vous pouvez protéger vos serveurs derrière le périphérique de passerelle à l’aide de la _conversion NAT de destination_.

## Routage au niveau de l'entreprise
{: #enterprise-grade-routing}

Le vSRX vous donne plus de flexibilité pour établir une connectivité entre des applications multiniveaux exécutées sur différents réseaux isolés. Vous pouvez configurer le routage dynamique à l'aide de BGP, ce qui vous permet de faire connaître votre propre espace IP public aux routeurs IBM Cloud. BGP offre également plus de flexibilité pour les configurations de réseau privé personnalisées lors de l'utilisation d'une combinaison de tunnels et de [solutions Direct Link](/docs/infrastructure/direct-link?topic=direct-link-overview-of-direct-link-offerings#overview-of-direct-link-offerings).

## Concepts sur les VLAN et le rôle du dispositif de passerelle
{: #concepts-about-vlans-and-the-gateway-appliance-s-role}

Un VLAN (réseau local virtuel) est un mécanisme qui partage un réseau physique en de nombreux segments virtuels. Par commodité, le trafic en provenance de plusieurs VLAN sélectionnés peut être distribué via un seul câble réseau, à l'aide d'un processus connu sous le nom de "jonction" (trunking).

vSRX est géré par deux interfaces différentes : le ou les serveurs vSRX et l'équipement fixe Dispositif de passerelle. Le dispositif de passerelle fournit une interface (graphique et de programmation) pour sélectionner les VLAN que vous souhaitez associer à votre vSRX. L'association d'un VLAN à un dispositif de passerelle redirige (ou "joint") ce VLAN et l'ensemble de ses sous-réseaux vers votre vSRX, vous permettant ainsi de contrôler les opérations de filtrage, de transfert et de protection. Les serveurs d'un VLAN associé ne sont accessibles depuis d'autres VLAN qu'en passant par votre vSRX. Il n'est pas possible de contourner le vSRX à moins d'ignorer ou de dissocier le VLAN.

Par défaut, un nouveau dispositif de passerelle est associé à deux VLAN de "transit" fixes, un pour votre réseau _public_ et un autre pour votre réseau _privé_. Ces réseaux sont généralement utilisés à des fins d'administration et peuvent être sécurisés séparément à l'aide de commandes vSRX.

vSRX peut gérer les VLAN qui lui sont associés via le dispositif de passerelle uniquement.

Pour plus d'informations sur la gestion des VLAN à partir de l'écran des **détails du dispositif de passerelle**, voir la rubrique [Gestion de réseaux locaux virtuels](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans).
