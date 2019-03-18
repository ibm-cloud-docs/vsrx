---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Creazione della nuova interfaccia, della zona e della sottorete della rubrica
{: #creating-the-new-interface-zone-and-address-book-subnet}

Per prima cosa, dovrai creare un'unità di interfaccia per la VLAN e aggiungere l'indirizzo gateway della sottorete. Sarai quindi in grado di creare una zona di sicurezza associata alla nuova unità e una voce `address-book` per la sottorete.  

**NOTA:** scorri a destra per visualizzare il comando completo!

```
set interfaces reth3 unit 1523 vlan-id 1523
set interfaces reth3 unit 1523 family inet address 169.47.211.153/29
set security zones security-zone CUSTOMER-PUBLIC interfaces reth3.1523 host-inbound-traffic system-services all
set security address-book global address VSI_PUB_NET 169.47.211.152/29
```
