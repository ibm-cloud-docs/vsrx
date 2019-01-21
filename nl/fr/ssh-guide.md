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

# Comment autoriser le trafic SSH et ping vers un sous-réseau public ?
Dans ce guide, vous allez apprendre à configurer IBM® Cloud Juniper vSRX Standard avec une nouvelle interface, une nouvelle zone et un nouveau carnet d'adresses. L'action par défaut étant d'abandonner le trafic (drop), ce guide vous expliquera comment configurer des flux de circulation autorisant tout le trafic dans la nouvelle zone, tout le trafic de la nouvelle zone vers Internet, et autorisant seulement le trafic SSH et ping depuis Internet vers un sous-réseau du nouveau réseau local virtuel.

Les valeurs suivantes sont utilisées dans l'exemple.
```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

**Remarque :** Cette procédure détaillée suppose un déploiement haute disponibilité du vSRX, avec un seul VLAN public et sous-réseau.

## Ce que vous allez faire

Dans ce guide, vous apprendrez à configurer le service :

Tâche  | Description
------------- | -------------
[Création d'une interface, d'une zone et d'un sous-réseau de carnet d'adresses](ssh-create-interface.html) | Vous allez créer une unité d'interface balisée et une zone de sécurité pour le nouveau réseau local virtuel.
[Création de nouveaux flux de circulation](ssh-create-flows.html) | Vous allez créer les nouveaux flux de circulation pour autoriser le trafic ping et SSH entrant.
[Confirmation de sortie et validation des modifications](ssh-check-output.html) | Vous allez vérifier la sortie pour valider les modifications à apporter à la configuration active.
