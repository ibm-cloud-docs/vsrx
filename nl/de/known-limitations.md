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

# Bekannte Einschränkungen

Aktuelle Einschränkungen für Juniper vSRX für {{site.data.keyword.cloud}} IBM® Cloud:

* Das Gateway Juniper vSRX wird mit Netzvirtualisierung über die Linux-Bridge bereitgestellt. Die auf der Linux-Bridge basierende Netzvirtualisierung erreicht nur einen begrenzten Durchsatz und niemals einen Durchsatz mit Übertragungsgeschwindigkeit.

* Für die Durchführung eines Upgrades vom eigenständigen Modus in den Hochverfügbarkeitsmodus steht keine Unterstützung bereit.

* Das Gateway Juniper vSRX für IBM Cloud wird mit der Junos-Betriebssystemversion `15.1X49-D123` bereitgestellt. Derzeit gibt es keine Unterstützung für ein Upgrade auf eine andere Version.
