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

# Acerca de {{site.data.keyword.vsrx_full}}
{: #about-ibm-cloud-juniper-vsrx}

{{site.data.keyword.vsrx_full}} le permite direccionar de forma selectiva el tráfico de la red privada y pública a través de un cortafuegos de empresa con todas las características respaldado por las características de software de JunOS, como por ejemplo pilas de direccionamiento completas, QoS y compartición de tráfico, direccionamiento basado en políticas y VPN. El vSRX proporciona rendimiento, facilidad de configuración y ventajas de mantenimiento con la comodidad de que se ejecuta en un servidor nativo. El hardware está dimensionado para manejar el direccionamiento y la carga de seguridad asociados a varias VLAN y se puede pedir con enlaces de red redundantes y matrices RAID redundantes. Todas las características de vSRX están gestionadas por el cliente.

{{site.data.keyword.vsrx_full}} se ofrece en dos modalidades diferentes: modalidad autónoma o clúster de alta disponibilidad (HA).

Encontrará documentación adicional sobre {{site.data.keyword.vsrx_full}} en el tema [Documentación suplementaria](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation).{: note}

## Cortafuegos
{: #firewall}

El vSRX se despliega para proteger su entorno frente a amenazas externas e internas filtrando el tráfico tanto privado como de cara al público. Los clientes pueden gestionar ellos mismos el vSRX definiendo políticas y reglas que permitan o denieguen (entre otras acciones) el tráfico de red de entrada o de salida, protegiendo así sus aplicaciones de métodos internos y externos. Tanto las pilas IPv4 como las de IPv6 reciben soporte con estado.

## Pasarela de red privada virtual (VPN)
{: #virtual-private-network-vpn-gateway}

Conecte su oficina o centro de datos local a IBM Cloud mediante la ejecución en túnel VPN, proporcionando vSRX como dispositivo de pasarela de red. Puede utilizar un túnel VPN de sitio a sitio de IPsec para una comunicación segura de la oficina o el centro de datos de su empresa con la red de IBM Cloud. También se da soporte a una VPN de IPsec de acceso remoto.

Para ver una guía de configuración detallada de VPN, consulte los enlaces que se suministran en el tema [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn).

## Conversión de direcciones de red (NAT)
{: #network-address-translation-nat-}

Con el dispositivo de pasarela vSRX, puede suministrar aplicaciones y servidores de base de datos sin interfaces de red pública y seguir permitiendo que los servidores accedan a Internet utilizando _NAT de origen_. Para una mayor seguridad, puede proteger sus servidores detrás del dispositivo de pasarela utilizando _NAT de destino_.

## Direccionamiento de nivel empresarial
{: #enterprise-grade-routing}

El vSRX le permite una mayor flexibilidad para crear una conectividad entre aplicaciones multinivel que se ejecuten en distintas redes aisladas. Puede configurar el direccionamiento dinámico utilizando BGP, lo que le permitirá anunciar su propio espacio de IP pública en los direccionadores de IBM Cloud. BGP también ofrece más flexibilidad para las configuraciones de red privada personalizadas cuando se utilizan una combinación de túneles y [soluciones Direct Link](/docs/infrastructure/direct-link?topic=direct-link-overview-of-direct-link-offerings#overview-of-direct-link-offerings).

## Conceptos sobre las VLAN y el rol del dispositivo de pasarela
{: #concepts-about-vlans-and-the-gateway-appliance-s-role}

Una VLAN (red de área local virtual) es un mecanismo que segrega una red física en muchos segmentos virtuales. Para más comodidad, el tráfico de varias VLAN seleccionadas puede suministrarse mediante un solo cable de red, utilizando un proceso comúnmente denominado "conexión troncal".

vSRX se gestiona en dos interfaces distintas: los servidores de vSRX y el elemento fijo de dispositivo de pasarela. El dispositivo de pasarela proporciona una interfaz (GUI y API) para seleccionar las VLAN que desea asociar con su vSRX. La asociación de una VLAN con un dispositivo de pasarela redirige (o "realiza una conexión troncal") dicha VLAN y todas sus subredes a vSRX, proporcionándole control sobre el filtrado, reenvío y protección. Solo se pueden alcanzar los servidores de una VLAN asociada desde otras VLAN pasando por vSRX; no es posible omitir vSRX a menos que se ignore o se desasocie la VLAN.

De forma predeterminada, un nuevo dispositivo de pasarela se asocia a dos VLAN de "tránsito" no extraíbles, una para la _pública_ y otra para la _privada_. Estas redes se suelen utilizar para la administración y se pueden proteger mediante mandatos vSRX por separado.

vSRX puede gestionar VLAN asociadas al mismo mediante el dispositivo de pasarela (únicamente).

Para obtener información sobre cómo gestionar las VLAN desde la pantalla **Detalles de dispositivos de pasarela**, consulte el tema sobre [Gestión de VLAN](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans).
