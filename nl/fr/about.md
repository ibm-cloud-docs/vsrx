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

# A propos d'IBM Cloud Juniper vSRX
{: #about-ibm-cloud-juniper-vsrx}

IBM® Cloud Juniper vSRX vous permet d'acheminer de façon ciblée le trafic réseau privé et public via un pare-feu complet de niveau entreprise doté de fonctionnalités logicielles JunOS, telles que des piles de routage, une qualité de service et un partage du réseau, un routage basé sur des règles et un réseau privé virtuel. vSRX associe les performances et la facilité de configuration et de maintenance à la simplicité d'exécution sur un serveur bare metal. Le matériel est dimensionné pour gérer la charge de routage/sécurité pour plusieurs réseaux locaux virtuels et peut être organisé avec des liens vers des réseaux redondants et des grappes RAID redondantes. Toutes les fonctionnalités de vSRX sont gérées par le client.

IBM Cloud vSRX est proposé dans deux modes différents : cluster autonome ou haute disponibilité.

**Remarque :** Vous trouverez des informations complémentaires sur IBM Cloud Juniper vSRX dans la rubrique [Documentation supplémentaire](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation).

## Pare-feu
Déployez vSRX pour protéger votre environnement contre les menaces externes et internes en filtrant à la fois le trafic privé et le trafic public. Les clients peuvent gérer eux-mêmes vSRX en définissant des politiques et des règles autorisant ou interdisant (entre autres actions) le trafic réseau entrant ou sortant, protégeant ainsi leurs applications des utilisateurs internes et externes. Les piles IPv4 et IPv6 sont toutes deux prises en charge de manière dynamique.

## Passerelle de réseau privé virtuel (VPN)
Connectez votre centre de données local ou votre bureau IBM Cloud à l'aide d'un tunnel VPN en mettant à disposition votre vSRX en tant que périphérique de passerelle réseau. Vous pouvez utiliser un tunnel VPN IPsec de site à site pour sécuriser la communication de votre centre de données d'entreprise ou de votre bureau vers votre réseau IBM Cloud. L'accès à distance IPSEC VPN est également pris en charge.

Pour obtenir des informations détaillées sur la configuration d'un VPN, veuillez vous reporter aux liens fournis dans la rubrique [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn).

## Conversion d'adresses réseau NAT
Grâce au dispositif de passerelle vSRX, vous pouvez installer des serveurs d'applications et de bases de données sans interface de réseau public, tout en permettant à vos serveurs d'accéder à Internet via la conversion NAT source. Vous pouvez également masquer vos serveurs derrière le dispositif de passerelle avec la conversion d'adresses réseau (NAT) de destination pour une sécurité renforcée.

## Routage au niveau de l'entreprise
Pour les applications multiniveaux installées sur différents réseaux isolés, vSRX vous permet de créer une connectivité entre ces réseaux avec une plus grande flexibilité. Vous pouvez configurer le routage dynamique à l'aide de BGP, ce qui vous permet de faire connaître votre propre espace IP public aux routeurs IBM Cloud. BGP offrira également plus de flexibilité pour les configurations de réseau privé personnalisées lors de l'utilisation d'une combinaison de tunnels et de solutions de lien direct.

## Concepts sur les VLAN et le rôle du dispositif de passerelle
Un VLAN (réseau local virtuel) est un mécanisme qui partage un réseau physique en de nombreux segments virtuels. Par commodité, le trafic en provenance de plusieurs VLAN sélectionnés peut être distribué via un seul câble réseau, un processus connu sous le nom de "jonction" (trunking).

vSRX est géré par deux interfaces différentes : le ou les serveurs vSRX et l'équipement fixe Dispositif de passerelle. Le dispositif de passerelle fournit une interface (graphique et de programmation) pour sélectionner les VLAN que vous souhaitez associer à votre vSRX. L'association d'un VLAN à un dispositif de passerelle redirige (ou "joint") ce VLAN et l'ensemble de ses sous-réseaux vers votre vSRX, vous permettant ainsi de contrôler les opérations de filtrage, de transfert et de protection. Les serveurs d'un VLAN associé ne sont accessibles depuis d'autres VLAN qu'en passant par votre vSRX. Il n'est pas possible de contourner le vSRX à moins d'ignorer ou de dissocier le VLAN.

Par défaut, un nouveau dispositif de passerelle est associé à deux VLAN de "transit" fixes, un pour votre réseau _public_ et un autre pour votre réseau _privé_. Ces réseaux sont généralement utilisés à des fins d'administration et peuvent être sécurisés séparément à l'aide de commandes vSRX.

vSRX ne peut gérer que les VLAN qui lui sont associés via le dispositif de passerelle.

Pour plus d'informations sur la gestion des VLAN à partir de l'écran des **détails du dispositif de passerelle**, voir la rubrique [Gestion de réseaux locaux virtuels](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans).
