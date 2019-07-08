---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: reloading, os, upgrading, kvm, ha, standalone

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

# Recarga del SO
{: #reloading-the-os}

El proceso de recarga del SO se utiliza para reconstruir un servidor de pasarela. El proceso realiza las acciones siguientes:

* Volver a cargar el sistema operativo del host del servidor
* Instalar KVM en el sistema operativo
* Crear una máquina virtual vSRX en KVM
* Volver a configurar el vSRX con la configuración predeterminada para IBM® Cloud

El proceso suele tardar 1 hora 40 minutos en completarse. Las pasarelas autónomas estarán fuera de servicio durante este periodo. Para pasarelas Juniper de alta disponibilidad (HA), cuando vuelve a cargar el SO en uno de los servidores, vSRX realizará una migración tras error a otro servidor del clúster y seguirá procesando el tráfico de datos. Una vez que se haya completado la recarga, el servidor se volverá a unir al clúster.

Para una Volver a cargar o Volver a crear clúster de forma satisfactoria en un vSRX de alta disponibilidad:

* La contraseña raíz de la pasarela vSRX suministrada debe coincidir con la contraseña raíz definida en el portal de vSRX. La contraseña del portal se ha definido cuando se ha suministrado por primera vez la Pasarela, y puede que no coincida con la contraseña de Pasarela actual. Si se ha cambiado la contraseña después del suministro inicial, utilice SSH para conectarse a la Pasarela vSRX y cambie la contraseña raíz para que coincida. Una vez termine con las contraseñas, puede continuar con la operación de recarga de SO o de Volver a crear clúster. 

  <img src="images/gw-vsrx-password.png" alt="dibujo" style="width: 700px;"/>

* **NO** lleve a cabo una recarga de SO en los dos servidores de la pasarela de alta disponibilidad a la vez.

Realizar una recarga de SO en los dos servidores de la pasarela de alta disponibilidad a la vez destruiría el clúster vSRX y haría que la pasarela quedara fuera de servicio. Si el clúster vSRX se destruye, debe utilizar la opción **Volver a crear clúster** (que se detalla a continuación) para volver a suministrar vSRX y volver a crear el clúster HA.
{: important}

## Realización de una recarga de SO
{: #performing-an-os-reload}

Para volver a cargar el SO para un servidor de pasarela, siga el procedimiento siguiente:

1. [Acceda a la pantalla de Dispositivos de pasarela](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) en el portal de clientes y vaya a la página de detalles de la pasarela seleccionando el nombre de pasarela que desee.

  <img src="images/gw-sa-details.png" alt="dibujo" style="width: 700px;"/>

2. Pulse el nombre del servidor en el panel de hardware.

  ![Servidor de hardware](images/os_hardware.png)

3. En la página del dispositivo, pulse **Recarga de SO** en el menú desplegable Acción para acceder a la página Configuración de servidor. 

  ![Detalles de dispositivo](images/os_device_page.png)

4. En la página Configuración de servidor, puede configurar e iniciar la recarga. Si va a realizar la recarga desde otro sistema operativo, pulse **Editar** junto a **Sistema operativo**, seleccione **Juniper** y luego seleccione una de las opciones de Juniper vSRX 15.x Estándar. Cuando haya terminado de modificar los valores, seleccione **Volver a cargar la configuración anterior** para continuar.

5. Se visualiza la pantalla de detalles de recarga de SO. Revise los valores que ha elegido y pulse **Editar valores** si es necesario realizar cambios. En caso contrario, pulse **Siguiente** para continuar.

6. En la pantalla de confirmación de recarga de SO, acepte las condiciones del Acuerdo de servicio maestro y luego inicie el proceso de recarga de SO pulsando **Confirmar recarga de SO**. Si no desea continuar con la recarga, pulse **Cancelar**.

## Cómo volver a crear un clúster HA vSRX
{: #rebuilding-an-ha-vsrx-cluster}

Para volver a crear uno de los clústeres HA vSRX, siga el procedimiento siguiente:

1. [Acceda a la pantalla de Dispositivos de pasarela](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances) en el portal de clientes y vaya a la página de detalles de la pasarela seleccionando el nombre de la pasarela HA que desee.

2. Pulse en el desplegable **Acciones** y seleccione **Volver a crear clúster**.

3. Lea detenidamente el mensaje de aviso. La operación para volver a crear un clúster es destructiva. Si desea continuar, guarde la configuración de vSRX antes de pulsar **Volver a crear** para iniciar el proceso.

  ![Confirmar recreación de clúster](images/rebuild_cluster_confirm.png)
