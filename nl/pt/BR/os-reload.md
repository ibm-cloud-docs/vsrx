---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: reloading, os, upgrading, kvm, ha, standalone

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

# Recarregando o S.O.
{: #reloading-the-os}

O processo de recarregamento do sistema operacional é usado para reconstruir um servidor de gateway. O processo executa as ações a seguir:

* Recarregar o sistema operacional do host do servidor
* Instalar o KVM no sistema operacional
* Criar uma VM do vSRX no KVM
* Reconfigurar o vSRX com a configuração padrão para o IBM® Cloud

Geralmente, o processo requer 1 hora e 40 minutos para ser concluído. Gateways independentes estarão fora de serviço durante esse período. Para os gateways de alta disponibilidade (HA) do Juniper, ao recarregar o S.O. em um dos servidores, o vSRX executará failover em outro servidor no cluster e continuará a processar o tráfego de dados. Após a conclusão do recarregamento, o servidor se unirá novamente ao cluster.

Para recarregar ou recriar o cluster com sucesso em um vSRX de alta disponibilidade:

* A senha raiz para o Gateway vSRX provisionado deve corresponder à senha raiz definida no portal do vSRX. A senha do portal foi definida quando o Gateway foi provisionado pela primeira vez e pode não corresponder à senha atual do Gateway. Se ela tiver sido mudada após o provisionamento inicial, use o SSH para se conectar ao Gateway vSRX e mudar a senha raiz para gerar correspondência. Uma vez que as senhas correspondam, será possível prosseguir com a operação de cluster Recarregar ou Reconstruir o sistema operacional.

  <img src="images/gw-vsrx-password.png" alt="desenho" style="width: 700px;"/>

* **NÃO** execute um recarregamento do sistema operacional em ambos os servidores do gateway Altamente Disponível ao mesmo tempo.

A execução de um recarregamento do sistema operacional em ambos os servidores do gateway de alta disponibilidade ao mesmo tempo destruirá o cluster vSRX e fará com que o gateway fique fora de serviço. Se o cluster do vSRX for destruído, a opção **Reconstruir cluster** deverá ser usada (detalhada a seguir) para reprovisionar o vSRX e recriar o cluster de HA.
{: important}

## Executando um recarregamento de S.O.
{: #performing-an-os-reload}

Para recarregar o S.O. para um servidor gateway, execute o procedimento a seguir:

1. [Acesse a tela Dispositivo de gateway](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) no Portal do cliente e navegue para a página Detalhes do gateway selecionando o nome do gateway desejado.

  <img src="images/gw-sa-details.png" alt="drawing" style="width: 700px;"/>

2. Clique no nome do servidor no Painel de hardware.

  ![Servidor de hardware](images/os_hardware.png)

3. Na página do dispositivo, clique em **Recarregamento de sistema operacional** no menu suspenso Ação para acessar a página Configuração do servidor.

  ![Detalhes do dispositivo](images/os_device_page.png)

4. Na página Configuração do servidor, é possível configurar e iniciar o recarregamento. Se você estiver recarregando de um S.O. diferente, clique em **Editar** ao lado de **Sistema operacional**, selecione **Juniper** e, em seguida, selecione uma das opções do Juniper vSRX 15.x Standard. Ao concluir a modificação das configurações, selecione **Recarregar configuração acima** para continuar.

5. A tela Detalhes do recarregamento do S.O. é exibida. Revise as configurações escolhidas e clique em **Editar configurações** se mudanças forem necessárias. Caso contrário, clique em **Avançar** para continuar.

6. Na tela Confirmação de recarregamento do S.O., concorde com os termos do Contrato de Prestação de Serviços Principal e, em seguida, comece o processo de recarregamento do S.O. clicando em **Confirmar recarregamento do S.O.**. Se não desejar continuar com o recarregamento, clique em **Cancelar**.

## Reconstruindo um cluster de HA do vSRX
{: #rebuilding-an-ha-vsrx-cluster}

Para reconstruir um dos clusters de HA do vSRX, execute o procedimento a seguir:

1. [Acesse a tela Dispositivos de gateway](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) no Portal do cliente e navegue para a página Detalhes do gateway selecionando o nome do gateway de HA desejado.

2. Clique no menu suspenso **Ações** e selecione **Reconstruir o cluster**.

3. Leia atentamente a mensagem de aviso. A operação para reconstruir um cluster é destrutiva. Se desejar continuar, salve sua configuração do vSRX antes de clicar em **Reconstruir** para iniciar o processo.

  ![Confirmar a reconstrução do cluster](images/rebuild_cluster_confirm.png)
