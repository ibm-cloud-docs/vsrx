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

# Limitazioni note per IBM Cloud Juniper vSRX
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

Limitazioni correnti per {{site.data.keyword.cloud}} IBM® Cloud Juniper vSRX:

* Juniper vSRX Gateway viene distribuito con la virtualizzazione della rete utilizzando Linux Bridge. La virtualizzazione della rete basata su Linux Bridge può utilizzare solo una velocità effettiva limitata e mai quella della linea.

* Non c'è supporto per l'upgrade dalla modalità autonoma alla modalità ad elevata disponibilità.

* IBM Cloud Juniper vSRX Gateway viene distribuito con il SO Junos versione `15.1X49-D123`. Al momento, non c'è supporto per l'upgrade a una versione diversa.
