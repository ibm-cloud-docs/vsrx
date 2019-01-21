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

# Fonctionnement du routage
IBM® Cloud Juniper vSRX s'appuie sur `JunOS` pour vous permettre d'accéder à l'ensemble de la pile de routage Juniper.

##Routage statique
Pour configurer des routes statiques, exécutez les commandes suivantes :

###Configuration d'une route par défaut
```
set routing-options static route 0/0 next-hop <Gateway IP>
```

### Création d'une route statique
```
set routing-options static route <PREFIX/MASK> next-hop <Gateway IP>
```  

###Routage OSPF de base
Pour configurer le routage OSPF de base, seulement en utilisant la zone 0, exécutez les commandes suivantes à l'aide de l'authentification md5 :

```
set protocols ospf area 0 interface ge-0/0/1.0 authentication md5 0 key <KEY>
```

### Routage BGP de base
Pour configurer le routage BGP de base, définissez d'abord le système autonome local :

```
set routing-options autonomous-system 65001
```

Configurez ensuite le BGP voisin et ses attributs de session :

```
set protocols bgp group CUSTOMER local-address 1.1.1.1
set protocols bgp group CUSTOMER family inet unicast
set protocols bgp group CUSTOMER family inet6 unicast
set protocols bgp group CUSTOMER peer-as 65002
set protocols bgp group CUSTOMER neighbor 2.2.2.2
```

Dans cet exemple, BGP est configuré pour :

* Utiliser l'adresse IP source de `1.1.1.1` pour établir la session
* Négocier les familles unicast ipv4 et ipv6
* Echanger avec un voisin qui appartient à `AS 65002`
* Echanger avec l'IP voisin `2.2.2.2`

D'autres configurations sont disponibles [ici](https://www.juniper.net/documentation/en_US/junos11.4/information-products/topic-collections/config-guide-routing/config-guide-routing.pdf).
