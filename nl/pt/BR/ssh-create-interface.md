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

# Crie a nova sub-rede de interface, zona e catálogo de endereços
{: #creating-the-new-interface-zone-and-address-book-subnet}

Primeiro, será necessário criar uma unidade de interface para a VLAN e incluir o endereço do gateway da sub-rede. Em seguida, será possível criar uma zona de segurança associada à nova unidade e uma entrada `address-book` para a sub-rede.  

Role para a direita para visualizar todo o comando.
{: important}

```
set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29
```
