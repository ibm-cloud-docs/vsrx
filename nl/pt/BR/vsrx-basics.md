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

# Executando o básico do vSRX
O gateway do IBM® Cloud Juniper vSRX pode ser configurado usando uma sessão do console remoto por meio de SSH ou efetuando login na GUI de gerenciamento da web do Juniper.

**NOTA:** a configuração do vSRX fora de seu shell e interface pode produzir resultados inesperados e não é recomendada.

## Acessando o dispositivo usando SSH

Será possível acessar o vSRX usando o SSH por meio de um endereço IP público ou por meio de um endereço IP privado se você estiver na VPN SoftLayer:

1. Acesse a tela Detalhes do dispositivo de gateway e obtenha o IP do gateway público ou o IP do gateway privado.

  <img src="images/basics.png" alt="drawing" style="width: 700px;"/>

2. Clique no ícone de "olho" para exibir a senha do usuário administrativo. 

3. Execute o comando `ssh admin @<gateway-ip>`, em seguida, insira a senha do usuário administrativo.

**NOTA:** se você não vir o ícone de "olho", você poderá não ter permissão para visualizar a senha. Verifique as permissões de acesso com o proprietário da conta.

## Acessando o modo de configuração

É possível entrar no modo de configuração, depois que um shell tiver sido aberto para o vSRX, executando o comando `config`. É possível executar várias coisas nesse modo usando os comandos a seguir:

* `show`: visualizar configurações  
* `show | compare`: visualizar mudanças estagiadas
* `set`: estagiar mudanças
* `commit check`: verificar a sintaxe da configuração

Se estiver satisfeito com as mudanças, poderá confirmá-las na configuração ativa, executando os comandos `commit` e, em seguida, `save`.  

Para sair do modo de configuração, execute o comando `exit`.

## Acessando o dispositivo Usando a IU de gerenciamento da web do Juniper

A GUI de gerenciamento da web do Juniper foi configurada por padrão, com o certificado autoassinado gerado pelo vSRX. Somente https é ativado na porta 8443. É possível acessá-la em `https://gateway-ip:8443`.

![Detalhes de HA do dispositivo de gateway](images/vSRX-webui.png)

## Acessando o dispositivo usando o console do VIRSH

Também é possível acessar o vSRX por meio do sistema operacional do servidor gateway:

1. Efetue logon no servidor gateway executando o comando `ssh root@<server-ip>`.
2. Execute o comando `virsh list` para localizar o nome da VM do vSRX.
3. Execute o comando `virsh console <your vSRX VM name>`.

## Criando os usuários do sistema

Por padrão, o IBM Cloud Juniper vSRX é configurado com o acesso SSH para o nome de usuário `admin`. Os usuários adicionais podem ser incluídos com seu próprio conjunto de prioridades. Por exemplo:

```
set system login user ops class operator authentication encrypted-password <CYPHER>
```

Nesse exemplo, `ops` é o nome de usuário e `operador` é o nível de classe/permissão designado ao usuário.

As classes customizadas também podem ser definidas como opostas às predefinidas.

## Definindo o nome do host do vSRX

É possível configurar ou mudar o nome do host do vSRX usando o comando a seguir:

```
set system host-name <hostname>
```

## Configurando o DNS e o NTP

Para configurar a resolução do servidor de nomes e o NTP, execute os comandos a seguir:

```
set system name-server <DNS server>
set system ntp <NTP server>
```

## Mudando a senha raiz

É possível mudar a senha raiz executando o comando a seguir:

```
set system root-authentication plain-text-password
```

Isso solicita a inserção de uma nova senha, que é criptografada e armazenada na configuração, e não está visível.
