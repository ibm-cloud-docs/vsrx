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

# Création d'une interface, d'une zone et d'un sous-réseau de carnet d'adresses
Tout d'abord, vous devez créer une unité d'interface pour le réseau local virtuel et ajouter l'adresse de passerelle du sous-réseau. Vous pourrez ensuite créer une zone de sécurité associée à la nouvelle unité et une entrée `address-book` pour le sous-réseau.  

**Remarque :** Faites défiler l'écran vers la droite pour voir la commande dans son intégralité. 

```
set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29
```
