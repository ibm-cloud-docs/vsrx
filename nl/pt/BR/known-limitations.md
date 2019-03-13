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

# Limitações conhecidas

Limitações atuais para o {{site.data.keyword.cloud}} IBM® Cloud Juniper vSRX:

* O gatewya Juniper vSRX é implementado com virtualização de rede usando a ponte Linux. A virtualização de rede baseada em ponte Linux pode alcançar somente um rendimento limitado e nunca o rendimento da taxa da linha.

* Não há nenhum suporte para fazer upgrade do modo independente para o modo de alta disponibilidade.

* O gateway do IBM Cloud Juniper vSRX é implementado com o S.O. Junos versão `15.1X49-D123`. Atualmente, não há suporte para fazer upgrade para uma versão diferente.
