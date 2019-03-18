---

copyright:
  years: 2018
lastupdated: "2018-11-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Iniciación a IBM Cloud Juniper vSRX Gateway
{: #getting-started-with-ibm-cloud-juniper-vsrx-gateway}

Para empezar a trabajar con IBM® Cloud Juniper vSRX Gateway, determine en primer lugar si su cuenta está enlazada a IBM Cloud.

## Antes de empezar

Para averiguar si tiene una cuenta enlazada, vaya al [Portal de clientes ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window} en el navegador e inicie una sesión. Si su cuenta no está enlazada, verá un botón **Más información sobre Bluemix** en la parte superior derecha.

## Pasos para realizar la solicitud

Puede solicitar su dispositivo de pasarela siguiendo uno de estos métodos:

Para ver una lista de limitaciones conocidas de IBM Cloud Juniper vSRX Gateway, consulte el [tema sobre limitaciones conocidas](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx).
{:note}

### Cómo realizar la solicitud con una cuenta enlazada
Si la cuenta está enlazada, siga este procedimiento:

1.	Abra la [consola de IBM Cloud ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.bluemix.net/){: new_window} e inicie sesión en su cuenta.
2.	En el panel de navegación de la izquierda, seleccione **Infraestructura > Red > Dispositivos de pasarela**.
3.	En la lista **Dispositivos de pasarela**, pulse **Crear una pasarela**.
4. En la página **Solicitud**, elija un **Nombre de host** y un **Dominio**.
5. Seleccione la opción **Par de alta disponibilidad** si lo desea.

	<img src="images/linked_order.png" alt="dibujo" style="width: 700px;"/>

5. A continuación, seleccione su **Ubicación** y el **Pod** asociado y luego elija su **Servidor** y la cantidad de **RAM** que desee.

	Si tiene intención de utilizar un servidor de varios núcleos y dos procesadores, debe seleccionar **Intel Xeon 5120** como tipo de servidor. {:note:}

	<img src="images/linked_server.png" alt="dibujo" style="width: 600px;"/>

6. Seleccione una clave SSH si desea utilizarla para autenticar el acceso a la nueva pasarela.
7. En **Imagen**, seleccione **Juniper vSRX 15.x (hasta 1 Gbps) Estándar** para un servidor de un solo procesador o **Juniper vSRX 15.x (hasta 10 Gbps) Estándar** para un servidor de dos procesadores.
8. Seleccione los complementos opcionales, añada los **Discos de almacenamiento** adicionales y elija la **Velocidad de puerto de enlace ascendente** que desee.
8. Revise las selecciones en el **Resumen del pedido** y lea y acepte las condiciones de software de terceros.
9. Finalmente, pulse **Suministrar**.

### Cómo realizar la solicitud con una cuenta no enlazada
Si la cuenta no está enlazada, siga este procedimiento:

1.	Abra el [Portal de clientes ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window} e inicie sesión en su cuenta.
2.	En la navegación del Portal de clientes, seleccione **Red > Dispositivos de pasarela**.
3.	En la lista **Dispositivos de pasarela**, pulse **Solicitar pasarela**.
4.	En la página **Pedido**, seleccione el centro de datos que desee en el menú desplegable y elija el tipo de hardware de servidor deseado en el que se suministrará Juniper vSRX.

	Si tiene intención de utilizar un servidor de varios núcleos y dos procesadores, debe seleccionar **Intel Xeon 5120** como tipo de servidor. {:note}

5.	En la página **Pedido**, seleccione la opción **Par de alta disponibilidad** si lo desea y luego seleccione el tamaño de **Memoria**.
6. 	Luego pulse el separador **Juniper** bajo **Sistema operativo**, seleccione **Juniper vSRX 15.x (hasta 1 Gbps) Estándar** para un servidor de un solo procesador o **Juniper vSRX 15.x (hasta 10 Gbps) Estándar** para un servidor de dos procesadores.
7. 	Por último, seleccione la velocidad de enlace ascendente de red que desee.
8.	Revise las selecciones y luego pulse **Añadir a pedido**. Su pedido se verificará automáticamente.
9.	En la página **Pago**, si ya dispone de VLAN en el centro de datos seleccionado, seleccione las VLAN de fondo que desee proteger. No olvide:
	* Proporcione un nombre de host y un nombre de dominio para el servidor
	* Seleccionar una clave SSH para la autenticación de acceso, si lo desea
	* Marcar todos los recuadros correspondientes a las condiciones de servicio de IBM Cloud y a las condiciones de software de terceros
10. Pulse **Enviar pedido**.

## Qué hacer a continuación
Cuando se haya aprobado el pedido, el suministro de vSRX se iniciará automáticamente. Cuando se haya completado el proceso de suministro, la nueva pasarela se mostrará en la página de lista **Dispositivos de pasarela**.

Pulse el nombre de la pasarela para abrir la página **Detalles de pasarela**. Encontrará las direcciones IP, el nombre de usuario de inicio de sesión y las contraseñas para el dispositivo.

<img src="images/after_order.png" alt="dibujo" style="width: 700px;"/>
