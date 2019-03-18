---

copyright:
  years: 2018
lastupdated: "2018-11-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Limitaciones conocidas de IBM Cloud Juniper vSRX
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

Limitaciones actuales de {{site.data.keyword.cloud}} IBM® Cloud Juniper vSRX:

* Juniper vSRX Gateway se despliega con virtualización de red utilizando Linux Bridge. La virtualización de red mediante Linux Bridge solo puede conseguir un rendimiento limitado y nunca el rendimiento de la tasa de la línea.

* No hay soporte para actualizar de la modalidad autónoma a la de alta disponibilidad.

* IBM Cloud Juniper vSRX Gateway se despliega con Junos OS versión `15.1X49-D123`. Actualmente, no hay soporte para actualizar a otra versión.
