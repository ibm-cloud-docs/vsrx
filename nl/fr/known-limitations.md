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

# Limitations connues pour IBM Cloud Juniper vSRX
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

Limites actuelles d'{{site.data.keyword.cloud}}IBM® Cloud Juniper vSRX :

* La passerelle Juniper vSRX est déployée à l'aide de la virtualisation de réseau sous Linux Bridge. La virtualisation de réseau basée sur Linux Bridge ne permet d'atteindre qu'un débit limité et non un débit de ligne.

* Aucune prise en charge n'est proposée pour passer du mode autonome au mode haute disponibilité.

* La passerelle IBM Cloud Juniper vSRX est déployée avec Junos OS version `15.1X49-D123`. Actuellement, la mise à niveau vers une version différente n'est pas prise en charge.
