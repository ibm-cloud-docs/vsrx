---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: working, failover, codes, failure, cli

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

# Fonctionnement de la reprise en ligne
{: #working-with-failover}

La présente section s'applique uniquement si vos périphériques de passerelle Juniper vSRX sont configurés en mode haute disponibilité.
{: note}

Cette rubrique explique comment lancer la reprise en ligne depuis votre périphérique de passerelle principal vers une unité de secours, de sorte que l'ensemble du trafic du plan de contrôle et du plan de données soit acheminé via le périphérique de passerelle secondaire en cas de basculement.

Procédure :

1. Connectez-vous à votre périphérique de passerelle vSRX principal.

2. Entrez en mode d'interface CLI en exécutant la commande `cli` à l'invite de la console. Lorsque vous entrez en mode CLI, la console indique le rôle du noeud, à savoir `primary` ou `secondary`.

	Vérifiez que vous vous trouvé dans le noeud `primary`. Dans le cas contraire, quittez et connectez-vous à l'autre périphérique de passerelle vSRX de la paire.

2. Sur le périphérique de passerelle vSRX principal, exécutez la commande suivante :

	```
	show chassis cluster status
	```
	Le résultat devrait se présenter comme suit :

	```
	Monitor Failure codes:
		CS  Cold Sync monitoring        FL  Fabric Connection monitoring
		GR  GRES monitoring             HW  Hardware monitoring
		IF  Interface monitoring        IP  IP monitoring
		LB  Loopback monitoring         MB  Mbuf monitoring
		NH  Nexthop monitoring          NP  NPC monitoring
		SP  SPU monitoring              SM  Schedule monitoring
		CF  Config Sync monitoring

	Cluster ID: 2
	Node   Priority Status         Preempt Manual   	Monitor-failures

	Redundancy group: 0 , Failover count: 1
	node0  100      primary        no      no       None
	node1  1        secondary      no      no       None
	Redundancy group: 1 , Failover count: 1
	node0  100      primary        yes     no       None
	node1  1        secondary      yes     no       None

	{primary:node0}
	```

	Vérifiez que, pour les deux groupes de redondance, le même noeud est défini en tant que `primary`. Il est possible que différents noeuds soient définis en tant que rôle `primary` dans différents groupes de redondance. 
	
	Par défaut, le vSRX affecte la valeur `yes` à `Preempt` pour le groupe de redondance 1, et la valeur `no` au groupe de redondance 0. Cliquez sur [ce lien ![ Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.juniper.net/documentation/en_US/junos/topics/topic-map/security-chassis-cluster-redundancy-group-failover.html){:new_window} pour en savoir plus sur le comportement de préemption et de reprise en ligne.
	{: note}

3. Lancez la reprise en ligne en exécutant la commande ci-dessous dans l'invite de console :

	```
	request chassis cluster failover redundancy-group <redundancy group number> node <node number>
	```

	Sélectionnez le numéro de groupe de redondance approprié et le numéro de noeud résultant de la commande de l'étape 2. Pour effectuer la reprise en ligne des deux groupes de redondance, exécutez la commande deux fois, une fois pour chaque groupe.

4. Une fois le basculement terminé, vérifiez le résultat de la console. Le noeud doit maintenant apparaître comme `secondary`.

5. Connectez-vous à l'autre passerelle vSRX de la paire. Entrez à nouveau en mode CLI en exécutant la commande `cli` et vérifiez que la sortie de la console affiche `primary`.

Lorsque vous entrez en mode CLI dans votre périphérique de passerelle Juniper vSRX, la sortie indique `primary` du point de vue du plan de contrôle. Vérifiez toujours la sortie `show chassis cluster status` pour déterminer le périphérique de passerelle principal du point de vue du plan de données. Reportez-vous à la rubrique sur la [configuration par défaut de vSRX](/docs/infrastructure/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration) pour en savoir plus sur les groupes de redondance, ainsi que sur les plans de données et de contrôle.
{: tip}
