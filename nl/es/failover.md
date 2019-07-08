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

# Cómo trabajar con la migración tras error
{: #working-with-failover}

Esta sección solo se aplica si los dispositivos de pasarela Juniper vSRX se suministran en modalidad de alta disponibilidad.{: note}

En este tema se describe cómo iniciar una migración tras error desde el dispositivo de pasarela primario a un dispositivo de copia de seguridad, de modo que todo el tráfico de control y del plano de datos se direccione mediante el dispositivo de pasarela secundario después de la migración tras error.

Para ello, siga el procedimiento siguiente:

1. Inicie una sesión en el dispositivo de pasarela vSRX primario.

2. Entre en modalidad de CLI ejecutando el mandato `cli` en el indicador de la consola. Cuando entra en modalidad de CLI, la consola muestra el rol del nodo, que puede ser `primary` o `secondary`.

	Asegúrese de que está en el nodo `primary`. Si no lo está, salga e inicie sesión en el otro dispositivo de pasarela vSRX del par.

2. En el dispositivo de pasarela vSRX primario, ejecute el mandato:

	```
	show chassis cluster status
	```
	La salida debería parecerse
a la siguiente:

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

	Asegúrese de que se ha establecido el mismo nodo como `primary` para los dos grupos de redundancia. Es posible que distintos nodos se establezcan como el rol de `primary` en distintos grupos de redundancia. 
	
	De forma predeterminada, vSRX establece `Preempt` a `yes` para el Grupo de redundancia 1 y a `no` para el Grupo de redundancia 0. Consulte [este enlace ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.juniper.net/documentation/en_US/junos/topics/topic-map/security-chassis-cluster-redundancy-group-failover.html){:new_window} para obtener más información sobre la preferencia y el comportamiento de migración tras error.
	{: note}

3. Inicie la migración tras error ejecutando el mandato siguiente en el indicador de la consola:

	```
	request chassis cluster failover redundancy-group <redundancy group number> node <node number>
	```

	Seleccione el número de grupo de redundancia y el número de nodo adecuados de la salida del mandato del paso dos. Para realizar una migración tras error de ambos grupos de redundancia, ejecute el mandato anterior dos veces, uno para cada grupo.

4. Una vez que haya finalizado la migración tras error, verifique la salida de la consola. Se debería mostrar como `secondary`.

5. Inicie una sesión en la otra pasarela vSRX del par. Vuelva a entrar en modalidad de CLI con el mandato `cli` y verifique que la salida de la consola se muestra como `primary`.

Cuando entra en la modalidad de CLI en el dispositivo de pasarela Juniper vSRX, la salida se mostrará como `primary` desde la perspectiva del plano de control. Compruebe siempre la salida de `show chassis cluster status` para
determinar qué dispositivo de pasarela es el primario desde la perspectiva del plano de datos. Consulte el apartado sobre [Configuración
predeterminada de vSRX](/docs/infrastructure/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration) para obtener más información sobre los grupos de redundancia, así como los planos de control y de datos.
{: tip}
