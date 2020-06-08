---

copyright:
  years: 2018
lastupdated: "2019-11-14"

keywords: understanding, default, configuration, standalone, ha

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# Understanding the vSRX default configuration
{: #understanding-the-vsrx-default-configuration}

{{site.data.keyword.vsrx_full}} devices come with following default configuration:
{: shortdesc}

  * SSH and Ping are permitted on both vSRX public and private gateway IP addresses
  * Juniper Web Management (J-Web) UI access is permitted on HTTPS port 8443 for both public and private gateway IP addresses
  * An address-set `SERVICE` is predefined for IBM service networks
  * Two security zones: `SL-PRIVATE` and `SL-PUBLIC` are predefined.
  * Access from the zone `SL-PRIVATE` to all services is provided by IBM and address-set `SERVICE` is permitted
  * All other network accesses are denied

Two redundancy groups are configured. The following table illustrates these redundancy groups:

| Redundancy group   |  Redundancy group function      |
| :---          |    :---         |
| redundancy-group 0   |  Redundancy group for control plane |
| redundancy-group 1   |  Redundancy group for data plane |

Priority in the redundancy group decides which vSRX node is active. By default, node 0 is active for both control plane and data plane.

## Default Configuration of a sample 1G Standalone SR-IOV Public and Private vSRX Gateway
{: #default-configuration-of-a-sample-standalone-vsrx-gateway}

The following code samples are examples from the latest code release.
{: note}

```
## Last commit: 2020-04-28 00:32:27 UTC by root
version 18.4R1-S1.3;
system {
    login {
        class security {
            permissions [ security-control view-configuration ];
        }
        user admin {
            uid 2000;
            class super-user;
            authentication {
                encrypted-password "$6$5gPuIk9u$JPzyjh5zVz0tf4P3.POWv4UWGDfowbzirGmnpiBUW0tDWLf1ZfvP.YwN88Mc8.cyOIvgDMrksbCYsmZxf4f3p."; ## SECRET-DATA
            }
        }
    }
    root-authentication {
        encrypted-password "$6$q9tQzuqT$/TFQLkHK.woO.Qv9YcZ1nnJqZqhLBqXeg7L3xkUWXVmq8fn4N7mClTpckoCKhombXucxU6StRKOiHTDUeTdd91"; ## SECRET-DATA
    }
    services {
        ssh {
            root-login allow;
        }
        netconf {
            ssh {
                port 830;
            }
        }
        web-management {
            http {
                interface fxp0.0;
            }
            https {
                port 8443;
                system-generated-certificate;
                interface [ fxp0.0 ae0.0 ae1.0 ge-0/0/0.0 ge-0/0/1.0 ];
            }
            session {
                session-limit 100;
            }
        }
    }
    host-name asloma-swap-18-1g-sa0-vsrx-vSRX;
    name-server {
        10.0.80.11;
        10.0.80.12;
    }
    syslog {
        user * {
            any emergency;
        }
        file messages {
            any any;
            authorization info;
        }
        file interactive-commands {
            interactive-commands any;
        }
    }
    ntp {
        server 10.0.77.54;
    }
}
chassis {
    aggregated-devices {
        ethernet {
            device-count 10;
        }
    }
}
security {
    log {
        mode stream;
        report;
    }
    address-book {
        global {
            address SL8 10.1.192.0/20;
            address SL9 10.1.160.0/20;
            address SL4 10.2.128.0/20;
            address SL5 10.1.176.0/20;
            address SL6 10.1.64.0/19;
            address SL7 10.1.96.0/19;
            address SL1 10.0.64.0/19;
            address SL2 10.1.128.0/19;
            address SL3 10.0.86.0/24;
            address SL20 10.3.80.0/20;
            address SL18 10.2.176.0/20;
            address SL19 10.3.64.0/20;
            address SL16 10.2.144.0/20;
            address SL17 10.2.48.0/20;
            address SL14 10.1.208.0/20;
            address SL15 10.2.80.0/20;
            address SL12 10.2.112.0/20;
            address SL13 10.2.160.0/20;
            address SL10 10.2.32.0/20;
            address SL11 10.2.64.0/20;
            address SL_PRIV_MGMT 10.188.111.70/32;
            address SL_PUB_MGMT 169.60.101.121/32;
            address-set SERVICE {
                address SL8;
                address SL9;
                address SL4;
                address SL5;
                address SL6;
                address SL7;
                address SL1;
                address SL2;
                address SL3;
                address SL20;
                address SL18;
                address SL19;
                address SL16;
                address SL17;
                address SL14;
                address SL15;
                address SL12;
                address SL13;
                address SL10;
                address SL11;
            }
        }
    }
    screen {
        ids-option untrust-screen {
            icmp {
                ping-death;
            }
            ip {
                source-route-option;
                tear-drop;
            }
            tcp {
                syn-flood {
                    alarm-threshold 1024;
                    attack-threshold 200;
                    source-threshold 1024;
                    destination-threshold 2048;
                    queue-size 2000; ## Warning: 'queue-size' is deprecated
                    timeout 20;
                }
                land;
            }
        }
    }
    policies {
        from-zone SL-PRIVATE to-zone SL-PRIVATE {
            policy Allow_Management {
                match {
                    source-address any;
                    destination-address [ SL_PRIV_MGMT SERVICE ];
                    application any;
                }
                then {
                    permit;
                }
            }
        }
        from-zone SL-PUBLIC to-zone SL-PUBLIC {
            policy Allow_Management {
                match {
                    source-address any;
                    destination-address SL_PUB_MGMT;
                    application [ junos-ssh junos-https junos-http junos-icmp-ping ];
                }
                then {
                    permit;
                }
            }
        }
    }
    zones {
        security-zone SL-PRIVATE {
            interfaces {
                ae0.0 {
                    host-inbound-traffic {
                        system-services {
                            all;
                        }
                    }
                }
            }
        }
        security-zone SL-PUBLIC {
            interfaces {
                ae1.0 {
                    host-inbound-traffic {
                        system-services {
                            all;
                        }
                    }
                }
            }
        }
    }
}
interfaces {
    ge-0/0/0 {
        ether-options {
            802.3ad ae0;
        }
    }
    ge-0/0/1 {
        ether-options {
            802.3ad ae1;
        }
    }
    ge-0/0/2 {
        ether-options {
            802.3ad ae0;
        }
    }
    ge-0/0/3 {
        ether-options {
            802.3ad ae1;
        }
    }
    ae0 {
        description PRIVATE_VLANs;
        flexible-vlan-tagging;
        native-vlan-id 925;
        unit 0 {
            vlan-id 925;
            family inet {
                address 10.188.111.70/26;
            }
        }
    }
    ae1 {
        description PUBLIC_VLAN;
        flexible-vlan-tagging;
        native-vlan-id 985;
        unit 0 {
            vlan-id 985;
            family inet {
                address 169.60.101.121/28;
            }
            family inet6 {
                address 2607:f0d0:3901:0063:0000:0000:0000:000f/64;
            }
        }
    }
    fxp0 {
        unit 0;
    }
    lo0 {
        unit 0 {
            family inet {
                filter {
                    input PROTECT-IN;
                }
                address 127.0.0.1/32;
            }
        }
    }
}
firewall {
    filter PROTECT-IN {
        term PING {
            from {
                destination-address {
                    169.60.101.121/32;
                    10.188.111.70/32;
                }
                protocol icmp;
            }
            then accept;
        }
        term SSH {
            from {
                destination-address {
                    169.60.101.121/32;
                    10.188.111.70/32;
                }
                protocol tcp;
                destination-port ssh;
            }
            then accept;
        }
        term WEB {
            from {
                destination-address {
                    169.60.101.121/32;
                    10.188.111.70/32;
                }
                protocol tcp;
                port 8443;
            }
            then accept;
        }
        term DNS {
            from {
                protocol udp;
                source-port 53;
            }
            then accept;
        }
    }
}
routing-options {
    static {
        route 166.9.0.0/16 next-hop 10.188.111.65;
        route 0.0.0.0/0 next-hop 169.60.101.113;
        route 161.26.0.0/16 next-hop 10.188.111.65;
        route 10.0.0.0/8 next-hop 10.188.111.65;
    }
}
```

The following table illustrates network interface definitions for the previous configuration:

| Interface name    |  Interface function      |
| :---          |   :---         |
| ge-0/0/0      |   Gigabit ethernet interface for SL-PRIVATE transit VLAN |
| ge-0/0/1      |   Gigabit ethernet interface for SL-PUBLIC transit VLAN  |
| ge-0/0/2      |   Gigabit ethernet interface for SL-PRIVATE transit VLAN |
| ge-0/0/3      |   Gigabit ethernet interface for SL-PUBLIC transit VLAN |
| ae0.0         |   Aggregated Ethernet interface |
| ae1.0         |   Aggregated Ethernet interface |
| fxp0          |   Management interface        |
| lo0           |   loopback interface          |

## Default Configuration of a sample 10G HA SR-IOV Public and Private vSRX Gateway
{: #default-configuration-of-a-sample-highly-available-ha-vsrx-gateway}

```
## Last commit: 2020-04-21 17:22:34 UTC by root
version 18.4R1-S1.3;
groups {
    node0 {
        system {
            host-name asloma-tc1b-18-10g-pubpriv-dual-ha1-vsrx-vSRX-Node0;
        }
    }
    node1 {
        system {
            host-name asloma-tc1b-18-10g-pubpriv-dual-ha1-vsrx-vSRX-Node1;
        }
    }
}
apply-groups "${node}";
system {
    login {
        class security {
            permissions [ security-control view-configuration ];
        }
        user admin {
            uid 2000;
            class super-user;
            authentication {
                encrypted-password "xxx"; ## SECRET-DATA
            }
        }
    }
    root-authentication {
        encrypted-password "xxx”;## SECRET-DATA
    }
    services {
        ssh {
            root-login allow;
        }
        netconf {
            ssh {
                port 830;
            }
        }
        web-management {
            http {
                interface fxp0.0;
            }
            https {
                port 8443;
                system-generated-certificate;
                interface [ fxp0.0 reth1.0 reth0.0 ];
            }
            session {                   
                session-limit 100;
            }
        }
    }
    name-server {
        10.0.80.11;
        10.0.80.12;
    }
    syslog {
        user * {
            any emergency;
        }
        file messages {
            any any;
            authorization info;
        }
        file interactive-commands {
            interactive-commands any;
        }
    }
    ntp {
        server 10.0.77.54;
    }
}
chassis {
    cluster {
        control-link-recovery;
        reth-count 4;
        heartbeat-interval 2000;
        heartbeat-threshold 8;
        redundancy-group 0 {
            node 0 priority 100;
            node 1 priority 1;
        }
        redundancy-group 1 {
            node 0 priority 100;
            node 1 priority 1;
            inactive: preempt;
            interface-monitor {
                ge-0/0/3 weight 130;
                ge-0/0/4 weight 130;
                ge-7/0/3 weight 130;
                ge-7/0/4 weight 130;
            }
        }
    }
}
security {
    log {                               
        mode stream;
        report;
    }
    address-book {
        global {
            address SL8 10.1.192.0/20;
            address SL9 10.1.160.0/20;
            address SL4 10.2.128.0/20;
            address SL5 10.1.176.0/20;
            address SL6 10.1.64.0/19;
            address SL7 10.1.96.0/19;
            address SL1 10.0.64.0/19;
            address SL2 10.1.128.0/19;
            address SL3 10.0.86.0/24;
            address SL20 10.3.80.0/20;
            address SL18 10.2.176.0/20;
            address SL19 10.3.64.0/20;
            address SL16 10.2.144.0/20;
            address SL17 10.2.48.0/20;
            address SL14 10.1.208.0/20;
            address SL15 10.2.80.0/20;
            address SL12 10.2.112.0/20;
            address SL13 10.2.160.0/20;
            address SL10 10.2.32.0/20;
            address SL11 10.2.64.0/20;
            address SL_PRIV_MGMT 10.87.40.36/32;
            address SL_PUB_MGMT 169.62.79.21/32;
            address-set SERVICE {
                address SL8;
                address SL9;
                address SL4;
                address SL5;
                address SL6;
                address SL7;
                address SL1;
                address SL2;
                address SL3;
                address SL20;
                address SL18;
                address SL19;
                address SL16;
                address SL17;
                address SL14;
                address SL15;
                address SL12;
                address SL13;
                address SL10;
                address SL11;
            }                           
        }
    }
    screen {
        ids-option untrust-screen {
            icmp {
                ping-death;
            }
            ip {
                source-route-option;
                tear-drop;
            }
            tcp {
                syn-flood {
                    alarm-threshold 1024;
                    attack-threshold 200;
                    source-threshold 1024;
                    destination-threshold 2048;
                    queue-size 2000; ## Warning: 'queue-size' is deprecated
                    timeout 20;
                }
                land;
            }
        }
    }
    policies {
        from-zone SL-PRIVATE to-zone SL-PRIVATE {
            policy Allow_Management {
                match {
                    source-address any;
                    destination-address [ SL_PRIV_MGMT SERVICE ];
                    application any;
                }
                then {
                    permit;
                }
            }
        }
        from-zone SL-PUBLIC to-zone SL-PUBLIC {
            policy Allow_Management {
                match {
                    source-address any;
                    destination-address SL_PUB_MGMT;
                    application [ junos-ssh junos-https junos-http junos-icmp-ping ];
                }
                then {
                    permit;
                }
            }
        }                               
    }
    zones {
        security-zone SL-PRIVATE {
            interfaces {
                reth0.0 {
                    host-inbound-traffic {
                        system-services {
                            all;
                        }
                    }
                }
            }
        }
        security-zone SL-PUBLIC {
            interfaces {
                reth1.0 {
                    host-inbound-traffic {
                        system-services {
                            all;
                        }
                    }
                }
            }
        }
    }
}
interfaces {
    ge-0/0/1 {
        gigether-options {
            redundant-parent reth0;
        }
    }
    ge-0/0/2 {
        gigether-options {
            redundant-parent reth0;
        }
    }
    ge-0/0/3 {
        gigether-options {
            redundant-parent reth1;
        }
    }
    ge-0/0/4 {
        gigether-options {
            redundant-parent reth1;
        }
    }
    ge-0/0/5 {
        gigether-options {              
            redundant-parent reth2;
        }
    }
    ge-0/0/6 {
        gigether-options {
            redundant-parent reth2;
        }
    }
    ge-0/0/7 {
        gigether-options {
            redundant-parent reth3;
        }
    }
    ge-0/0/8 {
        gigether-options {
            redundant-parent reth3;
        }
    }
    ge-7/0/1 {
        gigether-options {
            redundant-parent reth0;
        }
    }
    ge-7/0/2 {
        gigether-options {
            redundant-parent reth0;
        }
    }
    ge-7/0/3 {
        gigether-options {
            redundant-parent reth1;
        }
    }
    ge-7/0/4 {
        gigether-options {
            redundant-parent reth1;
        }
    }
    ge-7/0/5 {
        gigether-options {
            redundant-parent reth2;
        }
    }
    ge-7/0/6 {
        gigether-options {
            redundant-parent reth2;
        }
    }
    ge-7/0/7 {                          
        gigether-options {
            redundant-parent reth3;
        }
    }
    ge-7/0/8 {
        gigether-options {
            redundant-parent reth3;
        }
    }
    fab0 {
        fabric-options {
            member-interfaces {
                ge-0/0/0;
                ge-0/0/9;
            }
        }
    }
    fab1 {
        fabric-options {
            member-interfaces {
                ge-7/0/0;
                ge-7/0/9;
            }
        }
    }
    lo0 {
        unit 0 {
            family inet {
                filter {
                    input PROTECT-IN;
                }
                address 127.0.0.1/32;
            }
        }
    }
    reth0 {
        redundant-ether-options {
            redundancy-group 1;
        }
        unit 0 {
            description "SL PRIVATE VLAN INTERFACE";
            family inet {
                address 10.87.40.36/26;
            }
        }
    }
    reth1 {
        redundant-ether-options {
            redundancy-group 1;         
        }
        unit 0 {
            description "SL PUBLIC VLAN INTERFACE";
            family inet {
                address 169.62.79.21/29;
            }
            family inet6 {
                address 2607:f0d0:2901:002e:0000:0000:0000:0003/64;
            }
        }
    }
    reth2 {
        vlan-tagging;
        redundant-ether-options {
            redundancy-group 1;
        }
    }
    reth3 {
        vlan-tagging;
        redundant-ether-options {
            redundancy-group 1;
        }
    }
}
firewall {
    filter PROTECT-IN {
        term PING {
            from {
                destination-address {
                    169.62.79.21/32;
                    10.87.40.36/32;
                }
                protocol icmp;
            }
            then accept;
        }
        term SSH {
            from {
                destination-address {
                    169.62.79.21/32;
                    10.87.40.36/32;
                }
                protocol tcp;
                destination-port ssh;
            }
            then accept;
        }
        term WEB {
            from {                      
                destination-address {
                    169.62.79.21/32;
                    10.87.40.36/32;
                }
                protocol tcp;
                port 8443;
            }
            then accept;
        }
        term DNS {
            from {
                protocol udp;
                source-port 53;
            }
            then accept;
        }
    }
}
routing-options {
    static {
        route 166.9.0.0/16 next-hop 10.87.40.1;
        route 0.0.0.0/0 next-hop 169.62.79.17;
        route 161.26.0.0/16 next-hop 10.87.40.1;
        route 10.0.0.0/8 next-hop 10.87.40.1;
    }
}
```

The information in the following table represents the configuration above:

| Interface name   | Interface  function   | Redundant interface |
| :---       |    :---     |    :---     |
| ge-0/0/1 / ge-0/0/2 | Gigabit ethernet interface for SL-PRIVATE transit VLAN on node 0 | reth0 |
| ge-0/0/3 / ge-0/0/4 | Gigabit ethernet interface for SL-PUBLIC transit VLAN on node 0 | reth1 |
| ge-0/0/5 / ge-0/0/6 | Gigabit ethernet interface for SL-PRIVATE transit VLAN on node 0 | reth2 |
| ge-0/0/7 / ge-0/0/8 | Gigabit ethernet interface for SL-PUBLIC transit VLAN on node 0 | reth3 |
| ge-7/0/1 / ge-7/0/2 | Gigabit ethernet interface for SL-PRIVATE transit VLAN on node 1 | reth0 |
| ge-7/0/3 / ge-7/0/4 | Gigabit ethernet interface for SL-PUBLIC transit VLAN on node 1 | reth1 |
| ge-7/0/5 / ge-7/0/6 | Gigabit ethernet interface for SL-PRIVATE transit VLAN on node 1 | reth2 |
| ge-7/0/7 / ge-7/0/8 | Gigabit ethernet interface for SL-PUBLIC transit VLAN on node 1 | reth3 |
| fab0 | Chassis cluster fabric link uses ge-0/0/0 and ge-0/0/9 | |
| fab1 | Chassis cluster fabric link uses ge-7/0/0 and ge-7/0/9 | |
| fxp0          |   Management interface        | |
| lo0           |   loopback interface          | |

## Interface configurations
The legacy architecture for these configurations leveraged Linux bridging on the Ubuntu host hypervisor. IBM has since transitioned to a new architecture for its gateways that leverages SR-IOV on the host. This caused the vSRX configuration’s interface mapping to change in many cases. Differences in the interface configuration are also influenced by whether the vSRX is:

* 10G or 1G
* Standalone or High Availability
* Public and Private, or Private Only
* The vSRX Version
  - All 15.1 based vSRX’s use the legacy architecture
  - Some 18.4 based vSRX’s also use the legacy architectue

Both the legacy and current architecture is detailed in the following sections.

### vSRX High Availability interfaces (current architecture)

|**Interface**|**10G Pub+Priv** |**10G Priv Only** |**1G Pub+Priv** |**1G Priv Only** |
|-------------|----------------|-----------------|-----------------|----------------|
|ge-0/0/0|fab0|fab0|fab0|fab0|
|ge-0/0/1|reth0|reth0|reth0|reth0|
|ge-0/0/2|reth0|reth0|reth0|reth0|
|ge-0/0/3|reth1|reth2|reth1|reth2|
|ge-0/0/4|reth1|reth2|reth1|reth2|
|ge-0/0/5|reth2|fab0|reth2|fab0|
|ge-0/0/6|reth2|Does Not Exist|reth2|Does Not Exist|
|ge-0/0/7|reth3|Does Not Exist|reth3|Does Not Exist|
|ge-0/0/8|reth3|Does Not Exist|reth3|Does Not Exist|
|ge-0/0/9|fab0|Does Not Exist|fab0|Does Not Exist|
|ge-7/0/0|fab1|fab1|fab1|fab1|
|ge-7/0/1|reth0|reth0|reth0|reth0|
|ge-7/0/2|reth0|reth0|reth0|reth0|
|ge-7/0/3|reth1|reth2|reth1|reth2|
|ge-7/0/4|reth1|reth2|reth1|reth2|
|ge-7/0/5|reth2|fab1|reth2|fab1|
|ge-7/0/6|reth2|Does Not Exist|reth2|Does Not Exist|
|ge-7/0/7|reth3|Does Not Exist|reth3|Does Not Exist|
|ge-7/0/8|reth3|Does Not Exist|reth3|Does Not Exist|
|ge-7/0/9|fab1|Does Not Exist|fab1|Does Not Exist|

### vSRX Standalone interfaces (current architecture)

|**Interface**|**10G Pub+Priv** |**10G Priv Only** |**1G Pub+Priv** |**1G Priv Only** |
|-------------|----------------|-----------------|-----------------|----------------|
|ge-0/0/0|ae0|ae0|ae0|ae0|
|ge-0/0/1|ae1|ae0|ae1|ae0|
|ge-0/0/2|ae0|Does Not Exist|ae0|Does Not Exist|
|ge-0/0/3|ae1|Does Not Exist|ae1|Does Not Exist|

### vSRX High Availability interfaces (legacy architecture)

|**Interface**|**10G Priv+Pub** |**10G Priv Only** |**1G Priv + Pub** |**1G Priv Only** |
|-------------|----------------|-----------------|-----------------|----------------|
|ge-0/0/0|fab0|fab0|fab0|fab0|
|ge-0/0/1|reth0|reth0|reth0|reth0|
|ge-0/0/2|reth0|reth0|reth2|reth2|
|ge-0/0/3|reth1|reth2|reth1|Unused|
|ge-0/0/4|reth1|reth2|reth3|Unused|
|ge-0/0/5|reth2|Unused|Does Not Exist|Does Not Exist|
|ge-0/0/6|reth2|Unused|Does Not Exist|Does Not Exist|
|ge-0/0/7|reth3|Unused|Does Not Exist|Does Not Exist|
|ge-0/0/8|reth3|Unused|Does Not Exist|Does Not Exist|
|ge-7/0/0|fab1|fab1|fab1|fab1|
|ge-7/0/1|reth0|reth0|reth0|reth0|
|ge-7/0/2|reth0|reth0|reth2|reth2|
|ge-7/0/3|reth1|reth2|reth1|Unused|
|ge-7/0/4|reth1|reth2|reth3|Unused|
|ge-7/0/5|reth2|Unused|Does Not Exist|Does Not Exist|
|ge-7/0/6|reth2|Unused|Does Not Exist|Does Not Exist|
|ge-7/0/7|reth3|Unused|Does Not Exist|Does Not Exist|
|ge-7/0/8|reth3|Unused|Does Not Exist|Does Not Exist|

### vSRX standalone interfaces (legacy architecture)

|**Interface**|**10G Pub+Priv** |**10G Priv Only** |**1G Pub+Priv** |**1G Priv Only** |
|-------------|----------------|-----------------|-----------------|----------------|
|ge-0/0/0|ae0|ae0|ge-0/0/0|ge-0/0/0|
|ge-0/0/1|ae1|ae0|ge-0/0/1|Does Not Exist|
|ge-0/0/2|ae0|Does Not Exist|Does Not Exist|Does Not Exist|
|ge-0/0/3|ae1|Does Not Exist|Does Not Exist|Does Not Exist|
