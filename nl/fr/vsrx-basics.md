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

# Exécution des opérations IBM Cloud Juniper vSRX élémentaires
{: #performing-ibm-cloud-juniper-vsrx-basics}

La passerelle IBM® Cloud Juniper vSRX peut être configurée à l'aide d'une session de console distante via SSH ou en se connectant à l'interface graphique de gestion Web de Juniper.

**Remarque :** La configuration de vSRX en dehors de son shell et de son interface peut produire des résultats inattendus, et n'est donc pas recommandée.

## Accès à l'unité via SSH

Vous pouvez accéder au vSRX à l'aide de SSH via une adresse IP publique ou via une adresse IP privée si vous êtes sur un VPN SoftLayer :

1. Accédez à l'écran de détails Dispositifs de passerelle pour vous procurer l'IP de la passerelle publique ou privée.

  <img src="images/basics.png" alt="dessin" style="width: 700px;"/>

2. Cliquez sur l'icône représentant un oeil pour révéler le mot de passe de l'utilisateur admin.

3. Exécutez la commande `ssh admin@<gateway-ip>` et entrez le mot de passe de l'utilisateur admin.

**Remarque :** Si vous ne voyez pas l'icône représentant un oeil, il se peut que vous n'ayez pas les droits nécessaires pour visualiser le mot de passe. Vérifiez vos droits d'accès auprès du propriétaire du compte.

## Accès au mode de configuration

Vous pouvez passer en mode de configuration une fois qu'un shell a été ouvert sur le vSRX, en lançant la commande `config`. Vous pouvez effectuer plusieurs actions dans ce mode en utilisant les commandes suivantes :

* `show` - Afficher les configurations  
* `show | compare` - Afficher les modifications ayant été mises en préproduction
* `set` - Mettre en préproduction les modifications
* `commit check` - Vérifier la syntaxe de la configuration

Si les modifications vous conviennent, vous pouvez les valider dans la configuration active en exécutant les commandes `commit`, puis `save`.  

Pour quitter le mode de configuration, exécutez la commande `exit`.

## Accès au périphérique à l'aide de l'interface utilisateur de gestion Web de Juniper

L'interface graphique de gestion Web de Juniper a été configurée par défaut avec le certificat autosigné par vSRX. Seul le protocole HTTPS est activé sur le port 8443. Vous pouvez y accéder à l'adresse `https://gateway-ip:8443`.

![Détails sur le dispositif de passerelle haute disponibilité](images/vSRX-webui.png)

## Accès au périphérique à l'aide de la console VIRSH

Vous pouvez également accéder au vSRX à partir du système d'exploitation du serveur de passerelle :

1. Connectez-vous à votre serveur de passerelle en exécutant la commande `ssh root@<server-ip>`.
2. Exécutez la commande `virsh list` pour rechercher le nom de votre machine virtuelle vSRX.
3. Exécutez la commande `virsh console <your vSRX VM name>`.

## Création d'utilisateurs système

Par défaut, IBM Cloud Juniper vSRX est configuré avec un accès SSH pour le nom d'utilisateur `admin`. Des utilisateurs supplémentaires peuvent être ajoutés avec leur propre ensemble de priorités. Par exemple :

```
set system login user ops class operator authentication encrypted-password <CYPHER>
```

Dans cet exemple, `ops` correspond au nom d'utilisateur et `operator` désigne le niveau de classe/permission affecté à l'utilisateur.

Des classes personnalisées peuvent également être définies par opposition aux classes prédéfinies.

## Définition du nom d'hôte vSRX

Vous pouvez définir ou modifier le nom d'hôte vSRX à l'aide de la commande suivante :

```
set system host-name <hostname>
```

## Configuration DNS et NTP

Pour configurer la résolution du serveur de noms et le protocole NTP, exécutez les commandes suivantes :

```
set system name-server <DNS server>
set system ntp <NTP server>
```

## Changement du mot de passe root

Vous pouvez changer le mot de passe root à l'aide de la commande suivante :

```
set system root-authentication plain-text-password
```

Le système vous invite alors à saisir un nouveau mot de passe, qui est chiffré et stocké dans la configuration, et qui n'est pas visible.
