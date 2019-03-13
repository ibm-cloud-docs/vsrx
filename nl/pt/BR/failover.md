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

# Trabalhando com failover
**NOTA:** esta seção é aplicável apenas se os dispositivos de gateway Juniper vSRX são provisionados no modo de alta disponibilidade.

Este tópico descreve como iniciar o failover do dispositivo de gateway primário para um dispositivo de backup, de modo que todo o tráfego do plano de controle e de dados seja roteado por meio do dispositivo de gateway secundário após o failover.

Para fazer isso, execute o procedimento a seguir:

1. Efetue login no dispositivo de gateway vSRX primário.

2. Entre no modo de CLI executando o comando `cli` no prompt do console. Ao entrar no modo de CLI, o console exibe a função do nó, `primary` ou `secundary`.

	Certifique-se de que esteja no nó `primary`. Se não estiver, saia e efetue login no outro dispositivo de gateway vSRX do par.

2. No dispositivo de gateway vSRX primário, execute o comando:

	```
	show chassis cluster status
	```
	A saída deve ser semelhante à seguinte:

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

	Assegure-se de que, para os dois grupos de redundância, o mesmo nó seja configurado como `primary`. É possível que diferentes nós sejam configurados como a função `primary` em diferentes grupos de redundância.

3. Inicie o failover executando o seguinte comando no prompt do console:

	```
	request chassis cluster failover redundancy-group <redundancy group number> node <node number>
	```

	Selecione o número do grupo de redundância e o número do nó apropriados da saída do comando na etapa dois. Para executar failover nos dois grupos de redundância, execute o comando anterior duas vezes, uma para cada grupo.

4. Após a conclusão do failover, verifique a saída do console. Agora, ela deve ser listada como `secondary`.

5. Efetue login no outro gateway vSRX do par. Entre no modo de CLI, executando novamente o comando `cli` e, em seguida, verifique se a saída do console é mostrada como `primary`.

**NOTA:** ao entrar no modo de CLI no dispositivo de gateway Juniper vSRX, a saída será mostrada como `primary` da perspectiva do plano de controle. Sempre marque a saída `show chassis cluster status` para determinar qual dispositivo de gateway é primário da perspectiva do plano de dados. Consulte [Configuração padrão do vSRX](vsrx-default-config.html) para saber mais sobre os grupos de redundância, bem como sobre os planos de controle e de dados.
