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

# Cómo trabajar con cortafuegos
{: #working-with-firewalls}

IBM® Cloud Juniper vSRX utiliza el concepto de zonas de seguridad, donde cada interfaz vSRX está correlacionada con una "zona" para gestionar los cortafuegos con estado. Los cortafuegos sin estado se controlan mediante filtros de cortafuegos.

Se utilizan políticas para permitir y bloquear el tráfico entre estas zonas definidas, y las reglas definidas aquí son con estado.

En IBM Cloud, un vSRX está diseñado para que tenga cuatro zonas de seguridad diferentes:

| Zona                     | Interfaz autónoma | Interfaz HA |
| :---                     |        :----:        |         ---: |
| SL-Private (sin etiquetar)    | ge-0/0/0.0           | reth0.0      |
| SL-Public (sin etiquetar )     | ge-0/0/1.0           | reth1.0      |
| Customer-Private (etiquetada)| ge-0/0/0.1           | reth2.1      |
| Customer-Public (etiquetada) | ge-0/0/1.1           | reth3.1      |

## Políticas de zona
Para configurar un cortafuegos con estado, lleve a cabo el procedimiento siguiente:

1. Cree zonas de seguridad y asigne las interfaces respectivas:

	Escenario autónomo:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces ge-0/0/1.1
	```
	Escenario de alta disponibilidad:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces reth2.1
	```
2. Defina la política y las reglas entre dos zonas distintas.

	En el ejemplo siguiente se muestra cómo ejecutar ping sobre el tráfico desde la zona `Customer-Private` a `Customer-Public`:

	```
	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP match source-address any destination-address any application junos-icmp

	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP then permit
	```

En las políticas se pueden definir algunos atributos:

* Direcciones de origen
* Direcciones de destino
* Aplicaciones
* Acción (permit/deny/reject/count/log)

Puesto que se trata de una operación con estado, no es necesario permitir los paquetes de retorno (en este caso, las respuestas de eco).

Utilice los siguientes mandatos para permitir el tráfico dirigido a vSRX:

Escenario autónomo:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.0 host-inbound-traffic system-services all
```
Escenario de alta disponibilidad:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.0 host-inbound-traffic system-services all
```

Para permitir protocolos, como por ejemplo OSPF o BGP, utilice el mandato siguiente:

Escenario autónomo:
```
set security zones security-zone trust interfaces ge-0/0/0.0 host-inbound-traffic protocols all
```
Escenario de alta disponibilidad:
```
set security zones security-zone trust interfaces reth2.0 host-inbound-traffic protocols all
```

## Filtros de cortafuegos
De forma predeterminada, IBM Cloud Juniper vSRX permite ping, SSH y HTTPS a sí mismo y descarta el resto del tráfico mediante la aplicación del filtro `PROTECT-IN` a la interfaz `lo`.

Para configurar un nuevo cortafuegos sin estado, siga este procedimiento:

1. Cree el filtro y la duración del cortafuegos (el siguiente filtro solo permitirá ICMP y descartará el resto del tráfico)
	```
	set firewall filter ALLOW-PING term ICMP from protocol icmp
	set firewall filter ALLOW-PING term ICMP then accept
	```

2. Aplique la regla de filtro a la interfaz (el mandato siguiente aplicará el filtro a todo el tráfico de red privada)
	```
	set interfaces ge-0/0/0 unit 0 family inet filter input ALLOW-PING
	```
