---

copyright:
  years: 2018
lastupdated: "2018-11-06"

keywords: limitations, problems

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

# IBM Cloud Juniper vSRX の既知の制限事項
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

{{site.data.keyword.cloud}} Juniper vSRX の現在の制限事項は以下のとおりです。

* Juniper vSRX ゲートウェイは、Linux ブリッジを使用するネットワーキング仮想化と共にデプロイされます。 Linux ブリッジ・ベースのネットワーキング仮想化で実現できるスループットは限られており、回線速度のスループットは全く実現できません。

* スタンドアロン・モードから高可用性モードへのアップグレードはサポートされていません。

* IBM Cloud Juniper vSRX ゲートウェイは、Junos OS バージョン `15.1` または `18.4` のいずれかと共にデプロイされます。現在、別のバージョンへのアップグレード/ダウングレードはサポートされていません。

* システム上に別の (有効な) ライセンスがあるとしても、60 日間の評価ライセンスを使用すると、カーネルがエラー・メッセージを生成する場合があります。この問題を回避するには、60 日間の評価ライセンスを削除する必要があります。これを行うには、以下の手順を実行します。

1. vSRX ゲートウェイ・デバイスにログインします。

2. コンソール・プロンプトで、`cli` コマンドを実行して、CLI モードに入ります。 

3. 次のコマンドを実行してライセンス ID を取得します。

```
show system license
```
出力は以下のようになります。

```
License usage:
                                 Licenses     Licenses    Licenses    Expiry
  Feature name                       used    installed      needed
  logical-system                        0            3           0    permanent
  Virtual Appliance                     1            1           0    2021-10-18 00:00:00 UTC
  remote-access-ipsec-vpn-client        0            2           0    permanent

Licenses installed:
  License identifier: E2018101804
  License version: 4
  Software Serial Number: SUB00024128768
  Customer ID: IBM_SL_10G
  Features:
    Virtual Appliance - Virtual Appliance
      date-based, 2018-10-18 00:00:00 UTC - 2021-10-18 00:00:00 UTC
```

4. 削除するライセンスの ID をコピーして、次のコマンドを実行します。

```
request system license delete <ライセンス ID>
```
