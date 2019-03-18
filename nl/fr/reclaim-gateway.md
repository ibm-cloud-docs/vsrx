---

copyright:
  years: 2018
lastupdated: "2018-11-06"

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

# Récupération d'une passerelle
{: #reclaiming-a-gateway}

Pour récupérer votre passerelle, procédez comme suit :

1. [Accédez à l'écran Dispositifs de passerelle](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) dans le portail client et naviguez jsuqu'à la page des détails en sélectionnant le nom de la passerelle souhaitée.

2. Cliquez sur le nom de serveur dans le panneau relatif au matériel.

	![Serveur matériel](images/os_hardware.png)

	Before reclaiming a gateway, make sure all protected VLANs have been [disassociated](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans) from it.

3. Sur la page du périphérique, cliquez sur **Annuler unité** dans le menu déroulant Action pour accéder à la page de configuration du serveur.  

4. Dans l'écran de confirmation d'annulation du périphérique, démarrez le processus de récupération en cliquant sur **Continuer**. Si vous ne souhaitez pas poursuivre le processus, cliquez sur **Fermer**.

Pour les paires haute disponibilité (HA), ces actions devront être réalisées sur les deux périphériques.
