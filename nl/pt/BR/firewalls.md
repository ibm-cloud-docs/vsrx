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

# Trabalhando com firewalls
O IBM® Cloud Juniper vSRX usa o conceito de zonas de segurança, em que cada interface do vSRX é mapeada para uma "zona" para manipulação de firewalls stateful. Os firewalls stateless são controlados por filtros de firewall.

As políticas são usadas para permitir e bloquear o tráfego entre essas zonas definidas e as regras definidas aqui são stateful.

No IBM Cloud, um vSRX é projetado para ter quatro zonas de segurança diferentes:

| Zona                     | Interface independente | Interface HA |
| :---                     |        :----:        |         ---: |
| SL-Private (não identificado)    | ge-0/0/0.0           | reth0.0      |
| SL-Public (não identificado)     | ge-0/0/1.0           | reth1.0      |
| Customer-Private (identificado)| ge-0/0/0.1           | reth2.1      |
| Customer-Public (identificado) | ge-0/0/1.1           | reth3.1      |

## Políticas de zona
Para configurar um firewall stateful, execute o procedimento a seguir:

1. Crie zonas de segurança e designe as respectivas interfaces:

	Cenário independente:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces ge-0/0/1.1
	```
	Cenário de alta disponibilidade:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces reth2.1
	```
2. Defina a política e as regras entre duas zonas diferentes.

	O exemplo a seguir ilustra o tráfego de ping da zona `Customer-Private` para a `Customer-Public`:

	```
	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP match source-address any destination-address any application junos-icmp

	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP then permit
	```

Estes são alguns dos atributos que podem ser definidos nas políticas:

* Endereços de origem
* Endereços de destino
* Aplicativos
* Ação (permitir/negar/rejeitar/contar/registrar)

Como essa é uma operação stateful, não há necessidade de permitir pacotes de retorno (neste caso, as respostas de eco).

Use os seguintes comandos para permitir o tráfego que é direcionado para o vSRX:

Caso independente:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.0 host-inbound-traffic system-services all
```
Caso HA:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.0 host-inbound-traffic system-services all
```

Para permitir protocolos, como o OSPF ou o BGP, use o comando a seguir:

Caso independente:
```
set security zones security-zone trust interfaces ge-0/0/0.0 host-inbound-traffic protocols all
```
Caso HA:
```
set security zones security-zone trust interfaces reth2.0 host-inbound-traffic protocols all
```

## Filtros de firewall
Por padrão, o IBM Cloud Juniper vSRX permite ping, SSH e HTTPS para si mesmo e descarta todos os outros tráfegos aplicando o filtro `PROTECT-IN` à interface `lo`.

Para configurar um novo firewall stateless, execute o procedimento a seguir:

1. Crie o filtro e o prazo do firewall (o filtro a seguir permitirá apenas o ICMP e descartará todos os outros tráfegos)
	```
	set firewall filter ALLOW-PING term ICMP from protocol icmp
	set firewall filter ALLOW-PING term ICMP then accept
	```

2. Aplique a regra de filtragem à interface (o comando a seguir aplicará o filtro a todos os tráfegos de rede privada)
	```
	set interfaces ge-0/0/0 unit 0 family inet filter input ALLOW-PING
	```
