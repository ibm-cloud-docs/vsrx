---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords:

subcollection: vsrx, ssh, allowing, pinging, subnet, public

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

# Permitindo o SSH e o ping para uma sub-rede pública
{: #allowing-ssh-and-pinging-to-a-public-subnet}

Neste guia, você aprenderá a configurar o {{site.data.keyword.vsrx_full}} Standard com uma nova interface, zona e catálogo de endereços. Como a ação padrão para todo o tráfego é descartar, este guia mostrará como configurar os fluxos de tráfego que permitem todo o tráfego dentro da nova zona, todo o tráfego da nova zona para a Internet e como permitir apenas SSH e ping da Internet para uma sub-rede na nova VLAN.

Neste exemplo, os seguintes valores são usados.

```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

Este passo a passo considera uma implementação de alta disponibilidade do vSRX com uma única VLAN pública e sub-rede.
{: note}

## O que você aprenderá
{: #what-you-ll-accomplish}

Neste guia passo a passo, você aprenderá a configurar o serviço:

Atividade  | Descrição
------------- | -------------
[Crie uma nova sub-rede de interface, zona e catálogo de endereços](/docs/infrastructure/vsrx?topic=vsrx-creating-the-new-interface-zone-and-address-book-subnet) | Crie a unidade de interface identificada e a zona de segurança para a nova VLAN.
[Criando seus novos fluxos de tráfego](/docs/infrastructure/vsrx?topic=vsrx-creating-your-new-traffic-flows) | Crie os novos fluxos de tráfego para permitir ping e SSH de entrada.
[Certifique a saída e confirme as mudanças](/docs/infrastructure/vsrx?topic=vsrx-confirming-the-output-and-commiting-the-changes) | Verifique a saída para certificar o que será confirmado para a configuração ativa.
