---

copyright:
  years: 2018
lastupdated: "2018-11-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Initiation

Pour commencer à utiliser la passerelle IBM® Cloud Juniper vSRX, déterminez d'abord si votre compte est lié à IBM Cloud.

## Avant de commencer

Pour savoir si votre compte est lié, accédez au [Portail client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window} dans votre navigateur et connectez-vous. Si votre compte n'est pas lié, le bouton **En savoir plus sur Bluemix** s'affiche dans le coin supérieur droit.

## Etapes pour la commande

Vous pouvez commander votre dispositif de passerelle à l'aide de l'une de ces méthodes :

**Remarque :** Pour obtenir une liste des limitations connues avec la passerelle IBM Cloud Juniper vSRX, reportez-vous à la rubrique [Limitations connues](known-limitations.html).

### Commander avec un compte lié
Si votre compte est lié, procédez comme suit :

1.	Ouvrez la [Console IBM Cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.bluemix.net/){: new_window} et connectez-vous à votre compte.
2.	Dans le menu de gauche, sélectionnez **Infrastructure > Réseau > Dispositifs de passerelle**.
3.	Dans la liste **Dispositifs de passerelle**, cliquez sur **Créer une passerelle**.
4. Dans la page **Commander**, indiquez un **Nom d'hôte** et un **Domaine**.
5. Sélectionnez l'option **Paire à haute disponibilité**, si vous le souhaitez.

	<img src="images/linked_order.png" alt="dessin" style="width: 700px;"/>

5. Sélectionnez ensuite votre **Emplacement** et la **Capsule** associée, puis choisissez votre **Serveur** et la quantité de mémoire **RAM** voulue.

	**Remarque :** Si vous envisagez d'utiliser un serveur multicoeur à deux processeurs, choisissez le type de serveur **Intel Xeon 5120**.

	<img src="images/linked_server.png" alt="dessin" style="width: 600px;"/>

6. Sélectionnez une clé SSH si vous souhaitez l'utiliser pour authentifier l'accès à votre nouvelle passerelle.
7. Sous **Image**, sélectionnez **Juniper vSRX 15.x (jusqu'à 1 Gbit/s) Standard** pour un serveur à processeur unique ou **Juniper vSRX 15.x (jusqu'à 10 Gbit/s) Standard** pour un serveur à deux processeurs.
8. Sélectionnez des modules complémentaires facultatifs, ajoutez des **disques de stockage** supplémentaires, et indiquez la **Vitesse de port de liaison montante** de votre choix.
8. Passez en revue vos sélections dans la page **Récapitulatif de la commande**, puis lisez et acceptez les conditions du logiciel tiers.
9. Enfin, cliquez sur **Mettre à disposition**.

### Commander avec un compte non lié
Si votre compte n'est pas lié, procédez comme suit :

1.	Accédez au [portail client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window} et connectez-vous à votre compte.
2.	Dans la navigation du portail client, sélectionnez **Réseau > Dispositifs de passerelle**.
3.	Dans la liste **Dispositifs de passerelle**, cliquez sur **Commander passerelle**.
4.	Dans la page **Commander**, sélectionnez le centre de données de votre choix dans le menu déroulant, puis choisissez le type de matériel serveur sur lequel Juniper vSRX sera mis à disposition. 

	**Remarque :** Si vous envisagez d'utiliser un serveur multicoeur à deux processeurs, choisissez le type de serveur **Intel Xeon 5120**.
	
5.	Sur la page **Commander**, sélectionnez l'option **Paire à haute disponibilité** si vous le souhaitez, puis sélectionnez la taille de la **mémoire**.
6. 	Ensuite, cliquez sur l'onglet **Juniper** sous **Système d'exploitation**, sélectionnez **Juniper vSRX 15.x (jusqu'à 1 Gbit/s) Standard** pour un serveur à processeur unique ou **Juniper vSRX 15.x (jusqu'à 10 Gbit/s) Standard** pour un serveur à deux processeurs.
7. 	Enfin, sélectionnez la vitesse de liaison montante réseau souhaitée.
8.	Vérifiez vos sélections, puis cliquez sur **Ajouter à la commande**. Votre commande sera vérifiée automatiquement.
9.	Sur la page de **paiement**, si vous possédez déjà des VLAN dans le centre de données spécifié, sélectionnez les VLAN principaux que vous souhaitez protéger. N'oubliez pas de :
	* Donner un nom d'hôte et un nom de domaine à votre serveur
	* Sélectionner une clé SSH pour l'authentification d'accès, si vous le souhaitez
	* Cocher toutes les cases des conditions du service IBM Cloud et du logiciel tiers
10. Cliquez sur **Soumettre commande**.

## Que faire ensuite ?
Une fois votre commande approuvée, la mise à disposition du vSRX démarre automatiquement. Quand le processus est terminé, la passerelle apparaît dans la liste **Dispositifs de passerelle**.

Cliquez sur le nom de la passerelle pour ouvrir la page **Détails de la passerelle**. Les adresses IP, le nom d'utilisateur et les mots de passe du périphérique seront affichés.

<img src="images/after_order.png" alt="dessin" style="width: 700px;"/>
