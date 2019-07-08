---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: working, routing, static, default, creating, ospf, bgp

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

# 経路指定の処理
{: #working-with-routing}

IBM® Cloud Juniper vSRX は `JunOS` に基づいており、Juniper ルーティング・スタックへのフル・アクセスを可能にします。

##静的経路指定
{: #static-routing}

静的ルートを構成するには、以下のコマンドを実行します。

###デフォルト・ルートの設定
{: #setting-a-default-route}

```
set routing-options static route 0/0 next-hop <Gateway IP>
```

### 静的ルートの作成
{: #creating-a-static-route}
```
set routing-options static route <PREFIX/MASK> next-hop <Gateway IP>
```  

###基本 OSPF ルーティング
{: #basic-ospf-routing}

エリア 0 のみを使用して基本 OSPF ルーティングをセットアップするには、md5 認証を使用して以下のコマンドを実行します。

```
set protocols ospf area 0 interface ge-0/0/1.0 authentication md5 0 key <KEY>
```

### 基本 BGP ルーティング
{: #basic-bgp-routing}

基本 BGP ルーティングをセットアップするには、まず以下のようにローカル AS を定義します。

```
set routing-options autonomous-system 65001
```

次に、BGP 近隣とそのセッション属性を構成します。

```
set protocols bgp group CUSTOMER local-address 1.1.1.1
set protocols bgp group CUSTOMER family inet unicast
set protocols bgp group CUSTOMER family inet6 unicast
set protocols bgp group CUSTOMER peer-as 65002
set protocols bgp group CUSTOMER neighbor 2.2.2.2
```

この例では、以下のために BGP を構成します。

* ソース IP アドレス `1.1.1.1` を使用したセッションの確立
* ipv4 と ipv6 の両方のユニキャスト・ファミリーのネゴシエーション
* `AS 65002` に属する近隣とのピア接続
* ピア近隣 IP `2.2.2.2`

追加構成は、[Juniperの Web サイト![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.juniper.net/documentation/en_US/junos11.4/information-products/topic-collections/config-guide-routing/config-guide-routing.pdf){: new_window}にあります。
