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

# Como permitir SSH e ping para uma sub-rede pública
Neste guia, você aprenderá a configurar o IBM® Cloud Juniper vSRX Standard com uma nova interface, zona e catálogo de endereços. Como a ação padrão para todo o tráfego é descartar, este guia mostrará como configurar os fluxos de tráfego que permitem todo o tráfego dentro da nova zona, todo o tráfego da nova zona para a Internet e como permitir apenas SSH e ping da Internet para uma sub-rede na nova VLAN.

Neste exemplo, os seguintes valores são usados.
```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

**NOTA:** esse passo a passo supõe uma implementação de alta disponibilidade do vSRX, com uma única VLAN pública e sub-rede.

## O que você aprenderá

Neste guia passo a passo, você aprenderá a configurar o serviço:

Atividade  | Descrição
------------- | -------------
[Crie uma nova sub-rede de interface, zona e catálogo de endereços](ssh-create-interface.html) | Crie a unidade de interface identificada e a zona de segurança para a nova VLAN.
[Criando os novos fluxos de tráfego](ssh-create-flows.html) | Crie os novos fluxos de tráfego para permitir ping e SSH de entrada.
[Certifique a saída e confirme as mudanças](ssh-check-output.html) | Verifique a saída para certificar o que será confirmado para a configuração ativa.
