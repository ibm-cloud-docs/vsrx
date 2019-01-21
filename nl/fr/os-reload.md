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

# Rechargement/Migration du système d'exploitation
Le processus de rechargement du système d'exploitation sert à régénérer un serveur de passerelle. Il s'articule autour des actions suivantes :

* Rechargement du système d'exploitation de l'hôte de serveur
* Installation d'une machine virtuelle multinoyaux (KVM) dans le système d'exploitation
* Création d'une machine virtuelle vSRX dans la KVM
* Reconfiguration de vSRX avec la configuration par défaut d'IBM® Cloud

Le processus nécessite généralement 1 heure 40 minutes. Les passerelles autonomes seront hors service pendant cette période. Pour les passerelles Juniper à haute disponibilité (HA), lorsque vous rechargez le système d'exploitation sur l'un de vos serveurs, le vSRX bascule vers un autre serveur du cluster et continue de traiter le trafic de données. Une fois le rechargement terminé, le serveur rejoint le cluster.

**Avertissement :** Si vous exécutez déjà un cluster Juniper haute disponibilité vSRX, ne procédez pas au rechargement du système d'exploitation sur les deux serveurs de la passerelle haute disponibilité simultanément. Cela détruirait le cluster vSRX et mettrait la passerelle hors service. Si le cluster vSRX est détruit, utilisez l'option de **régénération de cluster** (détaillée ci-dessous) pour remettre vSRX à disposition et recréer le cluster haute disponibilité.

## Rechargement du système d'exploitation
Pour recharger le système d'exploitation d'un serveur de passerelle, procédez comme suit :

1. [Accédez à l'écran Dispositifs de passerelle](access-gateway-appliances.html) dans le portail client et naviguez jusqu'à la page des détails en sélectionnant le nom de la passerelle désirée.

2. Cliquez sur le nom de serveur dans le panneau relatif au matériel.
![Serveur matériel](images/os_hardware.png)

3. Sur la page du périphérique, cliquez sur **Rechargement du système d'exploitation** dans le menu déroulant Action pour accéder à la page de configuration du serveur.
![Détails du périphérique](images/os_device_page.png)

4. Sur la page de configuration du serveur, configurez et démarrez le rechargement. Si vous rechargez à partir d'un autre système d'exploitation, cliquez sur **Editer** en regard de **Système d'exploitation**, sélectionnez **Juniper** et choisissez l'une des options Juniper vSRX 15.x Standard. Lorsque vous avez terminé de modifier vos paramètres, sélectionnez **Recharger configuration ci-dessus** pour continuer.

5. L'écran de détails du rechargement du système d'exploitation s'ouvre. Vérifiez les paramètres que vous avez choisis et cliquez sur **Editer les paramètres** si des changements sont nécessaires. Sinon, cliquez sur **Suivant** pour continuer.

6. Sur l'écran de confirmation du rechargement du système d'exploitation, acceptez les termes du Contrat principal de services et démarrez le processus de rechargement en cliquant sur **Confirmer le rechargement du système d'exploitation**. Sinon, cliquez sur **Annuler**.

## Migration à partir d'un serveur Vyatta/VRA vers un vSRX Juniper à l'aide de l'option de rechargement du système d'exploitation
Si vous rechargez un serveur Vyatta autonome, un vSRX Juniper sera mis à disposition une fois le rechargement du système d'exploitation terminé. Les mêmes adresses IP de passerelle seront utilisées et le mot de passe de l'utilisateur root sur le serveur hôte (ainsi que le mot de passe de l'utilisateur administrateur et de l'utilisateur root dans vSRX) seront réinitialisés.

Si vous rechargez des serveurs Vyatta haute disponibilité, vous devez exécuter la commande `Rechargement du système d'exploitation` sur les deux serveurs matériel. Ceci installe Ubuntu version 16.04. Ensuite, utilisez l'option de régénération du cluster (détaillée dans la section suivante) pour mettre à disposition le vSRX et créer le cluster haute disponibilité. A l'instar d'un vSRX autonome, les mêmes adresses IP de passerelle seront utilisées, et le mot de passe de l'utilisateur root sur le serveur hôte (ainsi que le mot de passe pour l'utilisateur administrateur et de l'utilisateur root) seront réinitialisés.

**Avertissement :** Ne procédez pas au rechargement du système d'exploitation sur un seul serveur du cluster Vyatta haute disponibilité. L'utilisation de deux systèmes d'exploitation différents sur un même cluster de passerelle haute disponibilité n'est pas prise en charge.

## Régénération d'un cluster vSRX haute disponibilité
Pour régénérer l'un de vos clusters vSRX haute disponibilité, procédez comme suit :

1. [Accédez à l'écran Dispositifs de passerelle](access-gateway-appliances.html) dans le portail client et naviguez jusqu'à la page des détails en sélectionnant le nom de la passerelle HA désirée.

2. Cliquez sur l'option permettant de **régénérer le cluster** dans le panneau vSRX.
![Régénération du cluster](images/rebuild_cluster.png)

3. Lisez attentivement le message d'avertissement. L'opération de régénération d'un cluster est destructrice. Si vous souhaitez continuer, enregistrez votre configuration vSRX avant de cliquer sur **Régénérer** pour démarrer le processus.
![Confirmation de régénération du cluster](images/rebuild_cluster_confirm.png)
