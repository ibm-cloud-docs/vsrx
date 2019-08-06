---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: about, vsrx, overview, details, firewall, vpn, nat, routing, vlan

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

# Sobre o {{site.data.keyword.vsrx_full}}
{: #about-ibm-cloud-juniper-vsrx}

O {{site.data.keyword.vsrx_full}} permite rotear o tráfego de rede privada e pública seletivamente, por meio de um firewall completo de nível corporativo que é desenvolvido com os recursos do software JunOS, como as pilhas de roteamento completo, o compartilhamento de tráfego e QoS, o roteamento baseado em políticas e a VPN. O vSRX oferece desempenho, facilidade de configuração e vantagens de manutenção, com a simplicidade da execução em um servidor bare metal. O hardware é dimensionado para lidar com a carga de roteamento e segurança associada a diversas VLANs e pode ser solicitado com links de rede redundantes e matrizes RAID redundantes. Todos os recursos do vSRX são gerenciados pelo cliente.

O {{site.data.keyword.vsrx_full}} é oferecido em dois modos diferentes: modo independente ou cluster de Alta Disponibilidade (HA).

A documentação adicional do {{site.data.keyword.vsrx_full}} pode ser localizada no tópico [Documentação suplementar](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation).
{: note}

## Firewall
{: #firewall}

O vSRX é implementado para proteger seu ambiente contra ameaças externas e internas, filtrando o tráfego privado e voltado ao público. Os clientes podem gerenciar o vSRX por conta própria, definindo políticas e regras que permitem ou negam (entre outras ações) o tráfego de rede de entrada ou de saída, protegendo seus aplicativos contra abordagens internas e externas. As pilhas IPv4 e IPv6 são suportadas de maneira stateful.

## Gateway de rede privada virtual (VPN)
{: #virtual-private-network-vpn-gateway}

Conecte o data center ou o escritório no site ao IBM Cloud usando o tunelamento de VPN, provisionando o vSRX como um dispositivo de gateway de rede. É possível usar um túnel VPN IPsec de site para site para comunicação segura do data center ou do escritório de sua empresa com a rede do IBM Cloud. A VPN IPsec de acesso remoto também é suportada.

Para obter um guia de configuração detalhado sobre a VPN, consulte os links fornecidos no tópico [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn).

## NAT (Network Address Translation)
{: #network-address-translation-nat-}

Com o dispositivo de gateway vSRX, é possível provisionar servidores de aplicativos e bancos de dados sem interfaces de rede pública e ainda permitir que seus servidores acessem a Internet usando o _NAT de origem_. Para obter maior segurança, é possível proteger seus servidores atrás do dispositivo de gateway por meio do _NAT de destino_.

## Roteamento de nível corporativo
{: #enterprise-grade-routing}

O vSRX oferece maior flexibilidade para criar a conectividade entre aplicativos multicamadas executados em diferentes redes isoladas. É possível configurar o roteamento dinâmico usando o BGP, que permite anunciar o seu próprio espaço IP público para os roteadores do IBM Cloud. O BGP também oferece mais flexibilidade para configurações customizadas de rede privada quando você está usando uma combinação de túneis e [soluções de Direct Link](/docs/infrastructure/direct-link?topic=direct-link-overview-of-direct-link-offerings#overview-of-direct-link-offerings).

## Conceitos sobre as VLANs e a função do dispositivo de gateway
{: #concepts-about-vlans-and-the-gateway-appliance-s-role}

Uma VLAN (rede local virtual) é um mecanismo que segrega uma rede física em diversos segmentos virtuais. Por conveniência, o tráfego de diversas VLANs selecionadas pode ser fornecido por meio de um único cabo de rede, usando um processo comumente chamado de "entroncamento".

O vSRX é gerenciado em duas interfaces diferentes: nos servidores vSRX e no acessório do dispositivo de gateway. O dispositivo de gateway fornece uma interface (GUI e API) para selecionar as VLANs que você deseja associar ao vSRX. Associar uma VLAN a um dispositivo de gateway roteia novamente (ou "entronca") essa VLAN e todas as suas sub-redes para o vSRX, fornecendo controle sobre a filtragem, o encaminhamento e a proteção. Servidores em uma VLAN associada podem ser acessados ​​por meio de outras VLANs somente através de seu vSRX, portanto, não é possível contornar o vSRX, a menos que você ignore ou desassocie a VLAN.

Por padrão, um novo dispositivo de gateway é associado a duas VLANs de "trânsito" não removíveis, uma para a rede _pública_ e outra para a _privada_. Essas redes geralmente são usadas para administração e podem ser protegidas pelos comandos do vSRX separadamente.

O vSRX pode gerenciar as VLANs associadas a ele por meio do Dispositivo de gateway (somente).

Para obter informações sobre como gerenciar as VLANs por meio da tela **Detalhes dos dispositivos de gateway**, consulte o tópico [Gerenciar VLANs](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans).
