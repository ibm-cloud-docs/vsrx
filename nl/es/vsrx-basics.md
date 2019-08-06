---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: basics, performing, accessing, ssh, device, gateway, configuration, mode, juniper, ui, dns, htp, password

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

# Conceptos básicos sobre el funcionamiento de {{site.data.keyword.vsrx_full}}
{: #performing-ibm-cloud-juniper-vsrx-basics}

La pasarela {{site.data.keyword.vsrx_full}} se puede configurar mediante una sesión de consola remota a través de SSH o mediante el inicio de sesión en la GUI de gestión de web de Juniper.

La configuración de vSRX fuera de su shell e interfaz puede producir resultados inesperados y no se recomienda.{: note}

## Acceso al dispositivo mediante SSH
{: #accessing-the-device-using-ssh}

Puede acceder a vSRX mediante SSH a través de una dirección IP pública o a través de una dirección IP privada si está en un VPN SoftLayer:

1. Vaya a la pantalla Detalles del dispositivo de pasarela y obtenga la IP de pasarela pública o la IP de pasarela privada.

  <img src="images/gw-sa-details.png" alt="dibujo" style="width: 700px;"/>

2. Pulse el icono con un "ojo" para ver la contraseña del usuario administrador.

3. Ejecute el mandato `ssh admin@<gateway-ip>` y escriba la contraseña del usuario administrador.

Si no ve el icono de "ojo", es posible que no tenga permiso para ver la contraseña. Compruebe los permisos de acceso con el propietario de la cuenta.
{: note}

## Acceso a la modalidad de configuración
{: accessing-the-configuration-mode}

Puede entrar en la modalidad de configuración, una vez que se haya abierto un shell en vSRX, con el mandato `config`. Puede hacer varias cosas en esta modalidad con los mandatos siguientes:

* `show` - Ver configuraciones  
* `show | compare` - Ver cambios por etapas
* `set` - Realizar cambios por etapas
* `commit check` - Verificar la sintaxis de la configuración

Si está satisfecho con los cambios, puede confirmarlos en la configuración activa con los mandatos `commit` y luego `save`.  

Para salir de la modalidad de configuración, ejecute el mandato `exit`.

## Acceso al dispositivo mediante la interfaz de usuario de gestión de web de Juniper
{: #accessing-the-device-using-the-juniper-web-management-ui}

La GUI de gestión de web de Juniper se ha configurado de forma predeterminada con un certificado autofirmado generado por vSRX. Solo https está habilitado en el puerto 8443. Puede acceder en `https://gateway-ip:8443`.

![Detalles del dispositivo de pasarela de alta disponibilidad](images/vSRX-webui.png)

## Creación de usuarios del sistema
{: #creating-system-users}

De forma predeterminada, {{site.data.keyword.vsrx_full}} está configurado con acceso SSH para el nombre de usuario `admin`. Se pueden añadir más usuarios con su propio conjunto de prioridades. Por ejemplo:

```
set system login user ops class operator authentication encrypted-password <CYPHER>
```

En este ejemplo, `ops` es el nombre de usuario y `operator` es el nivel de clase/permiso asignado al usuario.

También se pueden definir clases personalizadas, en contraposición a las predefinidas.

## Definición del nombre de host de vSRX
{: #defining-the-vsrx-hostname}

Puede definir o cambiar el nombre de host de vSRX con el mandato siguiente:

```
set system host-name <hostname>
```

## Configuración de DNS y NTP
{: #configuring-dns-and-ntp}

Para configurar la resolución del servidor de nombres y NTP, ejecute los mandatos siguientes:

```
set system name-server <DNS server>
set system ntp <NTP server>
```

## Cambio de la contraseña de root
{: #changing-the-root-password}

Puede cambiar la contraseña de root con el mandato siguiente:

```
set system root-authentication plain-text-password
```

Esto le solicita que especifique una nueva contraseña, que se cifra y se almacena en la configuración, y que no resulta visible.
