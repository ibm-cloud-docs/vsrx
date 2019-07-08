---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: create, creating, interface, zone, address, subnets, ssh

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# Crear la nueva interfaz, zona y subred de libreta de direcciones
{: #creating-the-new-interface-zone-and-address-book-subnet}

En primer lugar, tendrá que crear una unidad de interfaz para la VLAN y añadir la dirección de la pasarela de la subred. Luego podrá crear una zona de seguridad asociada a la nueva unidad y una entrada `address-book` para la subred.  

Desplácese hacia la derecha para ver el mandato completo.{: important}

```
set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29
```
