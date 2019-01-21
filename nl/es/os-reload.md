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

# Recarga y migración del sistema operativo
El proceso de recarga del SO se utiliza para reconstruir un servidor de pasarela. El proceso realiza las acciones siguientes:

* Volver a cargar el sistema operativo del host del servidor
* Instalar KVM en el sistema operativo
* Crear una máquina virtual vSRX en KVM
* Volver a configurar el vSRX con la configuración predeterminada para IBM® Cloud

El proceso suele tardar 1 hora 40 minutos en completarse. Las pasarelas autónomas estarán fuera de servicio durante este periodo. Para pasarelas Juniper de alta disponibilidad (HA), cuando vuelve a cargar el SO en uno de los servidores, vSRX realizará una migración tras error a otro servidor del clúster y seguirá procesando el tráfico de datos. Una vez que se haya completado la recarga, el servidor se volverá a unir al clúster.

**ATENCIÓN:** si ya está ejecutando un clúster de alta disponibilidad Juniper vSRX, no realice una recarga de SO en ambos servidores de la pasarela HA a la vez. Esto destruiría el clúster vSRX y haría que la pasarela estuviera fuera de servicio. Si el clúster vSRX se destruye, debe utilizar la opción **Volver a crear clúster** (que se detalla a continuación) para volver a suministrar vSRX y volver a crear el clúster HA.

## Realización de una recarga de SO
Para volver a cargar el SO para un servidor de pasarela, siga el procedimiento siguiente:

1. [Acceda a la pantalla de Dispositivos de pasarela](access-gateway-appliances.html) en el portal de clientes y vaya a la página de detalles de la pasarela seleccionando el nombre de pasarela que desee.

2. Pulse el nombre del servidor en el panel de hardware. ![Servidor de hardware](images/os_hardware.png)

3. En la página del dispositivo, pulse **Recarga de SO** en el menú desplegable Acción para acceder a la página Configuración de servidor. ![Detalles del dispositivo](images/os_device_page.png)

4. En la página Configuración de servidor, puede configurar e iniciar la recarga. Si va a realizar la recarga desde otro sistema operativo, pulse **Editar** junto a **Sistema operativo**, seleccione **Juniper** y luego seleccione una de las opciones de Juniper vSRX 15.x Estándar. Cuando haya terminado de modificar los valores, seleccione **Volver a cargar la configuración anterior** para continuar.

5. Se visualiza la pantalla de detalles de recarga de SO. Revise los valores que ha elegido y pulse **Editar valores** si es necesario realizar cambios. En caso contrario, pulse **Siguiente** para continuar.

6. En la pantalla de confirmación de recarga de SO, acepte las condiciones del Acuerdo de servicio maestro y luego inicie el proceso de recarga de SO pulsando **Confirmar recarga de SO**. Si no desea continuar con la recarga, pulse **Cancelar**.

## Migración desde un servidor Vyatta/VRA a un Juniper vSRX mediante recarga de SO
Si va a volver a cargar un servidor Vyatta autónomo, se suministrará un Juniper vSRX autónomo una vez que se complete la recarga de SO. Se utilizarán las mismas direcciones IP de pasarela y se restablecerá la contraseña del usuario root en el servidor host (así como la contraseña de los usuarios admin y root en vSRX).

Si va a realizar la recarga de servidores Vyatta de alta disponibilidad, debe ejecutar el mandato de `Recarga de OS` en ambos servidores de hardware. Esto instala Ubuntu 16.04. A continuación, utilice la opción Volver a crear clúster (que se detalla en la sección siguiente) para suministrar el vSRX y crear el clúster HA. Al igual que sucede con vSRX autónomo, se utilizarán las mismas direcciones IP de pasarela y se restablecerá la contraseña del usuario root en el servidor host (así como la contraseña de los usuarios admin y root en vSRX).

**ATENCIÓN:** no realice una recarga de SO en un solo servidor del clúster de alta disponibilidad Vyatta. No se da soporte a dos sistemas operativos distintos en un solo clúster HA de pasarela.

## Cómo volver a crear un clúster HA vSRX
Para volver a crear uno de los clústeres HA vSRX, siga el procedimiento siguiente:

1. [Acceda a la pantalla de Dispositivos de pasarela](access-gateway-appliances.html) en el portal de clientes y vaya a la página de detalles de la pasarela seleccionando el nombre de la pasarela HA que desee.

2. Pulse **Volver a crear clúster** en el panel de vSRX.
![Volver a crear clúster](images/rebuild_cluster.png)

3. Lea detenidamente el mensaje de aviso. La operación para volver a crear un clúster es destructiva. Si desea continuar, guarde la configuración de vSRX antes de pulsar **Volver a crear** para iniciar el proceso. ![Confirmar recreación de clúster](images/rebuild_cluster_confirm.png)
