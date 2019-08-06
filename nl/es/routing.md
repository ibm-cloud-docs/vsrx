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

# Cómo trabajar con el direccionamiento
{: #working-with-routing}

{{site.data.keyword.vsrx_full}} se basa en `JunOS`, que le ofrece acceso a la pila completa de direccionamiento de Juniper.

##Direccionamiento estático
{: #static-routing}

Para configurar rutas estáticas, ejecute los mandatos siguientes:

###Configuración de una ruta predeterminada
{: #setting-a-default-route}

```
set routing-options static route 0/0 next-hop <Gateway IP>
```

### Creación de una ruta estática
{: #creating-a-static-route}
```
set routing-options static route <PREFIX/MASK> next-hop <Gateway IP>
```  

###Direccionamiento OSPF básico
{: #basic-ospf-routing}

Para configurar el direccionamiento OSPF básico, utilizando sólo el área 0, ejecute los siguientes mandatos utilizando la autenticación md5:

```
set protocols ospf area 0 interface ge-0/0/1.0 authentication md5 0 key <KEY>
```

### Direccionamiento BGP básico
{: #basic-bgp-routing}

Para configurar el direccionamiento BGP básico, defina primero el AS local:

```
set routing-options autonomous-system 65001
```

A continuación, configure el BGP vecino y sus atributos de sesión:

```
set protocols bgp group CUSTOMER local-address 1.1.1.1
set protocols bgp group CUSTOMER family inet unicast
set protocols bgp group CUSTOMER family inet6 unicast
set protocols bgp group CUSTOMER peer-as 65002
set protocols bgp group CUSTOMER neighbor 2.2.2.2
```

En este ejemplo, se configura BGP para lo siguiente:

* Utilizar la dirección IP de origen `1.1.1.1` para establecer la sesión
* Negociar familias de difusión única ipv4 e ipv6
* Establecer una relación de igual a igual con un vecino perteneciente a `AS 65002`
* Establecer una relación de igual a igual con el IP vecino `2.2.2.2`

Puede encontrar configuraciones adicionales en el [sitio web de Juniper ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.juniper.net/documentation/en_US/junos11.4/information-products/topic-collections/config-guide-routing/config-guide-routing.pdf){: new_window}.
