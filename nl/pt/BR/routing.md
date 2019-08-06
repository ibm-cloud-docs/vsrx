---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: working, routing, static, default, creating, ospf, bgp

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

# Trabalhando com roteamento
{: #working-with-routing}

O {{site.data.keyword.vsrx_full}} é baseado no `JunOS`, fornecendo acesso à pilha de roteamento Juniper completa.

##Roteamento estático
{: #static-routing}

Para configurar as rotas estáticas, execute os comandos a seguir:

###Configurando uma rota padrão
{: #setting-a-default-route}

```
set routing-options static route 0/0 next-hop <Gateway IP>
```

### Criando uma rota estática
{: #creating-a-static-route}
```
set routing-options static route <PREFIX/MASK> next-hop <Gateway IP>
```  

###Roteamento de OSPF básico
{: #basic-ospf-routing}

Para configurar o roteamento de OSPF básico apenas usando a área 0, execute os seguintes comandos usando a autenticação md5:

```
set protocols ospf area 0 interface ge-0/0/1.0 authentication md5 0 key <KEY>
```

### Roteamento de BGP básico
{: #basic-bgp-routing}

Para configurar o roteamento de BGP básico, primeiro defina o AS local:

```
set routing-options autonomous-system 65001
```

Em seguida, configure o vizinho do BGP e seus atributos de sessão:

```
set protocols bgp group CUSTOMER local-address 1.1.1.1
set protocols bgp group CUSTOMER family inet unicast
set protocols bgp group CUSTOMER family inet6 unicast
set protocols bgp group CUSTOMER peer-as 65002
set protocols bgp group CUSTOMER neighbor 2.2.2.2
```

Nesse exemplo, o BGP é configurado para o seguinte:

* Usar o endereço IP de origem do `1.1.1.1` para estabelecer a sessão
* Negociar as duas famílias unicast IPv4 e IPv6
* Colocar no mesmo nível de um vizinho que pertence a `AS 65002`
* Colocar no mesmo nível do IP do vizinho `2.2.2.2`

Configurações adicionais podem ser localizadas no
[website
do Juniper ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.juniper.net/documentation/en_US/junos11.4/information-products/topic-collections/config-guide-routing/config-guide-routing.pdf){: new_window}.
