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

# Acerca de IBM Cloud Juniper vSRX
{: #about-ibm-cloud-juniper-vsrx}

IBM® Cloud Juniper vSRX le permite direccionar de forma selectiva el tráfico de la red privada y pública a través de un cortafuegos de empresa con todas las funciones respaldado por las características de software de JunOS, como por ejemplo pilas de direccionamiento completas, QoS y compartición de tráfico, direccionamiento basado en políticas y VPN. El vSRX proporciona rendimiento, facilidad de configuración y ventajas de mantenimiento con la comodidad de que se ejecuta en un servidor nativo. El hardware tiene el tamaño para manejar la carga de direccionamiento y de seguridad para varias VLAN y puede ordenarse con enlaces de red redundantes y matrices RAID redundantes. Todas las características de vSRX están gestionadas por el cliente.

IBM Cloud vSRX se ofrece en dos modalidades diferentes: clúster autónomo o alta disponibilidad (HA).

**NOTA:** encontrará documentación adicional sobre IBM Cloud Juniper vSRX en el tema [Documentación suplementaria](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation).

## Cortafuegos
El vSRX se despliega para proteger su entorno frente a amenazas externas e internas, filtrando tanto el tráfico privado como el público. Los clientes pueden gestionar ellos mismos el vSRX definiendo políticas y reglas para permitir o denegar (entre otras acciones) el tráfico de red de entrada o de salida, protegiendo sus aplicaciones de usuarios internos y externos. Tanto las pilas IPv4 como las de IPv6 reciben soporte con estado.

## Pasarela de red privada virtual (VPN)
Conecte su oficina o centro de datos local a IBM Cloud mediante la ejecución en túnel VPN, proporcionando vSRX como dispositivo de pasarela de red. Puede utilizar un túnel VPN de sitio a sitio de IPsec para una comunicación segura de la oficina o el centro de datos de su empresa con la red de IBM Cloud. También se da soporte al VPN IPSEC de acceso remoto.

Para ver una guía de configuración detallada de VPN, consulte los enlaces que se suministran en el tema [VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn).

## Conversión de dirección de red (NAT)
Con el dispositivo de pasarela vSRX, puede proporcionar aplicaciones y servidores de base de datos sin interfaces de red pública mientras permite que los servidores puedan acceder a Internet mediante Source NAT. También puede ocultar los servidores detrás del dispositivo de pasarela con Destination NAT para mejorar la seguridad.

## Direccionamiento de empresa
Para las aplicaciones multinivel en diferentes redes aisladas, vSRX le permite crear conectividad entre estas redes con mayor flexibilidad. Puede configurar el direccionamiento dinámico utilizando BGP, lo que le permitirá anunciar su propio espacio de IP pública en los direccionadores de IBM Cloud. BGP también ofrece más flexibilidad para las configuraciones de red privada personalizadas cuando se utilizan una combinación de túneles y soluciones de enlace directo.

## Conceptos sobre las VLAN y el rol del dispositivo de pasarela
Una VLAN (LAN virtual) es un mecanismo que segrega una red física en muchos segmentos virtuales. Por su comodidad, el tráfico de varias VLAN seleccionadas puede suministrarse mediante un solo cable de red, proceso comúnmente denominado "conexión troncal".

vSRX se gestiona en dos interfaces distintas: los servidores de vSRX y el elemento fijo de dispositivo de pasarela. El dispositivo de pasarela proporciona una interfaz (GUI y API) para seleccionar las VLAN que desea asociar con su vSRX. La asociación de una VLAN con un dispositivo de pasarela redirige (o "realiza una conexión troncal") dicha VLAN y todas sus subredes a vSRX, proporcionándole control sobre el filtrado, reenvío y protección. Los servidores de una VLAN asociada solo puede alcanzarse a partir de otras VLAN pasando por vSRX; no es posible omitir vSRX a menos que ignore o desasocie la VLAN.

De forma predeterminada, un nuevo dispositivo de pasarela se asocia a dos VLAN de "tránsito" no extraíbles, una para la _pública_ y otra para la _privada_. Estas redes se suelen utilizar para la administración y se pueden proteger mediante mandatos vSRX por separado.

vSRX solo puede gestionar VLAN asociadas con el mismo mediante el dispositivo de pasarela.

Para obtener información sobre cómo gestionar las VLAN desde la pantalla **Detalles de dispositivos de pasarela**, consulte el tema sobre [Gestión de VLAN](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans).
