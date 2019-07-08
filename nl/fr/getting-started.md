---

copyright:
  years: 2018
lastupdated: "2019-05-03"

keywords: vsrx, ordering, gateway, appliance

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

# Initiation à la passerelle IBM Cloud Juniper vSRX
{: #getting-started}

Pour commencer à utiliser la passerelle IBM® Cloud Juniper vSRX, déterminez d'abord si votre compte est lié à IBM Cloud.

Pour savoir si votre compte est lié, accédez au [Portail client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window} dans votre navigateur et connectez-vous. Si votre compte est lié, le bouton **En savoir plus sur Bluemix** ne s'affiche pas dans le coin supérieur droit.

## Etapes pour la commande
{: #steps-for-ordering}

Vous pouvez commander votre dispositif de passerelle à l'aide de l'une de ces méthodes :

Pour la liste des limitations connues concernant la passerelle IBM Cloud Juniper vSRX, voir la [rubrique Limitations connues](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx).
{: note}

### Commander avec un compte lié
{: #ordering-with-a-linked-account}

Si votre compte est lié, procédez comme suit :

1. Depuis votre navigateur, ouvrez la page Dispositifs de passerelle dans le [Catalogue IBM Cloud ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/gen1/infrastructure/provision/gateway){: new_window} et connectez-vous à votre compte.

  Vous pouvez également accéder à cette page en vous connectant à la [console d'interface graphique IBM Cloud ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com) et en sélectionnant **Infrastructure classique > Réseau > Dispositif de passerelle**.
Dans le [Catalogue IBM Cloud ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/catalog), vous pouvez aussi sélectionner la catégorie **Réseau**, puis choisir la vignette **Dispositif de passerelle**.

2. Choisissez **Juniper vSRX (jusqu'à 1 Gbps)** ou **Juniper vSRX (jusqu'à 10 Gbps)** sous **Fournisseur de passerelle**.

3. Dans la section **Dispositif de passerelle**, entrez les informations **Nom d'hôte** et **Domaine**. Ces zones sont déjà renseignées avec les informations par défaut. Assurez-vous donc que les valeurs sont correctes. 

	<img src="images/linked_order.png" alt="dessin" style="width: 700px;"/>

4. Cochez l'option **Haute disponibilité** si vous le souhaitez, puis sélectionnez l'**Emplacement** du centre de données souhaité et le **Pod** spécifique dans le menu déroulant. 

  Seuls les pods ayant déjà un VLAN associé s'affichent ici. Si vous souhaitez mettre à disposition votre dispositif de passerelle dans un pod ne figurant pas dans la liste, créez d'abord un réseau VLAN.
  {: note}

	<img src="images/linked_server.png" alt="dessin" style="width: 600px;"/>

4. Dans la section **Configuration**, choisissez votre processeur en sélectionnant vos clés RAM et SSH (si vous souhaitez l'utiliser pour authentifier l'accès à votre nouvelle passerelle). 

  Le processeur approprié est automatiquement sélectionné en fonction de la version de la licence que vous choisissez à l'étape deux. Vous pouvez cependant choisir différentes configurations de RAM.
  {: note}

5. Dans la section **Disques de stockage**, choisissez les options correspondant à vos besoins en stockage. 

  Les options RAID0 et RAID1 offrent une protection supplémentaire contre la perte de données, tout comme les unités de secours à chaud (composants de sauvegarde pouvant être mis en service immédiatement en cas de défaillance d'un composant principal).
  {: note}

  Vous pouvez installer jusqu'à quatre disques par vSRX. La "taille de disque" associée à une configuration RAID correspond à la taille de disque utilisable, car les configurations RAID sont mises en miroir.
  {: note}

  Réservez plus que la valeur par défaut du disque si vous envisagez d'exécuter des diagnostics réseau produisant des journaux détaillés.
{: tip}

6. Dans la section **Interface réseau**, sélectionnez les **Vitesses de port pour la liaison montante**. La sélection par défaut est une interface unique, mais il existe également des options redondantes et privées uniquement. Choisissez celle qui correspond le mieux à vos besoins. 

  La section **Modules complémentaires** de l'Interface réseau vous permet de sélectionner une adresse IPv6 si nécessaire et vous indique les options par défaut supplémentaires incluses.

8. Passez en revue vos sélections, vérifiez que vous avez lu les contrats de service tiers, puis cliquez sur **Créer**. La commande est vérifiée automatiquement. 

Une fois votre commande approuvée, la mise à disposition de IBM Cloud Juniper vSRX Gateway démarre automatiquement. Quand le processus est terminé, le nouveau vSRX apparaît dans la page de liste Dispositifs de passerelle. Cliquez sur le nom de la passerelle pour ouvrir la page Détails de la passerelle. Vous y trouverez les adresses IP, le nom d'utilisateur et le mot de passe de connexion correspondant à l'unité.  

N'oubliez pas qu'une fois que vous commandez et configurez votre passerelle à partir d'IBM Cloud Catalog, vous devez également configurer l'unité elle-même avec les mêmes paramètres. {: tip}

### Commander avec un compte non lié
{: #ordering-with-a-unlinked-account}

Si votre compte n'est pas lié, procédez comme suit :

1.	Accédez au [portail client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window} et connectez-vous à votre compte.
2.	Dans la navigation du portail client, sélectionnez **Réseau > Dispositifs de passerelle**.
3.	Dans la liste **Dispositifs de passerelle**, cliquez sur **Commander passerelle**.
4.	Dans la page **Commander**, sélectionnez le centre de données de votre choix dans le menu déroulant, puis choisissez le type de matériel serveur sur lequel Juniper vSRX sera mis à disposition.

	Si vous prévoyez d'utiliser un serveur multicoeur à deux processeurs, vous devez sélectionner le type de serveur **Intel Xeon 5120**.
  {: note}

5.	Sur la page **Commander**, sélectionnez l'option **Paire à haute disponibilité** si vous le souhaitez, puis sélectionnez la taille de la **mémoire**.
6. 	Ensuite, cliquez sur l'onglet **Juniper** sous **Système d'exploitation**, sélectionnez **Juniper vSRX (jusqu'à 1 Gbit/s) Standard** pour un serveur à processeur unique ou **Juniper vSRX (jusqu'à 10 Gbit/s) Standard** pour un serveur à deux processeurs.
7. 	Enfin, sélectionnez la vitesse de liaison montante réseau souhaitée.
8.	Vérifiez vos sélections, puis cliquez sur **Ajouter à la commande**. Votre commande sera vérifiée automatiquement.
9.	Sur la page de **paiement**, si vous possédez déjà des VLAN dans le centre de données spécifié, sélectionnez les VLAN principaux que vous souhaitez protéger. N'oubliez pas de :
	* Donner un nom d'hôte et un nom de domaine à votre serveur. 
	* Sélectionner une clé SSH pour l'authentification d'accès, si vous le souhaitez.
	* Cocher toutes les cases des conditions du service IBM Cloud et du logiciel tiers.   
10. Cliquez sur **Soumettre commande**.

## Que faire ensuite ?
{: #what-s-next-}

Une fois votre commande approuvée, la mise à disposition du vSRX démarre automatiquement. Quand le processus est terminé, la passerelle apparaît dans la liste **Dispositifs de passerelle**.

Cliquez sur le nom de la passerelle pour ouvrir la page **Détails de la passerelle**. Les adresses IP, le nom d'utilisateur et les mots de passe du périphérique seront affichés.

<img src="images/after_order.png" alt="dessin" style="width: 700px;"/>
