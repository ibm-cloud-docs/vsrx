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

# Introdução ao gateway do IBM Cloud Juniper vSRX
{: #getting-started}

Para iniciar com o gateway do IBM® Cloud Juniper vSRX, primeiro determine se a sua conta está vinculada ao IBM Cloud.

Para descobrir se você tem uma conta vinculada, navegue para o [Portal do cliente ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){: new_window} no navegador e efetue login. Se sua conta estiver vinculada, **Saiba mais sobre o Bluemix.** não será exibido na parte superior direita.

## Etapas para fazer o pedido
{: #steps-for-ordering}

É possível pedir o dispositivo de gateway usando um destes métodos:

Para obter uma lista de limitações conhecidas com o gateway do IBM Cloud Juniper vSRX, consulte o
[tópico Limitações
conhecidas](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx).
{: note}

### Fazendo o pedido com uma conta vinculada
{: #ordering-with-a-linked-account}

Se a conta estiver vinculada, siga este procedimento:

1. Em seu navegador, abra a página Dispositivos de gateway no [Catálogo do Cloud ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/gen1/infrastructure/provision/gateway){: new_window} e efetue login em sua conta.

  Também é possível acessar essa página efetuando login no [Console da IU do IBM Cloud ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com) e selecionando **Infraestrutura clássica > Rede > Dispositivo de gateway**.
Como alternativa, no [Catálogo do IBM Cloud ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/catalog), selecione a categoria **Rede** e, em seguida, escolha o quadro **Dispositivo de gateway**.

2. Escolha **Juniper vSRX (até 1 Gbps)** ou **Juniper vSRX (até 10 Gbps)** em **Fornecedor de gateway**.

3. Na seção **Dispositivo de gateway**, insira suas informações de nome de **Domínio** e **Nome de host**. Esses campos já estarão preenchidos com informações padrão, portanto, certifique-se de que os valores estejam corretos.

	<img src="images/linked_order.png" alt="drawing" style="width: 700px;"/>

4. Marque a opção **Alta disponibilidade**, se desejar, e selecione o **Local** desejado de seu data center e o **Pod** específico que deseja no menu suspenso.

  Somente pods que já possuem uma VLAN associada serão exibidos aqui. Se desejar provisionar seu Dispositivo de gateway em um pod que não está listado, crie primeiro uma VLAN nele.
  {: note}

	<img src="images/linked_server.png" alt="drawing" style="width: 600px;"/>

4. Na seção **Configuração**, escolha seu processador selecionando suas chaves RAM e SSH (se desejar usá-lo para autenticar o acesso ao seu novo Gateway).

  O processador apropriado será escolhido para você com base na versão da licença selecionada na etapa dois. No entanto, é possível escolher diferentes configurações de RAM.
  {: note}

5. Na seção **Discos de armazenamento**, escolha as opções que atendem aos seus requisitos de armazenamento.

  As opções RAID0 e RAID1 estão disponíveis para proteção adicional contra perda de dados, assim como hot spares (componentes de backup que podem ser colocados em serviço imediatamente quando um componente primário falha).
  {: note}

  É possível ter até quatro discos por vSRX. O "tamanho do disco" com uma configuração RAID é o tamanho do disco utilizável, pois as configurações RAID são espelhadas.
  {: note}

  Reserve mais do que a configuração de disco padrão se planeja executar diagnósticos de rede que gerem logs detalhados.
  {: tip}

6. Na seção **Interface de rede**, selecione suas **Velocidades da porta de uplink**. A seleção padrão é uma interface única, mas também existem opções redundantes e somente privadas. Escolha a que melhor atenda às suas necessidades.

  A seção **Complementos** da Interface de rede permite que você selecione um endereço IPv6, se necessário, e mostra quaisquer opções padrão adicionais incluídas.

8. Revise suas seleções, verifique se leu os Contratos de Prestação de Serviço de Terceiros e clique em **Criar**. O pedido é verificado automaticamente.

Após a aprovação de seu pedido, o fornecimento de seu Gateway IBM Cloud Juniper vSRX será iniciado automaticamente. Após a conclusão do processo de provisionamento, o novo vSRX aparecerá na página de lista Dispositivos de gateway. Clique no nome do gateway para abrir a página Detalhes do gateway. Você localizará os endereços IP, o nome do usuário de login e a senha para o dispositivo.  

Lembre-se de que, ao solicitar e configurar seu gateway por meio do Catálogo do IBM Cloud, também será preciso configurar o próprio dispositivo com as mesmas configurações.
{: tip}

### Fazendo o pedido com uma conta desvinculada
{: #ordering-with-a-unlinked-account}

Se a conta estiver desvinculada, siga este procedimento:

1.	Abra o [Portal do cliente ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){: new_window} e efetue login na conta.
2.	Na navegação do Portal do Cliente, selecione **Rede > Dispositivo de Gateways**.
3.	Na lista **Dispositivos de gateway**, clique em **Pedir gateway**.
4.	Na página **Pedido**, selecione o data center desejado no menu suspenso e, em seguida, escolha o tipo desejado de hardware do servidor no qual o Juniper vSRX será provisionado.

	Se você planeja usar um servidor com diversos núcleos de processador dual, é necessário selecionar **Intel Xeon 5120** como o tipo de servidor.
  {: note}

5.	Na página **Pedido**, selecione a opção **Par de alta disponibilidade**, se desejado e, em seguida, selecione o tamanho da **Memória**.
6. 	A seguir, clique na guia **Juniper** em **Sistema operacional**, selecione **Juniper vSRX (até 1 Gbps) Standard** para obter um único servidor de processador ou **Juniper vSRX (até 10 Gbps) Standard** para obter um servidor de processador dual.
7. 	Finalmente, selecione a velocidade de uplink de rede desejada.
8.	Revise as seleções e, então, clique em **Incluir no pedido**. O pedido será verificado automaticamente.
9.	Na página **Finalizar compra**, se você já tem VLANs no data center selecionado, selecione as VLANs de back-end que deseja proteger. Certifique-se de:
	* Forneça um nome de host e de domínio para o seu servidor.
	* Selecione uma chave SSH para a autenticação do acesso, se desejar.
	* Marque todas as caixas para os termos de serviço do IBM Cloud e os Termos de Software de Terceiros.
10. Clique em **Enviar pedido**.

## Qual o próximo?
{: #what-s-next-}

Após a aprovação do pedido, o provisionamento do vSRX será iniciado automaticamente. Quando o processo de provisionamento estiver concluído, o gateway aparecerá na lista **Dispositivos de gateway**.

Clique no nome do gateway para abrir a página **Detalhes do gateway**. Você localizará os endereços IP, o nome de usuário de login e as senhas para o dispositivo.

<img src="images/after_order.png" alt="drawing" style="width: 700px;"/>
