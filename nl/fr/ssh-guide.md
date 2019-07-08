---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords:

subcollection: vsrx, ssh, allowing, pinging, subnet, public

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# Autorisation du trafic SSH et de Ping vers un sous-réseau public
{: #allowing-ssh-and-pinging-to-a-public-subnet}

Dans ce guide, vous allez apprendre à configurer IBM® Cloud Juniper vSRX Standard avec une nouvelle interface, une nouvelle zone et un nouveau carnet d'adresses. L'action par défaut étant d'abandonner le trafic (drop), ce guide vous expliquera comment configurer des flux de circulation autorisant tout le trafic dans la nouvelle zone, tout le trafic de la nouvelle zone vers Internet, et autorisant seulement le trafic SSH et ping depuis Internet vers un sous-réseau du nouveau réseau local virtuel.

Les valeurs suivantes sont utilisées dans l'exemple.

```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

Cette procédure détaillée suppose un déploiement haute disponibilité du vSRX, avec un seul VLAN public et sous-réseau.
{: note}

## Ce que vous allez faire
{: #what-you-ll-accomplish}

Dans ce guide, vous apprendrez à configurer le service :

Tâche  | Description
------------- | -------------
[Création d'une interface, d'une zone et d'un sous-réseau de carnet d'adresses](/docs/infrastructure/vsrx?topic=vsrx-creating-the-new-interface-zone-and-address-book-subnet) | Vous allez créer une unité d'interface balisée et une zone de sécurité pour le nouveau réseau local virtuel.
[Création de nouveaux flux de circulation](/docs/infrastructure/vsrx?topic=vsrx-creating-your-new-traffic-flows) | Vous allez créer les nouveaux flux de circulation pour autoriser le trafic ping et SSH entrant.
[Confirmation de sortie et validation des modifications](/docs/infrastructure/vsrx?topic=vsrx-confirming-the-output-and-commiting-the-changes) | Vous allez vérifier la sortie pour valider les modifications à apporter à la configuration active.
