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

# 既知の制限事項

{{site.data.keyword.cloud}} Juniper vSRX の現在の制限事項は以下のとおりです。

* Juniper vSRX ゲートウェイは、Linux ブリッジを使用するネットワーキング仮想化と共にデプロイされます。Linux ブリッジ・ベースのネットワーキング仮想化で実現できるスループットは限られており、回線速度のスループットは全く実現できません。

* スタンドアロン・モードから高可用性モードへのアップグレードはサポートされていません。

* IBM Cloud Juniper vSRX ゲートウェイは、Junos OS バージョン `15.1X49-D123` と共にデプロイされます。現在、別のバージョンへのアップグレードはサポートされていません。
