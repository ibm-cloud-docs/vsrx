---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: about, vsrx, overview, details, firewall, vpn, nat, routing, vlan

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

# {{site.data.keyword.vsrx_full}} の概要
{: #about-ibm-cloud-juniper-vsrx}

{{site.data.keyword.vsrx_full}} を使用すると、完全なルーティング・スタック、QoS やトラフィックの共有、ポリシー・ベースのルーティング、VPN などの JunOS ソフトウェア・フィーチャーにより機能するフル装備のエンタープライズ・レベルのファイアウォールを介して、プライベートとパブリックのネットワーク・トラフィックを選択的に経路指定できます。vSRX は、ベアメタル・サーバー上での実行が単純化されており、パフォーマンス、構成のしやすさ、保守における利点があります。
ハードウェアは、複数の VLAN に関連付けられたルーティング・ロードとセキュリティー・ロードを処理するようにサイズ変更され、冗長ネットワーク・リンクおよび冗長 RAID アレイと共に注文することができます。すべての vSRX フィーチャーはお客様により管理されます。

{{site.data.keyword.vsrx_full}} は、スタンドアロン・モードと高可用性 (HA) クラスターという 2 種類のモードで提供されます。

{{site.data.keyword.vsrx_full}} の追加資料については、[補足資料](/docs/infrastructure/vsrx?topic=vsrx-supplemental-ibm-cloud-juniper-vsrx-documentation)のトピックを参照してください。
{: note}

## ファイアウォール
{: #firewall}

vSRX は、プライベートとパブリックの接続トラフィックをフィルタリングすることで外部および内部の脅威から環境を保護するためにデプロイします。お客様は、(数あるアクションの中で特に) インバウンドやアウトバウンドのネットワーク・トラフィックを許可したり拒否するポリシーとルールを定義することにより vSRX を自分で管理できます。これにより、内部と外部のアプローチから自分のアプリケーションを保護します。IPv4 スタックと IPv6 スタックの両方がステートフルな方法でサポートされます。

## 仮想プライベート・ネットワーク (VPN) ゲートウェイ
{: #virtual-private-network-vpn-gateway}

vSRX をネットワーク・ゲートウェイ・デバイスとしてプロビジョニングすることにより、VPN トンネリングを使用して、オンサイト・データ・センターまたはオフィスを IBM Cloud に接続します。 IPsec サイト間 VPN トンネルを使用して、エンタープライズ・データ・センターまたはオフィスから IBM Cloud ネットワークへのセキュアな通信を行うことができます。 リモート・アクセス IPsec VPN もサポートされます。

VPN に関する詳細な構成ガイドについては、[VPN](/docs/infrastructure/vsrx?topic=vsrx-working-with-vpn#working-with-vpn) のトピック内にあるリンクを参照してください。

## ネットワーク・アドレス変換 (NAT)
{: #network-address-translation-nat-}

vSRX ゲートウェイ・アプライアンスを使用することで、パブリック・ネットワーク・インターフェースなしでアプリケーション・サーバーとデータベース・サーバーをプロビジョンしつつ、ご使用のサーバーが引き続き_送信元 NAT_ を使用してインターネットにアクセスできるようにすることができます。セキュリティーを高めるために、_宛先 NAT_ を使用して、ゲートウェイ・デバイスの内側でサーバーを保護することができます。

## エンタープライズ・レベルの経路指定
{: #enterprise-grade-routing}

vSRX は、異なる独立ネットワークで実行されている多階層アプリケーション間の接続をかなり柔軟に構築することを可能にします。BGP を使用して動的ルーティングをセットアップできます。これにより、IBM Cloud ルーターに対する独自のパブリック IP スペースを公表できます。 また、BGP により、トンネルと[直接リンク・ソリューション](/docs/infrastructure/direct-link?topic=direct-link-overview-of-direct-link-offerings#overview-of-direct-link-offerings)を混合して使用する場合に、より柔軟にカスタム・プライベート・ネットワーク構成を行うことができます。

## VLAN とゲートウェイ・アプライアンスの役割に関する概念
{: #concepts-about-vlans-and-the-gateway-appliance-s-role}

VLAN (仮想ローカル・エリア・ネットワーク) は、1 つの物理ネットワークを多数の仮想セグメントに分離するメカニズムです。便宜上、選択した複数の VLAN からのトラフィックは、単一のネットワーク・ケーブルで送信することができ、このプロセスを使用することを一般に「トランキング」と呼びます。

vSRX は 2 種類のインターフェースで管理されます。vSRX サーバーとゲートウェイ・アプライアンス・フィクスチャーです。 ゲートウェイ・アプライアンスは、ご使用の vSRX と関連付けようとしている VLAN を選択するためのインターフェース (GUI と API) を提供します。 VLAN をゲートウェイ・アプライアンスと関連付けると、VLAN とそのすべてのサブネットがご使用の vSRX に経路変更 (トランク) されるため、フィルタリング、転送、保護を制御することが可能になります。 関連付けられた VLAN 内のサーバーは、ご使用の vSRX を介してのみ、他の VLAN から到達することが可能になります。つまり、VLAN をバイパスするか関連付けを解除しない限り、vSRX を回避することはできません。

デフォルトでは、新しいゲートウェイ・アプライアンスは、リムーバブルではない 2 つの「トランジット」VLAN (_パブリック_・ネットワークと_プライベート_・ネットワーク 1 つずつ) に関連付けられます。 通常これらのネットワークは管理に使用され、vSRX コマンドによって個別に保護できます。

vSRX は、ゲートウェイ・アプライアンス (のみ) を介して関連付けられた VLAN を管理できます。

**「ゲートウェイ・アプライアンスの詳細 (Gateway Appliances Details)」**画面から VLAN を管理する方法については、[VLAN の管理](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans)のトピックを参照してください。
