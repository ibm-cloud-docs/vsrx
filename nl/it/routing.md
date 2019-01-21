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

# Utilizzo dell'instradamento
IBM® Cloud Juniper vSRX si basa su `JunOS`, fornendoti l'accesso allo stack di instradamento Juniper completo.

##Instradamento statico
Per configurare gli instradamenti statici, immetti i seguenti comandi:

###Configurazione di un instradamento predefinito
```
set routing-options static route 0/0 next-hop <Gateway IP>
```

### Creazione di un instradamento statico
```
set routing-options static route <PREFIX/MASK> next-hop <Gateway IP>
```  

###Instradamento OSPF di base
Per configurare l'instradamento OSPF di base, utilizzando solo l'area 0, immetti i seguenti comandi utilizzando l'autenticazione md5:

```
set protocols ospf area 0 interface ge-0/0/1.0 authentication md5 0 key <KEY>
```

### Instradamento BGP di base
Per configurare l'instradamento BGP di base, definisci prima il SO locale:

```
set routing-options autonomous-system 65001
```

Quindi configura il router adiacente BGP e i relativi attributi della sessione:

```
set protocols bgp group CUSTOMER local-address 1.1.1.1
set protocols bgp group CUSTOMER family inet unicast
set protocols bgp group CUSTOMER family inet6 unicast
set protocols bgp group CUSTOMER peer-as 65002
set protocols bgp group CUSTOMER neighbor 2.2.2.2
```

In questo esempio, BGP è configurato per:

* Utilizzare l'indirizzo IP di origine `1.1.1.1` per stabilire la sessione
* Negoziare entrambe le famiglie unicast ipv4 e ipv6
* Eseguire il peer con un router adiacente che appartiene a `AS 65002`
* Eseguire il peer dell'IP del router adiacente `2.2.2.2`

È possibile trovare ulteriori configurazioni [qui](https://www.juniper.net/documentation/en_US/junos11.4/information-products/topic-collections/config-guide-routing/config-guide-routing.pdf).
