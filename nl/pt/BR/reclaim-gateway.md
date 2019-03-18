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

# Recuperando um gateway
{: #reclaiming-a-gateway}

Execute o seguinte procedimento para recuperar o gateway:

1. [Acesse a tela Dispositivos de gateway](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) no Portal do cliente e navegue para a página Detalhes do gateway selecionando o nome do gateway desejado.

2. Clique no nome do servidor no Painel de hardware.

	![Servidor de hardware](images/os_hardware.png)

	Antes de recuperar um gateway, certifique-se de que todas as VLANs protegidas tenham sido [desassociadas](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans) dele.

3. Na página do dispositivo, clique em **Cancelar dispositivo** no menu suspenso Ação para acessar a página Configuração do servidor.  

4. Na tela de confirmação Cancelar dispositivo, inicie o processo de recuperação clicando em **Continuar**. Se não desejar continuar com a recuperação, clique em **Fechar**.

Para os pares de HA, essas ações precisarão ser executadas nos dois dispositivos.
