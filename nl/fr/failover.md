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

# Fonctionnement de la reprise en ligne
{: #working-with-failover}

**Remarque :** La présente section s'applique uniquement si vos périphériques de passerelle Juniper vSRX sont configurés en mode haute disponibilité.

Cette rubrique explique comment lancer la reprise en ligne depuis votre périphérique de passerelle principal vers une unité de secours, de sorte que l'ensemble du trafic du plan de contrôle et du plan de données soit acheminé via le périphérique de passerelle secondaire en cas de basculement.

Procédure :

1. Connectez-vous à votre périphérique de passerelle vSRX principal.

2. Entrez en mode d'interface CLI en exécutant la commande `cli` à l'invite de la console. Lorsque vous entrez en mode CLI, la console indique le rôle du noeud, à savoir `primary` ou `secondary`.

	Ensure that you are in the `primary` node. If you are not, exit and login to the other vSRX gateway device of the pair.

2. Sur le périphérique de passerelle vSRX principal, exécutez la commande suivante :

	```
	show chassis cluster status
	```
	The output should be similar to the following:

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

	Ensure that for both redundancy groups, the same node is set as `primary`. It is possible for different nodes to be set as the `primary` role in different redundancy groups.

3. Lancez la reprise en ligne en exécutant la commande ci-dessous dans l'invite de console :

	```
	request chassis cluster failover redundancy-group <redundancy group number> node <node number>
	```

	Select the appropriate redundancy group number and node number from the output of the command in step two. To failover both redundancy groups, execute the previous command twice, one for each group.

4. Une fois le basculement terminé, vérifiez le résultat de la console. Le noeud doit maintenant apparaître comme `secondary`.

5. Connectez-vous à l'autre passerelle vSRX de la paire. Entrez à nouveau en mode CLI en exécutant la commande `cli` et vérifiez que la sortie de la console affiche `primary`.

**Remarque :** Lorsque vous entrez en mode CLI dans votre périphérique de passerelle Juniper vSRX, la sortie indique `primary` du point de vue du plan de contrôle. Vérifiez toujours la sortie `show chassis cluster status` pour déterminer le périphérique de passerelle principal du point de vue du plan de données. Reportez-vous à la rubrique sur la [configuration par défaut de vSRX](/docs/infrastructure/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration) pour en savoir plus sur les groupes de redondance, ainsi que sur les plans de données et de contrôle.
