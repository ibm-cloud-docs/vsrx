---

copyright:
  years: 2018
lastupdated: "2019-05-03"

keywords: vsrx, ordering, gateway, appliance

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

# Iniciación a {{site.data.keyword.vsrx_full}} Gateway
{: #getting-started}

Para empezar a trabajar con {{site.data.keyword.vsrx_full}} Gateway, determine en primer lugar si su cuenta está enlazada a IBM Cloud.

Para averiguar si tiene una cuenta enlazada, vaya al [Portal de clientes ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window} en el navegador e inicie una sesión. Si su cuenta está enlazada, no verá el botón **Más información sobre Bluemix** en la parte superior derecha.

## Pasos para realizar la solicitud
{: #steps-for-ordering}

Puede solicitar su dispositivo de pasarela siguiendo uno de estos métodos:

Para ver una lista de limitaciones conocidas de {{site.data.keyword.vsrx_full}} Gateway, consulte el [tema sobre limitaciones conocidas](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx).
{: note}

### Cómo realizar la solicitud con una cuenta enlazada
{: #ordering-with-a-linked-account}

Si la cuenta está enlazada, siga este procedimiento:

1. En el navegador, abra la página Dispositivos de pasarela del [catálogo de Cloud ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/gen1/infrastructure/provision/gateway){: new_window} e inicie sesión en su cuenta.

  También puede acceder a esta página iniciando sesión en la [Consola de interfaz de usuario de IBM Cloud ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com) y seleccionando **Infraestructura clásica > Red > Dispositivo de pasarela**.
También, en el [Catálogo de IBM Cloud ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/catalog), seleccione la categoría **Red** y elija el mosaico **Dispositivo de pasarela**.

2. Elija **Juniper vSRX (hasta 1 Gbps)** o **Juniper vSRX (hasta 10 Gbps)** en **Proveedor de pasarela**.

3. En la sección **Dispositivo de pasarela**, especifique la información de **Nombre de host** y nombre de **dominio**. Estos campos ya estarán cumplimentados con información predeterminada, asegúrese de que los valores son correctos.

	<img src="images/linked_order.png" alt="dibujo" style="width: 700px;"/>

4. Si lo desea, marque la opción **Alta disponibilidad** y seleccione la **Ubicación** deseada del centro de datos y el **Pod** específico que prefiera en el menú desplegable.

  Sólo se mostrarán los pods que ya tengan una VLAN asociada. Si desea suministrar su Dispositivo de pasarela en un pod que no aparece en la lista, primero cree una VLAN en el mismo.
  {: note}

	<img src="images/linked_server.png" alt="dibujo" style="width: 600px;"/>

4. En la sección **Configuración**, seleccione el procesador seleccionando la RAM y las claves SSH (si desea utilizarlas para autenticar el acceso a la nueva Pasarela).

  Se elige el procesador adecuado en base a la versión de licencia que ha seleccionado en el paso dos. Sin embargo, puede elegir configuraciones de RAM distintas.
  {: note}

5. En la sección **Discos de almacenamiento**, elija las opciones que se ajusten a sus requisitos de almacenamiento.

  Hay las opciones RAID0 y RAID1 disponibles para una mayor protección contra la pérdida de datos, así como los repuestos dinámicos (componentes de copia de seguridad que se pueden poner en servicio inmediatamente cuando falla un componente primario).
  {: note}

  Puede tener hasta cuatro discos por vSRX. El "Tamaño de disco" en una configuración de RAID es el tamaño de disco utilizable, ya que las configuraciones de RAID están duplicadas.
  {: note}

  Reserve más de los valores predeterminados de disco si desea ejecutar diagnósticos de red que generen registros detallados. {: tip}

6. En la sección **Interfaz de red**, seleccione las **Velocidades de puerto de enlace ascendente**. La selección predeterminada es una única interfaz, pero también hay las opciones redundante y privada. Elija la que mejor se ajuste a sus necesidades.

  La sección **Complementos** de interfaz de red le permite seleccionar una dirección IPv6 si es necesario, y muestra las opciones predeterminadas adicionales que haya.

8. Revise las selecciones que ha realizado, compruebe que ha leído los Acuerdos de servicio de terceros y pulse **Crear**. El pedido se verifica automáticamente.

Una vez que se aprueba el pedido, se inicia automáticamente el suministro de su pasarela {{site.data.keyword.vsrx_full}}. Cuando se haya completado el proceso de suministro, el nuevo vSRX aparecerá en la página de lista Dispositivos de pasarela. Pulse el nombre de la pasarela para abrir la página Detalles de pasarela. Encontrará las direcciones IP, el nombre de usuario de inicio de sesión y la contraseña del dispositivo.  

Recuerde que una vez que hace el pedido y configura la pasarela desde el catálogo de IBM Cloud, también debe configurar el propio dispositivo con los mismos Valores.
{: tip}

### Cómo realizar la solicitud con una cuenta no enlazada
{: #ordering-with-a-unlinked-account}

Si la cuenta no está enlazada, siga este procedimiento:

1.	Abra el [Portal de clientes ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window} e inicie sesión en su cuenta.
2.	En la navegación del Portal de clientes, seleccione **Red > Dispositivos de pasarela**.
3.	En la lista **Dispositivos de pasarela**, pulse **Solicitar pasarela**.
4.	En la página **Pedido**, seleccione el centro de datos que desee en el menú desplegable y elija el tipo de hardware de servidor deseado en el que se suministrará Juniper vSRX.

	Si tiene intención de utilizar un servidor de varios núcleos y dos procesadores, debe seleccionar **Intel Xeon 5120** como tipo de servidor.
  {: note}

5.	En la página **Pedido**, seleccione la opción **Par de alta disponibilidad** si lo desea y luego seleccione el tamaño de **Memoria**.
6. 	Luego pulse el separador **Juniper** bajo **Sistema operativo**, seleccione **Juniper vSRX (hasta 1 Gbps) Estándar** para un servidor de un solo procesador o **Juniper vSRX (hasta 10 Gbps) Estándar** para un servidor de dos procesadores.
7. 	Por último, seleccione la velocidad de enlace ascendente de red que desee.
8.	Revise las selecciones y luego pulse **Añadir a pedido**. Su pedido se verificará automáticamente.
9.	En la página **Pago**, si ya dispone de VLAN en el centro de datos seleccionado, seleccione las VLAN de fondo que desee proteger. No olvide:
	* Proporcione un nombre de host y un nombre de dominio para el servidor.
	* Seleccionar una clave SSH para la autenticación de acceso, si lo desea.
	* Marque todos los recuadros correspondientes a las condiciones de servicio de IBM Cloud y a las condiciones de software de terceros.
10. Pulse **Enviar pedido**.

## Qué hacer a continuación
{: #what-s-next-}

Cuando se haya aprobado el pedido, el suministro de vSRX se iniciará automáticamente. Cuando se haya completado el proceso de suministro, la nueva pasarela se mostrará en la página de lista **Dispositivos de pasarela**.

Pulse el nombre de la pasarela para abrir la página **Detalles de pasarela**. Encontrará las direcciones IP, el nombre de usuario de inicio de sesión y las contraseñas para el dispositivo.

<img src="images/after_order.png" alt="dibujo" style="width: 700px;"/>
