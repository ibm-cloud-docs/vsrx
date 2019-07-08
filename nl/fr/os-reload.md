---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: reloading, os, upgrading, kvm, ha, standalone

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Rechargement du système d'exploitation
{: #reloading-the-os}

Le processus de rechargement du système d'exploitation sert à régénérer un serveur de passerelle. Il s'articule autour des actions suivantes :

* Rechargement du système d'exploitation de l'hôte de serveur
* Installation d'une machine virtuelle multinoyau (KVM) dans le système d'exploitation
* Création d'une machine virtuelle vSRX dans la KVM
* Reconfiguration de vSRX avec la configuration par défaut d'IBM® Cloud

Le processus nécessite généralement 1 heure 40 minutes. Les passerelles autonomes seront hors service pendant cette période. Pour les passerelles Juniper à haute disponibilité (HA), lorsque vous rechargez le système d'exploitation sur l'un de vos serveurs, le vSRX bascule vers un autre serveur du cluster et continue de traiter le trafic de données. Une fois le rechargement terminé, le serveur rejoint le cluster.

Pour recharger ou reconstruire le cluster sur un vSRX à haute disponibilité, procédez comme suit : 

* Le mot de passe racine de la passerelle vSRX mise à disposition doit correspondre à celui défini dans le portail vSRX. Le mot de passe du portail a été défini lors de la première mise à disposition de la passerelle et peut ne pas correspondre au mot de passe actuel de la passerelle. Si le mot de passe a été modifié après la mise à disposition initiale, utilisez SSH pour vous connecter à la passerelle vSRX et modifiez le mot de passe root afin qu'il corresponde. Une fois les mots de passe définis, vous pouvez procéder à l'opération de rechargement du système d'exploitation ou de reconstruction du cluster. 

  <img src="images/gw-vsrx-password.png" alt="dessin" style="width: 700px;"/>

* **N'effectuez PAS** de rechargement du système d'exploitation sur les deux serveurs de la passerelle à haute disponibilité simultanément. 

Un rechargement du système d'exploitation simultané sur les deux serveurs de la passerelle à haute disponibilité détruit le cluster vSRX et entraîne la mise hors service de la passerelle. Si le cluster vSRX est détruit, utilisez l'option de **régénération de cluster** (détaillée ci-dessous) pour remettre vSRX à disposition et recréer le cluster haute disponibilité.
{: important}

## Rechargement du système d'exploitation
{: #performing-an-os-reload}

Pour recharger le système d'exploitation d'un serveur de passerelle, procédez comme suit :

1. [Accédez à l'écran Dispositifs de passerelle](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) dans le portail client et naviguez jusqu'à la page des détails en sélectionnant le nom de la passerelle désirée.

  <img src="images/gw-sa-details.png" alt="dessin" style="width: 700px;"/>

2. Cliquez sur le nom de serveur dans le panneau relatif au matériel.

  ![Serveur matériel](images/os_hardware.png)

3. Sur la page de l'unité, cliquez sur **Rechargement du système d'exploitation** dans le menu déroulant Action pour accéder à la page de configuration du serveur. 

  ![Détails de l'unité](images/os_device_page.png)

4. Sur la page de configuration du serveur, configurez et démarrez le rechargement. Si vous rechargez à partir d'un autre système d'exploitation, cliquez sur **Editer** en regard de **Système d'exploitation**, sélectionnez **Juniper** et choisissez l'une des options Juniper vSRX 15.x Standard. Lorsque vous avez terminé de modifier vos paramètres, sélectionnez **Recharger configuration ci-dessus** pour continuer.

5. L'écran de détails du rechargement du système d'exploitation s'ouvre. Vérifiez les paramètres que vous avez choisis et cliquez sur **Editer les paramètres** si des changements sont nécessaires. Sinon, cliquez sur **Suivant** pour continuer.

6. Sur l'écran de confirmation du rechargement du système d'exploitation, acceptez les termes du Contrat principal de services et démarrez le processus de rechargement en cliquant sur **Confirmer le rechargement du système d'exploitation**. Sinon, cliquez sur **Annuler**.

## Régénération d'un cluster vSRX haute disponibilité
{: #rebuilding-an-ha-vsrx-cluster}

Pour régénérer l'un de vos clusters vSRX haute disponibilité, procédez comme suit :

1. [Accédez à l'écran Dispositifs de passerelle](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) dans le portail client et naviguez jusqu'à la page des détails en sélectionnant le nom de la passerelle HA désirée.

2. Cliquez sur le menu déroulant **Actions** et sélectionnez l'option de **régénération de cluster**.

3. Lisez attentivement le message d'avertissement. L'opération de régénération d'un cluster est destructrice. Si vous souhaitez continuer, enregistrez votre configuration vSRX avant de cliquer sur **Régénérer** pour démarrer le processus.

  ![Confirmer la régénération du cluster](images/rebuild_cluster_confirm.png)
