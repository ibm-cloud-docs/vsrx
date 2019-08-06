---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: basics, performing, accessing, ssh, device, gateway, configuration, mode, juniper, ui, dns, htp, password

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# Executando o básico do {{site.data.keyword.vsrx_full}}
{: #performing-ibm-cloud-juniper-vsrx-basics}

O gateway do {{site.data.keyword.vsrx_full}} pode ser configurado usando uma sessão do console remoto por meio de SSH ou efetuando login na GUI de gerenciamento da web do Juniper.

Configurar o vSRX fora de seu shell e interface pode produzir resultados inesperados e, portanto, não é recomendado.
{: note}

## Acessando o dispositivo usando SSH
{: #accessing-the-device-using-ssh}

Será possível acessar o vSRX usando o SSH por meio de um endereço IP público ou por meio de um endereço IP privado se você estiver na VPN SoftLayer:

1. Acesse a tela Detalhes do dispositivo de gateway e obtenha o IP do gateway público ou o IP do gateway privado.

  <img src="images/gw-sa-details.png" alt="drawing" style="width: 700px;"/>

2. Clique no ícone de "olho" para exibir a senha do usuário administrativo.

3. Execute o comando `ssh admin@<gateway-ip>`, em seguida, insira a senha do usuário administrativo.

Se não vir o ícone de "olho", talvez você não tenha permissão para visualizar a senha. Verifique as permissões de acesso com o proprietário da conta.
{: note}

## Acessando o modo de configuração
{: accessing-the-configuration-mode}

É possível entrar no modo de configuração, depois que um shell tiver sido aberto para o vSRX, executando o comando `config`. É possível executar várias coisas nesse modo usando os comandos a seguir:

* `show`: visualizar configurações  
* `show | compare`: visualizar mudanças estagiadas
* `set`: estagiar mudanças
* `commit check`: verificar a sintaxe da configuração

Se estiver satisfeito com as mudanças, poderá confirmá-las na configuração ativa, executando os comandos `commit` e, em seguida, `save`.  

Para sair do modo de configuração, execute o comando `exit`.

## Acessando o dispositivo Usando a IU de gerenciamento da web do Juniper
{: #accessing-the-device-using-the-juniper-web-management-ui}

A GUI de gerenciamento da web do Juniper foi configurada por padrão, com o certificado autoassinado gerado pelo vSRX. Somente https é ativado na porta 8443. É possível acessá-la em `https://gateway-ip:8443`.

![Detalhes de HA do dispositivo de gateway](images/vSRX-webui.png)

## Criando os usuários do sistema
{: #creating-system-users}

Por padrão, o {{site.data.keyword.vsrx_full}} é configurado com o acesso SSH para o nome de usuário `admin`. Os usuários adicionais podem ser incluídos com seu próprio conjunto de prioridades. Por exemplo:

```
set system login user ops class operator authentication encrypted-password <CYPHER>
```

Nesse exemplo, `ops` é o nome de usuário e `operador` é o nível de classe/permissão designado ao usuário.

As classes customizadas também podem ser definidas como opostas às predefinidas.

## Definindo o nome do host do vSRX
{: #defining-the-vsrx-hostname}

É possível configurar ou mudar o nome do host do vSRX usando o comando a seguir:

```
set system host-name <hostname>
```

## Configurando o DNS e o NTP
{: #configuring-dns-and-ntp}

Para configurar a resolução do servidor de nomes e o NTP, execute os comandos a seguir:

```
set system name-server <DNS server>
set system ntp <NTP server>
```

## Mudando a senha raiz
{: #changing-the-root-password}

É possível mudar a senha raiz executando o comando a seguir:

```
set system root-authentication plain-text-password
```

Isso solicita a inserção de uma nova senha, que é criptografada e armazenada na configuração, e não está visível.
