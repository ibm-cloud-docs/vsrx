---

copyright:
  years: 2018
lastupdated: "2018-11-06"

keywords: limitations, problems

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

# Limitaciones conocidas de {{site.data.keyword.vsrx_full}}
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

Limitaciones actuales de {{site.data.keyword.cloud}} {{site.data.keyword.vsrx_full}}:

* Juniper vSRX Gateway se despliega con virtualización de red utilizando Linux Bridge. La virtualización de red mediante Linux Bridge solo puede conseguir un rendimiento limitado y nunca el rendimiento de la tasa de la línea.

* No hay soporte para actualizar de la modalidad autónoma a la de alta disponibilidad.

* {{site.data.keyword.vsrx_full}} Gateway se despliega con las opciones de Junos OS versión `15.1` o `18.4`. Actualmente, no hay soporte para actualizar/degradar a otra versión.

* La licencia de evaluación de 60 días puede hacer que el kernel genere mensajes de ERROR, aunque haya otra licencia (válida) en el sistema. Debe eliminar todas las licencias de evaluación de 60 días para evitar este problema. Para ello, siga el procedimiento siguiente:

1. Inicie una sesión en el dispositivo de pasarela vSRX.

2. Entre en modalidad de CLI ejecutando el mandato `cli` en el indicador de la consola.

3. Ejecute el mandato para obtener el identificador de licencia:

```
show system license
```
La salida debería parecerse
a la siguiente:

```
License usage:
                                 Licenses     Licenses    Licenses    Expiry
  Feature name                       used    installed      needed
  logical-system                        0            3           0    permanent
  Virtual Appliance                     1            1           0    2021-10-18 00:00:00 UTC
  remote-access-ipsec-vpn-client        0            2           0    permanent

Licenses installed:
  License identifier: E2018101804
  License version: 4
  Software Serial Number: SUB00024128768
  Customer ID: IBM_SL_10G
  Features:
    Virtual Appliance - Virtual Appliance
      date-based, 2018-10-18 00:00:00 UTC - 2021-10-18 00:00:00 UTC
```

4. Copie el identificador de la licencia que desea suprimir y ejecute el mandato:

```
request system license delete <license identifier>
```
