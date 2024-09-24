---

copyright:
  years: 2017, 2024
lastupdated: "2024-09-24"

keywords: working, vpn, sample, configuration

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Working with VPN
{: #working-with-vpn}

This topic details a sample configuration for a Route-based IPSec VPN between two sites. In this sample configuration, Server 1 (Site A) can communicate with Server 2 (Site B), and each site utilizes two phase IPSEC authentication.
{: shortdesc}

![Site-to-site VPN](images/site-to-site-vpn.png){: caption="Site-to-site VPN" caption-side="bottom"}

When setting up IPSec VPN tunnels, it is common to use the primary public IP of the vSRX as the IKE gateway local-address. However, it is recommended that you first [order a public static subnet/IP](/docs/subnets?topic=subnets-order-subnets&interface=ui) and route it to the primary public IP of the vSRX. You should also use that IP address as the IKE gateway local-address. If you then need to migrate the IPSev VPN tunnels, you can then keep the IP address and route it to a different gateway appliance. 

While migrating the primary IP of a vSRX or gateway appliance to a different one is not supported, [migrating a secondary static subnet](/docs/subnets?topic=subnets-re-routing-secondary-subnets&interface=ui) within the same datacenter is.
{: tip}

## Sample configuration for Site A (Dallas):
{: #sample-configuration-for-site-a-dallas-}

```sh
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
# show interfaces
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
# show security policies
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

## Sample configuration for Site B (London):
{: #sample-configuration-for-site-b-london-}

```sh
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
# show security zone security-zone CUSTOMER_PRIVATE
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
# show security policies from-zone CUSTOMER-PRIVATE to-zone VPN
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
 # show security zones security-zone VPN
interfaces {
    st0.1;
}
# show security policies from-zone VPN to-zone CUSTOMER-PRIVATE
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

## Performance consideration
{: #performance-consideration}

In order to achieve the best IPSEC VPN performance, use AES-GCM as the encryption algorithm for both IKE and IPSEC proposals.

For example:

```sh
set security ike proposal IKE-PROP encryption-algorithm aes-128-gcm
set security ipsec proposal IPSEC-PROP encryption-algorithm aes-128-gcm
```

With AES-GCM as the encryption algorithm, you don't need to specify the authentication algorithm in the same proposal. AES-GCM provides both encryption and authentication.

## Troubleshooting commands
{: #troubleshooting-commands}

```sh
#show phase 1 status:
show security ike sa

#show phase 2 status:
show security ipsec sa

#show information for any inactive/erroring tunnels
show security ipsec inactive-tunnels
 
#send ipsec logs to file kmd-logs:
set system syslog file kmd-logs daemon info
set system syslog file kmd-logs match KMD

#show the contents of the log file created above:
show log kmd-logs

#enabling debug logging and viewing those logs
show security ike debug-status
request security ike debug-enable local <local-ip-address> remote <remote-ip-address> level <1-15>
show log kmd

#disable debug logging - this is important for avoiding performance issues
request security ike debug-disable
```

## Examples of troubleshooting commands
{: #troubleshooting-commands-examples}

```sh
admin@siferg0-vsrx-vsrx-vSRX> show security ike sa
node0:
--------------------------------------------------------------------------
Index   State  Initiator cookie  Responder cookie  Mode           Remote Address
2859401 UP     f514114a799925fe  f8de58a2690993d7  IKEv2          128.168.104.229
 
admin@siferg0-vsrx-vsrx-vSRX> show security ipsec sa
node0:
--------------------------------------------------------------------------
  Total active tunnels: 1     Total Ipsec sas: 1
  ID    Algorithm       SPI      Life:sec/kb  Mon lsys Port  Gateway
  <131073 ESP:aes-gcm-128/None ec78f80e 2528/ unlim - root 500 128.168.104.229
  >131073 ESP:aes-gcm-128/None c674a8ac 2528/ unlim - root 500 128.168.104.229
 
{primary:node0}
 
admin@siferg0-vsrx-vsrx-vSRX> show security ipsec inactive-tunnels
node0:
--------------------------------------------------------------------------
  Total inactive tunnels: 0
  Total inactive tunnels with establish immediately: 0
 
{primary:node0}
admin@siferg0-vsrx-vsrx-vSRX> show security ike security-associations
node0:
--------------------------------------------------------------------------
Index   State  Initiator cookie  Responder cookie  Mode           Remote Address
2859309 DOWN   e7753a11ff890094  0000000000000000  IKEv2          128.168.104.229
 
{primary:node0}
admin@sifergu0-vsrx-vsrx-vSRX> show security ipsec inactive-tunnels
node0:
--------------------------------------------------------------------------
  Total inactive tunnels: 1
  Total inactive tunnels with establish immediately: 1
  ID           Port   Gateway          Pending SAs   Tunnel Down Reason
  131073       500    128.168.104.229  1             No response from peer. Negotiation failed (130 times)
 
{primary:node0}
```

## Additional VPN configurations
{: #additional-vpn-configurations}

To configure IPSec VPN, site to site, remote access VPN, and other features, refer to this [configuration guide](https://www.juniper.net/documentation/us/en/software/junos/vpn-ipsec/vpn-ipsec.pdf){: external} from Juniper.

For an example of how to configure a route-based site to site IPSec VPN, refer to this [configuration guide](https://www.juniper.net/documentation/us/en/software/junos/vpn-ipsec/topics/topic-map/security-route-based-ipsec-vpns.html#id-example-configuring-a-route-based-vpn){: external} from Juniper.
