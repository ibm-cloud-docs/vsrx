---

copyright:
  years: 2018
lastupdated: "2018-11-06"

keywords: limitations, problems

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

# Limitations connues pour IBM Cloud Juniper vSRX
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

Limites actuelles d'{{site.data.keyword.cloud}}IBM® Cloud Juniper vSRX :

* La passerelle Juniper vSRX est déployée à l'aide de la virtualisation de réseau sous Linux Bridge. La virtualisation de réseau basée sur Linux Bridge ne permet d'atteindre qu'un débit limité et non un débit de ligne.

* Aucune prise en charge n'est proposée pour passer du mode autonome au mode haute disponibilité.

* IBM Cloud Juniper vSRX Gateway est déployé avec les options de la version `15.1` ou `18.4` du système d'exploitation Junos. Actuellement, la mise à niveau/rétromigration vers une version différente n'est pas prise en charge.

* La licence d'évaluation de 60 jours peut amener le noyau à générer des messages ERROR, même s'il existe une autre licence (valide) sur le système. Vous devez supprimer toute licence d'évaluation de 60 jours pour éviter cela. Procédure :

1. Connectez-vous à votre périphérique de passerelle vSRX.

2. Entrez en mode d'interface CLI en exécutant la commande `cli` à l'invite de la console.

3. Exécutez la commande pour obtenir l'identifiant de licence : 

```
show system license
```
Le résultat devrait se présenter comme suit : 

```
License usage:
                                 Licenses     Licenses    Licenses    Expiry
  Feature name                       used    installed      needed
  logical-system                        0            3           0    permanent
  Virtual Appliance                     1            1           0    2021-10-18 00:00:00 UTC
  remote-access-ipsec-vpn-client        0            2           0    permanent

Licenses installed:
  License identifier: E2018101804
  License version: 4
  Software Serial Number: SUB00024128768
  Customer ID: IBM_SL_10G
  Features:
    Virtual Appliance - Virtual Appliance
      date-based, 2018-10-18 00:00:00 UTC - 2021-10-18 00:00:00 UTC
```

4. Copiez l'identifiant de la licence que vous souhaitez supprimer et exécutez la commande : 

```
request system license delete <license identifier>
```
