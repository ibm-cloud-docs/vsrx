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

# Création de nouveaux flux de circulation
Maintenant que vous avez créé la nouvelle zone (`CUSTOMER-PUBLIC`), vous devez configurer les politiques permettant de contrôler le flux de circulation réseau. Le premier flux défini ci-dessous autorise tout le trafic dans la zone `CUSTOMER-PUBLIC`. Le deuxième autorise tout le trafic de la zone `CUSTOMER-PUBLIC` vers l'Internet public, tandis que le troisième flux autorise uniquement le trafic SSH et PING de l'Internet public vers la zone `CUSTOMER-PUBLIC`, et supprime tout le reste (`drop` étant l'action par défaut).

**Remarque :** Faites défiler l'écran vers la droite pour voir la commande dans son intégralité.   

```
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL description "Allow all traffic within CUSTOMER_PUBLIC zone"
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL match source-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL match destination-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL match application any
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL then permit

set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND description "Allow all outbound traffic from CUSTOMER-PUBLIC to the internet"
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND match source-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND match destination-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND match application any
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND then permit

set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH description "Allow ping and SSH from the internet to the public subnet"
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match source-address any
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match destination-address VSI_PUB_NET
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match application junos-ssh
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match application junos-ping
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH then permit
```  
