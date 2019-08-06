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

# {{site.data.keyword.vsrx_full}} の基本操作の実行
{: #performing-ibm-cloud-juniper-vsrx-basics}

{{site.data.keyword.vsrx_full}} ゲートウェイは、SSH 経由で、または Juniper Web 管理 GUI にログインして、リモート・コンソール・セッションを使用して構成できます。

vSRX をシェルおよびインターフェースの外部で構成すると予期しない結果が生じる可能性があるため、推奨されません。
{: note}

## SSH を使用したデバイスへのアクセス
{: #accessing-the-device-using-ssh}

パブリック IP アドレスを介して、SSH を使用して vSRX にアクセスできます。SoftLayer VPN の場合はプライベート IP アドレスを介してアクセスできます。

1. 「ゲートウェイ・アプライアンスの詳細 (Gateway Appliance Details)」画面に移動し、パブリック・ゲートウェイ IP またはプライベート・ゲートウェイ IP を取得します。

  <img src="images/gw-sa-details.png" alt="図面" style="width: 700px;"/>

2. 「目」の形のアイコンをクリックして管理ユーザーのパスワードを表示します。

3. コマンド `ssh admin@<gateway-ip>` を実行して、管理ユーザーのパスワードを入力します。

「目」の形のアイコンが表示されない場合は、パスワードを表示する権限がない可能性があります。アカウント所有者にアクセス権限について確認してください。
{: note}

## 構成モードへのアクセス
{: accessing-the-configuration-mode}

vSRX に対してシェルが開かれたら、`config` コマンドを実行して構成モードに入ることができます。 このモードでは、以下のコマンドを使用していくつかの操作を実行できます。

* `show` - 構成の表示  
* `show | compare` - ステージングされた変更の表示
* `set` - ステージの変更
* `commit check` - 構成の構文の確認

変更内容に問題がなければ、コマンド `commit` を実行してから `save` を実行して、変更をアクティブ構成にコミットできます。  

構成モードを終了するには、コマンド `exit` を実行します。

## Juniper Web 管理 UI を使用したデバイスへのアクセス
{: #accessing-the-device-using-the-juniper-web-management-ui}

Juniper Web 管理 GUI は、デフォルトで vSRX で生成された自己署名証明書を使用して構成されています。 ポート 8443 では https のみが有効です。 `https://gateway-ip:8443` からアクセスできます。

![ゲートウェイ・アプライアンス HA の詳細](images/vSRX-webui.png)

## システム・ユーザーの作成
{: #creating-system-users}

デフォルトでは、{{site.data.keyword.vsrx_full}} は、ユーザー名 `admin` の SSH アクセスで構成されます。 ユーザーを追加し、独自の優先順位を設定することもできます。 以下に例を示します。

```
set system login user ops class operator authentication encrypted-password <CYPHER>
```

この例では、`ops` はユーザー名で、`operator` はそのユーザーに割り当てられたクラス/権限レベルです。

事前定義クラスではなく、カスタマイズしたクラスを定義することもできます。

## vSRX ホスト名の定義
{: #defining-the-vsrx-hostname}

以下のコマンドを使用して、vSRX ホスト名を設定または変更できます。

```
set system host-name <hostname>
```

## DNS および NTP の構成
{: #configuring-dns-and-ntp}

ネーム・サーバー解決および NTP を構成するには、以下のコマンドを実行します。

```
set system name-server <DNS server>
set system ntp <NTP server>
```

## ルート・パスワードの変更
{: #changing-the-root-password}

以下のコマンドを実行して、ルート・パスワードを変更できます。

```
set system root-authentication plain-text-password
```

これにより、新規パスワードの入力を求めるプロンプトが出されます。このパスワードは表示されず、暗号化されて構成に保管されます。
