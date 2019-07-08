---

copyright:
  years: 2018
lastupdated: "2018-11-06"

keywords: working, vpn, sample, configuration

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

# VPN の操作
{: #working-with-vpn}

このトピックでは、2 つのサイト間の経路ベース VPN のサンプル構成について詳しく説明します。 このサンプルでは、構成サーバー 1 (サイト A) はサーバー 2 (サイト B) と通信でき、各サイトは 2 フェーズの IPSEC 認証を使用します。

<img src="images/site-to-site-vpn.png" alt="図面" style="width: 600px;"/>

## サイト A (ダラス) のサンプル構成:
{: #sample-configuration-for-site-a-dallas-}

```
# show security address-book global address Network-A
10.84.237.200/29;
[edit]
# show security address-book global address Network-B
10.45.53.48/29;
# show security ike
proposal IKE-PROP {
    authentication-method pre-shared-keys;
    dh-group group5;
    authentication-algorithm sha1;
    encryption-algorithm aes-128-cbc;
    lifetime-seconds 3600;
}
policy IKE-POL {
    mode main;
    proposals IKE-PROP;
    pre-shared-key ascii-text "$9$ewkMLNs2aikPdbkP5Q9CKM8"; ## SECRET-DATA
}
gateway IKE-GW {
    ike-policy IKE-POL;
    address 158.100.100.100;
    external-interface ge-0/0/1.0;
}
#show security ipsec
proposal IPSEC-PROP {
    protocol esp;
    authentication-algorithm hmac-sha1-96;
    encryption-algorithm aes-128-cbc;
    lifetime-seconds 3600;
}
policy IPSEC-POL {
    perfect-forward-secrecy {
        keys group5;
    }
    proposals IPSEC-PROP;
}
vpn IPSEC-VPN {
    bind-interface st0.1;
    vpn-monitor;
    ike {
        gateway IKE-GW;
        ipsec-policy IPSEC-POL;
    }
    establish-tunnels immediately;
}
#show interfaces
ge-0/0/0 {
    description PRIVATE_VLANs;
    flexible-vlan-tagging;
    native-vlan-id 1121;
    unit 0 {
        vlan-id 1121;
        family inet {
            address 10.184.108.158/26;
        }
    }
    unit 10 {
        vlan-id 1811;
        family inet {
            address 10.184.237.201/29;
        }
    }
    unit 20 {
        vlan-id 1812;
        family inet {
            address 10.185.48.9/29;
        }
    }
}
st0 {
    unit 1 {
        family inet {
            address 169.254.200.0/31;
        }
    }
#show security policies
from-zone CUSTOMER-PRIVATE to-zone VPN {
    policy Custprivate-to-VPN {
        match {
            source-address any;
            destination-address Network-B;
            application any;
        }
        then {
            permit;
        }
    }
}
from-zone VPN to-zone CUSTOMER-PRIVATE {
    policy VPN-to-Custprivate {
        match {
            source-address Network-B;
            destination-address any;
            application any;
        }
        then {
            permit;
        }
    }
```

## サイト B (ロンドン) のサンプル構成:
{: #sample-configuration-for-site-b-london-}

```
# show interfaces
ge-0/0/0 {
    description PRIVATE_VLANs;
    flexible-vlan-tagging;
    native-vlan-id 822;
    unit 0 {
        vlan-id 822;
        family inet {
            address 10.45.165.140/26;
        }
    }
    unit 10 {
        vlan-id 821;
        family inet {
            address 10.45.53.49/29;
        }
    }
}
st0 {
    unit 1 {
        family inet {
            address 169.254.200.1/31;
        }
    }
#show security ike
proposal IKE-PROP {
    authentication-method pre-shared-keys;
    dh-group group5;
    authentication-algorithm sha1;
    encryption-algorithm aes-128-cbc;
    lifetime-seconds 3600;
}
policy IKE-POL {
    mode main;
    proposals IKE-PROP;
    pre-shared-key ascii-text "$9$H.fz9A0hSe36SevW-dk.P"; ## SECRET-DATA
}
gateway IKE-GW {
    ike-policy IKE-POL;
    address 169.100.100.100;
    external-interface ge-0/0/1.0;
}
# show security ipsec
proposal IPSEC-PROP {
    protocol esp;
    authentication-algorithm hmac-sha1-96;
    encryption-algorithm aes-128-cbc;
    lifetime-seconds 3600;
}
policy IPSEC-POL {
    perfect-forward-secrecy {
        keys group5;
    }
    proposals IPSEC-PROP;
}
vpn IPSEC-VPN {
    bind-interface st0.1;
    vpn-monitor;
    ike {
        gateway IKE-GW;
        ipsec-policy IPSEC-POL;
    }
    establish-tunnels immediately;
}
#show security zone security-zone CUSTOMER_PRIVATE
security-zone CUSTOMER-PRIVATE {
    interfaces {
        ge-0/0/0.10 {
            host-inbound-traffic {
                system-services {
                    all;
                }
            }
        }
    }
}
security-zone VPN {
    interfaces {
        st0.1;
    }
}
#show security policies from-zone CUSTOMER-PRIVATE to-zone VPN
policy Custprivate-to-VPN {
    match {
        source-address any;
        destination-address Network-A;
        application any;
    }
    then {
        permit;
    }
}
 #show security zones security-zone VPN
interfaces {
    st0.1;
}
#show security policies from-zone VPN to-zone CUSTOMER-PRIVATE
policy VPN-to-Custprivate {
    match {
        source-address Network-A;
        destination-address any;
        application any;
    }
    then {
        permit;
    }
}
```
## パフォーマンスの考慮
{: #performance-consideration}

IPSEC VPN のパフォーマンスを最大限に生かすには、IKE および IPSEC プロポーザルの両方の暗号化アルゴリズムとして AES-GCM を使用します。

以下に例を示します。

```
set security ike proposal IKE-PROP encryption-algorithm aes-128-gcm
set security ipsec proposal IPSEC-PROP encryption-algorithm aes-128-gcm
```

暗号化アルゴリズムとして AES-GCM を使用する場合、同じプロポーザルで認証アルゴリズムを指定する必要はありません。 AES-GCM は、暗号化と認証の両方を提供します。

## 追加の VPN 構成
{: #additional-vpn-configurations}

IPSEC VPN、サイト間 VPN、リモート・アクセス VPN、およびその他の機能を構成するには、Juniper のこちらの[構成ガイド![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.juniper.net/documentation/en_US/junos/information-products/pathway-pages/security/security-vpn-ipsec.pdf){: new_window}を参照してください。

経路ベースのサイト間 IPSEC VPN を構成する方法の例については、Juniper のこちらの[構成ガイド![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.juniper.net/documentation/en_US/junos/topics/example/ipsec-route-based-vpn-configuring.html){: new_window}を参照してください。
