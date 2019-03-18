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

# Recarregando e migrando o S.O.
{: #reloading-an-migrating-the-os}

O processo de recarregamento do S.O. é usado para reconstruir um servidor gateway. O processo executa as ações a seguir:

* Recarregar o sistema operacional do host do servidor
* Instalar o KVM no sistema operacional
* Criar uma VM do vSRX no KVM
* Reconfigurar o vSRX com a configuração padrão para o IBM® Cloud

Geralmente, o processo requer 1 hora e 40 minutos para ser concluído. Gateways independentes estarão fora de serviço durante esse período. Para os gateways de alta disponibilidade (HA) do Juniper, ao recarregar o S.O. em um dos servidores, o vSRX executará failover em outro servidor no cluster e continuará a processar o tráfego de dados. Após a conclusão do recarregamento, o servidor se unirá novamente ao cluster.

**CUIDADO:** se você já estiver executando um cluster de HA do Juniper vSRX, não execute um recarregamento de S.O. nos dois servidores do gateway de HA ao mesmo tempo. Ao fazer isso, o cluster do vSRX será destruído e o gateway ficará fora de serviço. Se o cluster do vSRX for destruído, a opção **Reconstruir cluster** deverá ser usada (detalhada a seguir) para reprovisionar o vSRX e recriar o cluster de HA.

## Executando um recarregamento de S.O.
Para recarregar o S.O. para um servidor gateway, execute o procedimento a seguir:

1. [Acesse a tela Dispositivo de gateway](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) no Portal do cliente e navegue para a página Detalhes do gateway selecionando o nome do gateway desejado.

2. Clique no nome do servidor no Painel de hardware.
![Servidor de hardware](images/os_hardware.png)

3. Na página do dispositivo, clique em **Recarregamento do S.O.** no menu suspenso Ação para acessar a página Configuração do servidor.
![Detalhes do dispositivo](images/os_device_page.png)

4. Na página Configuração do servidor, é possível configurar e iniciar o recarregamento. Se você estiver recarregando de um S.O. diferente, clique em **Editar** ao lado de **Sistema operacional**, selecione **Juniper** e, em seguida, selecione uma das opções do Juniper vSRX 15.x Standard. Ao concluir a modificação das configurações, selecione **Recarregar configuração acima** para continuar.

5. A tela Detalhes do recarregamento do S.O. é exibida. Revise as configurações escolhidas e clique em **Editar configurações** se mudanças forem necessárias. Caso contrário, clique em **Avançar** para continuar.

6. Na tela Confirmação de recarregamento do S.O., concorde com os termos do Contrato de Prestação de Serviços Principal e, em seguida, comece o processo de recarregamento do S.O. clicando em **Confirmar recarregamento do S.O.**. Se não desejar continuar com o recarregamento, clique em **Cancelar**.

## Migrando de um servidor Vyatta/VRA para um Juniper vSRX usando o recarregamento do S.O.
Se você estiver recarregando um servidor Vyatta independente, então, um Juniper vSRX independente será provisionado assim que o recarregamento do S.O. for concluído. Os mesmos endereços IP do gateway serão usados e a senha para o usuário raiz no servidor host (assim como a senha para os usuários administrativo e raiz no vSRX) será reconfigurada.

Se você estiver recarregando os servidores Vyatta de alta disponibilidade, deverá executar um recarregamento de
S.O. em ambos os servidores de hardware. Isso instala o Ubuntu 16.04. Em seguida, use a opção Reconstruir cluster (detalhada na seção a seguir) para provisionar o vSRX e criar o cluster de HA. Tal como com um vSRX independente, os mesmos endereços IP do gateway serão usados e a senha para o usuário raiz no servidor host (assim como a senha para os usuários administrativo e raiz no vSRX) será reconfigurada.

**CUIDADO:** não execute um Recarregamento do S.O. em apenas um servidor do cluster de HA do Vyatta. Ter dois sistemas operacionais diferentes em um único cluster de HA do gateway não é suportado.

## Reconstruindo um cluster de HA do vSRX
Para reconstruir um dos clusters de HA do vSRX, execute o procedimento a seguir:

1. [Acesse a tela Dispositivos de gateway](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) no Portal do cliente e navegue para a página Detalhes do gateway selecionando o nome do gateway de HA desejado.

2. Clique em **Reconstruir cluster** no Painel do vSRX.
![Reconstruir cluster](images/rebuild_cluster.png)

3. Leia atentamente a mensagem de aviso. A operação para reconstruir um cluster é destrutiva. Se desejar continuar, salve a configuração do vSRX antes de clicar em **Reconstruir** para iniciar o processo.
![Confirmar reconstrução do cluster](images/rebuild_cluster_confirm.png)
