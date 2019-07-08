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

# Gestionar VLAN de IBM
{: #managing-ibm-vlans}

Puede realizar una serie de acciones de la [pantalla Detalles de dispositivo de pasarela](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details).

## Asociar una VLAN a un dispositivo de pasarela
{: #associate-a-vlan-to-a-gateway-appliance}

Una VLAN necesita asociarse a un dispositivo de pasarela antes de poder ser direccionada. Una asociación VLAN es la vinculación de una VLAN elegible a la pasarela de red, de forma que se pueda direccionar a un dispositivo de pasarela. Esta asociación no direcciona de manera automática la VLAN al dispositivo de pasarela; la VLAN sigue utilizando los direccionadores frontales y fondo del cliente hasta que se direcciona.

Pueden asociarse las VLAN a una sola pasarela a la vez y no deben tener un cortafuegos. Realice el procedimiento siguiente para asociar una VLAN a una pasarela de red.

1. [Acceda a la pantalla Detalles de dispositivo de pasarela](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) en el Portal de clientes.
2. Seleccione el separador VLAN.
3. Pulse **Asociar VLAN** y seleccione una VLAN del menú desplegable.
4. Pulse **Guardar** y confirme su selección. La acción de asociar VLAN no direcciona la VLAN a través del cortafuegos.

Después de asociar una VLAN a un dispositivo de pasarela, aparece en la sección VLAN asociadas de la pantalla Detalles de dispositivo de pasarela. En esta sección, la VLAN puede direccionar a la pasarela o puede asociarse de la pasarela. Pueden asociarse VLAN elegibles adicionales al dispositivo de pasarela en cualquier momento repitiendo los pasos anteriores.

## Direccionar una VLAN asociada
{: #route-an-associated-vlan}

Las VLAN asociadas están vinculadas al dispositivo de pasarela, pero el tráfico de entrada y salida de la VLAN no alcanza la pasarela hasta que se ha direccionada la VLAN. Después de direccionar una VLAN asociada, todo el tráfico frontal y de fondo se direcciona a través del dispositivo de pasarela, en contraposición con los direccionadores de cliente.

Realice el procedimiento siguiente para direccionar una VLAN asociada:

1. [Acceda a la pantalla Detalles de dispositivo de pasarela](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) en el Portal de clientes.
2. Seleccione el separador VLAN.
3. Seleccione las VLAN que desee marcando el recuadro de selección.
4. Pulse **Direccionar a través** y confirme su selección.

Después de direccionar una VLAN, todo el tráfico frontal y de fondo se desplaza de los direccionadores de cliente a la pasarela de red. Los controles adicionales relacionados con el tráfico y el propio dispositivo de pasarela pueden utilizarse al acceder a la herramienta de gestión de la pasarela. Es posible que se retire el direccionamiento a través de la pasarela de red en cualquier momento [ignorando el dispositivo de pasarela](#bypass-gateway-appliance-routing-for-a-vlan).

## Ignorar el direccionamiento de dispositivo de pasarela para una VLAN
{: #bypass-gateway-appliance-routing-for-a-vlan}

Después de que se haya direccionado una VLAN, todo el tráfico frontal y de fondo viaja a través de la pasarela de red. En cualquier momento, se puede ignorar el dispositivo de pasarela para que el tráfico vuelva a los direccionadores de cliente frontales y de fondo (FCR y BCR).

Ignorar una VLAN permite que esta permanezca asociada a la pasarela de red. Si la VLAN no debe continuar asociándose con la pasarela de dispositivo, consulte [Desasociar una VLAN de un dispositivo de pasarela](#disassociate-a-vlan-from-a-gateway-appliance).

Realice el procedimiento siguiente para ignorar el direccionamiento de pasarela para una VLAN:

1. [Acceda a la pantalla Detalles de dispositivo de pasarela](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) en el Portal de clientes.
2. Seleccione el separador VLAN.
3. Seleccione las VLAN que desee marcando el recuadro de selección.
4. Pulse **Direccionar alrededor** y confirme su selección.

Después de ignorar la pasarela de red, todo el tráfico frontal y de fondo se direcciona mediante el FCR y el BCR asociados con la VLAN. La VLAN permanecerá asociada al dispositivo de pasarela y podrá direccionarse al mismo en cualquier momento.

## Desasociar una VLAN de un dispositivo de pasarela
{: #disassociate-a-vlan-from-a-gateway-appliance}

Las VLAN pueden vincularse a un dispositivo de pasarela a la vez mediante [asociación](#associate-a-vlan-to-a-gateway-appliance). La asociación permite que la VLAN se direccione al dispositivo de pasarela en cualquier momento. Es necesaria la disociación si una VLAN debe asociarse a otro dispositivo de pasarela, o si la VLAN ya no debe estar asociada al mismo. La disociación elimina el "enlace" de la VLAN al dispositivo de pasarela, permitiéndole asociarse a otra pasarela, si es necesario.

Realice el procedimiento siguiente para desasociar una VLAN del dispositivo de pasarela:

1. [Acceda a la pantalla Detalles de dispositivo de pasarela](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) en el Portal de clientes.
2. Seleccione el separador VLAN.
3. Seleccione las VLAN que desee marcando el recuadro de selección.
4. Pulse **Desasociar** y confirme su selección.

Después de desasociar una VLAN del dispositivo de pasarela, la VLAN puede asociarse a otra pasarela. También puede volver a asociarse al dispositivo de pasarela en cualquier momento. Después de desasociar una VLAN de un dispositivo de pasarela, el tráfico no puede direccionarse mediante la pasarela. Las VLAN deben asociarse a un dispositivo de pasarela antes de poder ser direccionadas.

## Direccionar varias VLAN en la misma interfaz de red
{: #route-multiple-vlans-over-the-same-network-interface}

IBM® Cloud Juniper vSRX puede trabajar con varias VLAN sobre la misma interfaz de red. También puede manejar el tráfico etiquetado y sin etiquetar a la vez. Esto se consigue en el dispositivo autónomo estableciendo la encapsulación de la interfaz en `flexible-vlan-tagging` o, en los dispositivos de alta disponibilidad, utilizando reth2 y reth3 como interfaces etiquetadas. Esto se realiza como parte de la configuración predeterminada y no es necesario modificarlo.  En los dispositivos autónomos, la unidad 0 es la subinterfaz que no está etiquetada; las otras unidades están etiquetadas.

Utilice el siguiente conjunto de mandatos para configurar interfaces etiquetadas adicionales:

Escenario autónomo:
```
set interfaces ge-0/0/0 unit 50 vlan-id 50
set interfaces ge-0/0/0 unit 50 family inet address <IP/MASK>
```

Escenario de alta disponibilidad:
```
set interfaces reth2 unit 50 vlan-id 50
set interfaces reth2 unit 50 family inet address <IP/MASK>
```

Aunque la unidad 0 no está etiquetada, `JunOS` la necesita para hacer referencia al ID de VLAN que está configurado como `native-vlan`. En el ejemplo, puesto que `native-vlan-id` es `10`, la unidad 0 debería tener también un `vlan-id` de `10`. De este modo, se informa a `JunOS` que la unidad 0 debe ser una unidad sin etiquetar.
{: note}

## Configuración de VLAN de ejemplo para vSRX
{: #sample-vlan-configuration-for-vsrx}

A continuación se muestra una configuración de ejemplo para vSRX que define dos interfaces privadas y una zona de cliente.
Con esta configuración de ejemplo, la VLAN1 privada y la VLAN2 privada se pueden comunicar entre sí. Las interfaces vSRX autónomas se definen como ge-0/0/0 (privada) y ge-0/0/1 (pública), y, para la instancia de alta disponibilidad, se definen como reth2 (HA privada) y reth3 (HA pública).

<img src="images/Sample-Topology-VLAN-to-VLAN.png" alt="dibujo" style="width: 500px;"/>

```
# show interfaces

ge-0/0/0 {
   description PRIVATE_VLANs;
   flexible-vlan-tagging;
   native-vlan-id 1121;
   unit 0 {
       vlan-id 1121;
       family inet {
           address 10.184.108.158/26;
       }
   }
   unit 10 {
       vlan-id 1811;
       family inet {
           address 10.184.237.201/29;
       }
   }
   unit 20 {
       vlan-id 1812;
       family inet {
           address 10.185.48.9/29;
       }
   }
}


# show security zones security-zone CUSTOMER-PRIVATE
interfaces {
   ge-0/0/0.10 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
   ge-0/0/0.20 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
}
# show security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PRIVATE
policy Allow_C_C {
   match {
       source-address any;
       destination-address any;
       application any;
   }
   then {
       permit;
   }
}
```
