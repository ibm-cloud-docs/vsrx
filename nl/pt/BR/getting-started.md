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

# Introdução

Para iniciar com o gateway do IBM® Cloud Juniper vSRX, primeiro determine se a sua conta está vinculada ao IBM Cloud.

## Antes de Começar

Para descobrir se você tem uma conta vinculada, navegue para o [Portal do cliente ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){: new_window} no navegador e efetue login. Se a conta estiver desvinculada, você verá um botão **Saiba mais sobre o Bluemix** na parte superior direita.

## Etapas para fazer o pedido

É possível pedir o dispositivo de gateway usando um destes métodos:

**NOTA:** para obter uma lista de Limitações conhecidas com o gateway do IBM Cloud Juniper vSRX, consulte [o tópico Limitações conhecidas](known-limitations.html).

### Fazendo o pedido com uma conta vinculada
Se a conta estiver vinculada, siga este procedimento:

1.	Abra o [console do IBM Cloud![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.bluemix.net/){: new_window} e efetue login na conta.
2.	Na navegação à esquerda, selecione **Infraestrutura > Rede > Dispositivos de gateway**.
3.	Na lista **Dispositivos de gateway**, clique em **Criar um gateway**.
4. Na página **Pedido**, escolha um **Nome de host** e **Domínio**.
5. Selecione a opção **Par de alta disponibilidade**, se desejado.

	<img src="images/linked_order.png" alt="drawing" style="width: 700px;"/>

5. Em seguida, selecione a **Localização** e o **Pod** associado e, então, escolha o **Servidor** e a quantia desejada de **RAM**.

	**NOTA:** caso haja planos de usar um servidor com diversos núcleos de processador dual, deve-se selecionar **Intel Xeon 5120** como o tipo de servidor.

	<img src="images/linked_server.png" alt="drawing" style="width: 600px;"/>

6. Selecione uma chave SSH se desejar usá-la para autenticar o acesso ao novo gateway.
7. Em **Imagem**, selecione **Juniper vSRX 15.x (até 1 Gbps) Standard** para um servidor de processador único ou **Juniper vSRX 15.x (até 10 Gbps) Standard** para um servidor de processador dual.
8. Selecione quaisquer complementos opcionais, inclua quaisquer **Discos de armazenamento** adicionais e escolha a **Velocidade da porta de uplink** desejada.
8. Revise as seleções no **Resumo do pedido** e, em seguida, leia e concorde com os Termos de software de terceiros.
9. Finalmente, clique em **Provisionar**.

### Fazendo o pedido com uma conta desvinculada
Se a conta estiver desvinculada, siga este procedimento:

1.	Abra o [Portal do cliente ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://control.softlayer.com/){: new_window} e efetue login na conta.
2.	Na navegação do Portal do Cliente, selecione **Rede > Dispositivo de Gateways**.
3.	Na lista **Dispositivos de gateway**, clique em **Pedir gateway**.
4.	Na página **Pedido**, selecione o data center desejado no menu suspenso e, em seguida, escolha o tipo desejado de hardware do servidor no qual o Juniper vSRX será provisionado. 

	**NOTA:** caso haja planos de usar um servidor com diversos núcleos de processador dual, deve-se selecionar **Intel Xeon 5120** como o tipo de servidor.
	
5.	Na página **Pedido**, selecione a opção **Par de alta disponibilidade**, se desejado e, em seguida, selecione o tamanho da **Memória**.
6. 	Em seguida, clique na guia **Juniper** em **Sistema operacional**, selecione **Juniper vSRX 15.x (até 1 Gbps) Standard** para um servidor de processador único ou **Juniper vSRX 15.x (até 10 Gbps) Standard** para um servidor de processador dual.
7. 	Finalmente, selecione a velocidade de uplink de rede desejada.
8.	Revise as seleções e, então, clique em **Incluir no pedido**. O pedido será verificado automaticamente.
9.	Na página **Finalizar compra**, se você já tem VLANs no data center selecionado, selecione as VLANs de back-end que deseja proteger. Certifique-se de:
	* Fornecer um nome de host e um nome de domínio para o servidor
	* Selecionar uma chave SSH para a autenticação de acesso, se desejado
	* Marcar todas as caixas para os termos de serviço do IBM Cloud e os termos de software de terceiros
10. Clique em **Enviar pedido**.

## Qual o próximo?
Após a aprovação do pedido, o provisionamento do vSRX será iniciado automaticamente. Quando o processo de provisionamento estiver concluído, o gateway aparecerá na lista **Dispositivos de gateway**.

Clique no nome do gateway para abrir a página **Detalhes do gateway**. Você localizará os endereços IP, o nome de usuário de login e as senhas para o dispositivo.

<img src="images/after_order.png" alt="drawing" style="width: 700px;"/>
