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

# Sobre
O IBM® Cloud Juniper vSRX permite rotear seletivamente o tráfego de rede privada e pública por meio de um firewall de nível corporativo completo que é desenvolvido com recursos do software JunOS, como pilhas de roteamento integral, compartilhamento de tráfego e QoS, roteamento baseado em política e VPN. O vSRX fornece desempenho, facilidade de configuração e vantagens de manutenção com a simplicidade de execução em um servidor bare metal. O hardware é dimensionado para manipular o carregamento de roteamento/segurança para múltiplas VLANs e pode ser solicitado com links de rede redundantes e matrizes RAID redundantes. Todos os recursos do vSRX são gerenciados pelo cliente.

O IBM Cloud vSRX é oferecido em dois modos diferentes: cluster independente ou de alta disponibilidade (HA).

**NOTA:** a documentação adicional para o IBM Cloud Juniper vSRX pode ser localizada no tópico [Documentação suplementar](vsrx-docs.html).

##Firewall
O vSRX é implementado para proteger o ambiente de ameaças externas e internas, filtrando o tráfego privado e o público. Os próprios clientes podem gerenciar o vSRX definindo políticas e regras para permitir ou negar (entre outras ações) o tráfego de rede de entrada ou saída, protegendo seus aplicativos de usuários internos e externos. As pilhas IPv4 e IPv6 são suportadas de maneira stateful.

## Gateway de Rede Privada Virtual (VPN)
Conecte o data center ou o escritório no site ao IBM Cloud usando o tunelamento de VPN, provisionando o vSRX como um dispositivo de gateway de rede. É possível usar um túnel VPN IPsec de site para site para comunicação segura do data center ou do escritório de sua empresa com a rede do IBM Cloud. A VPN IPSEC de acesso remoto também é suportada.

Para obter um guia de configuração detalhado sobre a VPN, consulte os links fornecidos no tópico [VPN](vpn.html).

## Conversão de Endereço de Rede (NAT)
Com o dispositivo de gateway vSRX, é possível provisionar servidores de aplicativo e de banco de dados sem interfaces de rede pública e ainda permitir que os servidores acessem a Internet usando a NAT de origem. Também é possível ocultar seus servidores por trás do dispositivo de gateway com NAT de Destino para segurança aprimorada.

## Roteamento de Nível Corporativo
Para aplicativos com multicamadas em diferentes redes isoladas, o vSRX permite a construção de conectividade entre essas redes com maior flexibilidade. É possível configurar o roteamento dinâmico usando o BGP, que permite anunciar o seu próprio espaço IP público para os roteadores do IBM Cloud. O BGP também oferece mais flexibilidade para as configurações de rede privada customizadas ao usar uma combinação de soluções de túneis e link direto.

## Conceitos sobre as VLANs e a função do dispositivo de gateway
Uma VLAN (LAN virtual) é um mecanismo que divide uma rede física em muitos segmentos virtuais. Por conveniência, o tráfego de várias VLANs selecionadas pode ser entregue por meio de um único cabo de rede, um processo comumente chamado de "entroncamento".

O vSRX é gerenciado em duas interfaces diferentes: nos servidores vSRX e no acessório do dispositivo de gateway. O dispositivo de gateway fornece uma interface (GUI e API) para selecionar as VLANs que você deseja associar ao vSRX. Associar uma VLAN a um dispositivo de gateway roteia novamente (ou "entronca") essa VLAN e todas as suas sub-redes para o vSRX, fornecendo controle sobre a filtragem, o encaminhamento e a proteção. Os servidores em uma VLAN associada podem ser acessados somente de outras VLANs passando pelo vSRX. Não é possível contornar o vSRX, a menos que você efetue bypass ou desassocie a VLAN.

Por padrão, um novo dispositivo de gateway é associado a duas VLANs de "trânsito" não removíveis, uma para a rede _pública_ e outra para a _privada_. Essas redes geralmente são usadas para administração e podem ser protegidas pelos comandos do vSRX separadamente.

O vSRX pode gerenciar somente as VLANs que estão associadas a ele por meio do dispositivo de gateway.

Para obter informações sobre como gerenciar as VLANs por meio da tela **Detalhes dos dispositivos de gateway**, consulte o tópico [Gerenciar VLANs](manage-vlans.html).
