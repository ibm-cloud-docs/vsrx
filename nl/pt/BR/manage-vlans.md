---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: manage, managing, vlan, gateway, route, bypass, disassociate, associate, configuration, disassociating, associating, standalone, ha

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Gerenciando as VLANs da IBM
{: #managing-ibm-vlans}

É possível executar uma variedade de ações da [tela Detalhes do Dispositivo de Gateway](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details).

## Associar uma VLAN a um Dispositivo de Gateway
{: #associate-a-vlan-to-a-gateway-appliance}

Uma VLAN precisa ser associada a um Dispositivo de Gateway antes de poder ser roteada. A associação de VLAN é a vinculação de uma VLAN elegível a um gateway de rede para que ela possa ser roteada para um dispositivo de gateway. Essa associação não roteará automaticamente a VLAN para um dispositivo de gateway. A VLAN continuará a usar os roteadores do cliente de front-end e back-end até que seja roteada.

VLANs podem ser associadas a apenas um Gateway por vez e não devem ter um firewall. Execute o procedimento a seguir para associar uma VLAN a um Gateway de Rede.

1. [Acesse a tela Detalhes do Dispositivo de Gateway](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) no Portal do Cliente.
2. Selecione a guia VLANs.
3. Clique em **Associar VLAN** e selecione uma VLAN na lista suspensa.
4. Clique em **Salvar** e confirme a seleção. A ação de associação de VLAN não roteia a VLAN por meio do firewall.

Depois de associar uma VLAN ao Dispositivo de Gateway, ela aparece na seção VLANs Associadas da tela Detalhes do Dispositivo de Gateway. Nesta seção, a VLAN pode ser roteada para o Gateway ou pode ser desassociada do Gateway. VLANs adicionais elegíveis podem ser associadas a um Dispositivo de Gateway a qualquer momento repetindo as etapas acima.

## Roteie uma VLAN associada
{: #route-an-associated-vlan}

VLANs associadas são vinculadas a um Dispositivo de Gateway, mas o tráfego dentro e fora da VLAN não atinge o Gateway até que a VLAN tenha sido roteada. Depois que uma VLAN associada tiver sido roteada, todo o tráfego de front-end e de back-end será roteado por meio do dispositivo de gateway, em oposição aos roteadores do cliente.

Execute o procedimento a seguir para rotear uma VLAN associada:

1. [Acesse a tela Detalhes do Dispositivo de Gateway](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) no Portal do Cliente.
2. Selecione a guia VLANs.
3. Selecione a(s) VLAN(s) desejada(s) alternando a caixa de seleção.
4. Clique em **Rotear por meio de** e confirme a seleção.

Depois de rotear uma VLAN, todo o tráfego de front-end e backend é movido de roteadores do cliente para o Network Gateway. Os controles adicionais relacionados ao trânsito e ao próprio Dispositivo de Gateway podem ser assumidos acessando a ferramenta de gerenciamento do Gateway. O roteamento por meio do Gateway de Rede pode ser descontinuado em qualquer momento [efetuando bypass no Dispositivo de Gateway](#bypass-gateway-appliance-routing-for-a-vlan).

## Efetue bypass do roteamento do dispositivo de gateway para uma VLAN
{: #bypass-gateway-appliance-routing-for-a-vlan}

Após uma VLAN ser roteada, todo o tráfego de front-end e backend atravessa o Gateway de Rede. A qualquer momento, o Dispositivo de Gateway pode ter bypass efetuado para que o tráfego retorne aos roteadores do cliente de front-end e backend (FCR e BCR).

O bypass de uma VLAN permite que a VLAN permaneça associada ao Gateway de Rede. Se a VLAN não precisar mais ser associada ao Dispositivo de Gateway, consulte [Desassociar uma VLAN de um Dispositivo de Gateway](#disassociate-a-vlan-from-a-gateway-appliance).

Execute o procedimento a seguir para efetuar bypass do roteamento de Gateway para uma VLAN:

1. [Acesse a tela Detalhes do Dispositivo de Gateway](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) no Portal do Cliente.
2. Selecione a guia VLANs.
3. Selecione a(s) VLAN(s) desejada(s) alternando a caixa de seleção.
4. Clique em **Rotear ao redor** e confirme a seleção.

Depois de efetuar bypass no Network Gateway, todo o tráfego de front-end e backend é roteado por meio do FCR e BCR associados à VLAN. A VLAN permanecerá associada ao Dispositivo de Gateway e poderá ser roteada de volta para o Dispositivo de Gateway a qualquer momento.

## Desassociar uma VLAN de um Dispositivo de Gateway
{: #disassociate-a-vlan-from-a-gateway-appliance}

VLANs podem ser vinculadas a um Dispositivo de Gateway em um momento por meio de [associação](#associate-a-vlan-to-a-gateway-appliance). A associação permite que a VLAN seja roteada para o Dispositivo de Gateway a qualquer momento. Se uma VLAN precisar ser associada a outro Dispositivo de Gateway ou se a VLAN não precisar mais ser associada ao seu Gateway, é necessária a desassociação. A desassociação remove o "link" da VLAN com o Dispositivo de Gateway, permitindo que ela seja associada a outro Gateway, se necessário.

Execute o procedimento a seguir para desassociar uma VLAN de um Dispositivo de Gateway:

1. [Acesse a tela Detalhes do Dispositivo de Gateway](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) no Portal do Cliente.
2. Selecione a guia VLANs.
3. Selecione a(s) VLAN(s) desejada(s) alternando a caixa de seleção.
4. Clique em **Desassociar** e confirme a seleção.

Depois de desassociar uma VLAN de um Dispositivo de Gateway, a VLAN pode ser associada a outro Gateway. A VLAN também pode ser associada de volta ao Dispositivo de Gateway a qualquer momento. Após desassociar uma VLAN de um Dispositivo de Gateway, o tráfego da VLAN não pode ser roteado por meio do Gateway. As VLANs devem estar associadas a um Dispositivo de Gateway antes de poderem ser roteadas.

## Roteie múltiplas VLANs por meio da mesma interface de rede
{: #route-multiple-vlans-over-the-same-network-interface}

O {{site.data.keyword.vsrx_full}} pode operar com múltiplas VLANs por meio da mesma interface de rede. Ele também pode manipular o tráfego identificado e o não identificado ao mesmo tempo. Isso é realizado no dispositivo independente configurando a encapsulação da interface como `flexible-vlan-tagging` ou nos dispositivos de alta disponibilidade usando reth2 e reth3 como interfaces identificadas. Isso é feito como parte da configuração padrão e não precisa ser modificado.  Nos dispositivos independentes, a unidade 0 é a subinterface não identificada. As outras unidades diferentes de zero são identificadas.

Use o seguinte conjunto de comandos para configurar as interfaces identificadas adicionais:

Caso independente:
```
set interfaces ge-0/0/0 unit 50 vlan-id 50
set interfaces ge-0/0/0 unit 50 family inet address <IP/MASK>
```

Caso HA:
```
set interfaces reth2 unit 50 vlan-id 50
set interfaces reth2 unit 50 family inet address <IP/MASK>
```

Embora a unidade 0 não esteja identificada, `JunOS` precisa que ela faça referência ao ID de VLAN configurado como `native-vlan`. No exemplo, uma vez que `native-vlan-id` é `10`, a unidade 0 também deve ter um `vlan-id` de `10`. Dessa forma, o `JunOS` é informado de que a unidade 0 deve ser não identificada.
{: note}

## Configuração de VLAN de amostra para o vSRX
{: #sample-vlan-configuration-for-vsrx}

Abaixo está uma configuração de amostra para o vSRX que define duas interfaces privadas e uma zona do cliente.
Com essa configuração de amostra, a VLAN1 e a VLAN2 privadas podem se comunicar uma com a outra. As interfaces do vSRX independente são definidas como ge-0/0/0 (privada) e ge-0/0/1 (pública) e para a instância de alta disponibilidade, elas são definidas como reth2 (HA privada) e reth3 (HA pública).

<img src="images/Sample-Topology-VLAN-to-VLAN.png" alt="drawing" style="width: 500px;"/>

```
# show interfaces

ge-0/0/0 {
   description PRIVATE_VLANs; flexible-vlan-tagging; native-vlan-id 1121; unit 0 {
       vlan-id 1121; family inet {
           address 10.184.108.158/26; }
   } unit 10 {
       vlan-id 1811; family inet {
           address 10.184.237.201/29; }
   } unit 20 {
       vlan-id 1812; family inet {
           address 10.185.48.9/29; }
   }
}


# show security zones security-zone CUSTOMER-PRIVATE
interfaces {
   ge-0/0/0.10 {
       host-inbound-traffic {
           system-services {
               all; }
       }
   }
   ge-0/0/0.20 {
       host-inbound-traffic {
           system-services {
               all; }
       }
   }
}
# show security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PRIVATE
policy Allow_C_C {
   match {
       source-address any; destination-address any; application any; } then {
       permit; }
}
```
