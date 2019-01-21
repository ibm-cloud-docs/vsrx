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

# Cómo permitir SSH y ejecutar ping en una subred pública
En esta guía aprenderá a configurar IBM® Cloud Juniper vSRX Estándar con una nueva interfaz, zona y libreta de direcciones. Como la acción predeterminada para todo el tráfico es descartar (drop), esta guía le mostrará cómo configurar flujos de tráfico que permitan todo el tráfico dentro de la nueva zona, todo el tráfico desde la nueva zona a internet y solo ssh y ping desde internet a una subred de la nueva VLAN.

En este ejemplo se utilizan los siguientes valores:
```
Vlan pública: 1523
Subred pública: 169.47.211.152/29
```

**NOTA:** en esta guía paso a paso se presupone que se utiliza un despliegue de alta disponibilidad de vSRX, con una única VLAN pública y subred.

## Qué conseguirá

En esta guía de paso a paso aprenderá a configurar el servicio:

Tarea  | Descripción
------------- | -------------
[Crear una nueva interfaz, zona y subred de libreta de direcciones](ssh-create-interface.html) | Cree la unidad de interfaz etiquetada y la zona de seguridad para la nueva VLAN.
[Crear sus nuevos flujos de tráfico](ssh-create-flows.html) | Cree los nuevos flujos de tráfico para permitir ping y SSH de entrada.
[Confirmar la salida y confirmar los cambios](ssh-check-output.html) | Compruebe la salida para confirmar lo que se confirmará en la configuración activa.
