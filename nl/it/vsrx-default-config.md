---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Descrizione della configurazione predefinita vSRX
I dispositivi gateway Juniper vSRX in IBM Cloud vengono forniti con la seguente configurazione predefinita:

* SSH e Ping sono consentiti su entrambi gli indirizzi IP gateway privato e pubblico vSRX
* L'accesso all'IU di gestione web Juniper (J-Web) è consentito sulla porta HTTPS 8443 per entrambi gli indirizzi IP gateway privato e pubblico
* Viene predefinito un set di indirizzi `SERVICE` per le reti del servizio SoftLayer
* Vengono predefinite due zone di sicurezza: `SL-PRIVATE` e `SL-PUBLIC`.
* L'accesso dalla zona `SL-PRIVATE` a tutti i servizi viene fornito da SoftLayer ed è consentito il set di indirizzi `SERVICE` 
* Tutti gli altri accessi alla rete vengono negati

## Configurazione predefinita di un gateway vSRX autonomo di esempio

```
system {
    host-name cicd-gw2-vSRX;
    root-authentication {
        encrypted-password "xxxxxxxxxxxxxxxxxxxxxxzx"; ## SECRET-DATA
    }
    name-server {
        10.0.80.11;
        10.0.80.12;
    }
    login {
        class security {
            permissions [ security-control view-configuration ];
        }
        user admin {
            uid 2000;
            class super-user;
            authentication {
                encrypted-password "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"; ## SECRET-DATA
            }
        }
    }
    services {
        ssh;
        netconf {
            ssh {
                port 830;
            }
        }
        web-management {
            https {
                port 8443;
                system-generated-certificate;
                interface [ fxp0.0 ge-0/0/0.0 ge-0/0/1.0 ];
            }
            session {
                session-limit 100;
            }
        }
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
            address SL_PRIV_MGMT 10.188.111.89/32;
            address SL_PUB_MGMT 169.60.86.234/32;
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
                    queue-size 2000;
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
                ge-0/0/0.0 {
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
                ge-0/0/1.0 {
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
        description PRIVATE_VLANs;
        flexible-vlan-tagging;
        native-vlan-id 925;
        unit 0 {
            vlan-id 925;
            family inet {
                address 10.188.111.89/26;
            }
        }
    }
    ge-0/0/1 {
        description PUBLIC_VLAN;
        flexible-vlan-tagging;
        native-vlan-id 985;
        unit 0 {
            vlan-id 985;
            family inet {
                address 169.60.86.234/29;
            }
            family inet6 {
                address 2607:f0d0:3901:0063:0000:0000:0000:0005/64;
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
routing-options {
    static {
        route 0.0.0.0/0 next-hop 169.60.86.233;
        route 161.26.0.0/16 next-hop 10.188.111.65;
        route 10.0.0.0/8 next-hop 10.188.111.65;
    }
}
firewall {
    filter PROTECT-IN {
        term PING {
            from {
                destination-address {
                    169.60.86.234/32;
                    10.188.111.89/32;
                }
                protocol icmp;
            }
            then accept;
        }
        term SSH {
            from {
                destination-address {
                    169.60.86.234/32;
                    10.188.111.89/32;
                }
                protocol tcp;
                destination-port ssh;
            }
            then accept;
        }
        term WEB {
            from {
                destination-address {
                    169.60.86.234/32;
                    10.188.111.89/32;
                }
                protocol tcp;
                port 8443;
            }
            then accept;
        }
    }
}
```

La seguente tabella illustra le definizioni dell'interfaccia di rete per la configurazione precedente:

| Nome interfaccia    |  Funzione interfaccia      |
| :---          |   :---         |
| ge-0/0/0      |   Interfaccia Gbe (GigaBit ethernet) per la VLAN di transito SL-PRIVATE |
| ge-0/0/1      |   Interfaccia Gbe (GigaBit ethernet) per la VLAN di transito SL-PUBLIC |
| fxp0          |   Interfaccia di gestione        |
| lo0           |   interfaccia loopback          |


## Configurazione predefinita di un gateway vSRX ad elevata disponibilità (HA) di esempio
```
groups {
    node0 {
        system {
            host-name cicd-gw1-vSRX-Node0;
        }
    }
    node1 {
        system {
            host-name cicd-gw1-vSRX-Node1;
        }
    }
}
apply-groups "${node}";
system {
    root-authentication {
        encrypted-password "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"; ## SECRET-DATA
    }
    name-server {
        10.0.80.11;
        10.0.80.12;
    }
    login {
        class security {
            permissions [ security-control view-configuration ];
        }
        user admin {
            uid 2000;
            class super-user;
            authentication {
                encrypted-password "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"; ## SECRET-DATA
            }
        }
    }
    services {
        ssh;
        netconf {
            ssh {
                port 830;
            }
        }
        web-management {
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
        reth-count 4;
        redundancy-group 0 {
            node 0 priority 100;
            node 1 priority 1;
        }
        redundancy-group 1 {
            node 0 priority 100;
            node 1 priority 1;
            preempt;
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
            address SL_PRIV_MGMT 10.137.165.55/32;
            address SL_PUB_MGMT 159.8.201.115/32;
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
                    queue-size 2000;
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
            redundant-parent reth2;
        }
    }
    ge-0/0/3 {
        gigether-options {
            redundant-parent reth1;
        }
    }
    ge-0/0/4 {
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
            redundant-parent reth2;
        }
    }
    ge-7/0/3 {
        gigether-options {
            redundant-parent reth1;
        }
    }
    ge-7/0/4 {
        gigether-options {
            redundant-parent reth3;
        }
    }
    fab0 {
        fabric-options {
            member-interfaces {
                ge-0/0/0;
            }
        }
    }
    fab1 {
        fabric-options {
            member-interfaces {
                ge-7/0/0;
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
    reth0 {
        redundant-ether-options {
            redundancy-group 1;
        }
        unit 0 {
            description "SL PRIVATE VLAN INTERFACE";
            family inet {
                address 10.137.165.55/26;
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
                address 159.8.201.115/28;
            }
            family inet6 {
                address 2a03:8180:1401:72::6/64;
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
routing-options {
    static {
        route 0.0.0.0/0 next-hop 159.8.201.113;
        route 161.26.0.0/16 next-hop 10.137.165.1;
        route 10.0.0.0/8 next-hop 10.137.165.1;
    }
}
firewall {
    filter PROTECT-IN {
        term PING {
            from {
                destination-address {
                    159.8.201.115/32;
                    10.137.165.55/32;
                }
                protocol icmp;
            }
            then accept;
        }
        term SSH {
            from {
                destination-address {
                    159.8.201.115/32;
                    10.137.165.55/32;
                }
                protocol tcp;
                destination-port ssh;
            }
            then accept;
        }
        term WEB {
            from {
                destination-address {
                    159.8.201.115/32;
                    10.137.165.55/32;
                }
                protocol tcp;
                port 8443;
            }
            then accept;
        }
    }
}

```

La seguente tabella illustra le definizioni dell'interfaccia di rete per la configurazione precedente:

| Nome interfaccia    |  Funzione interfaccia      |
| :---          |    :---         |
| ge-0/0/1 / ge-0/0/2   |  Interfaccia Gbe (GigaBit ethernet) per la VLAN privata sul nodo primario |
| ge-0/0/3 / ge-0/0/4   |  Interfaccia Gbe (GigaBit ethernet) per la VLAN pubblica sul nodo primario |
| ge-7/0/1 / ge-7/0/2  |  Interfaccia Gbe (GigaBit ethernet) per la VLAN privata sul nodo secondario |
| ge-7/0/3 / ge-7/0/4  |  Interfaccia Gbe (GigaBit ethernet) per la VLAN pubblica sul nodo secondario |
| reth0         |   Interfaccia ethernet ridondante per la VLAN di transito SL-PRIVATE |
| reth1         |   Interfaccia ethernet ridondante per la VLAN di transito SL-PUBLIC |
| reth2         |   Interfaccia ethernet ridondante per le VLAN private CUSTOMER  |
| reth3         |   Interfaccia ethernet ridondante per le VLAN pubbliche CUSTOMER  |
| fab0 / fab1   |   Link fabric cluster chassis |
| fxp0          |   Interfaccia di gestione        |
| lo0           |   interfaccia loopback          |

Inoltre, vengono configurati due gruppi di ridondanza. La seguente tabella illustra questi gruppi di ridondanza:

| Gruppo di ridondanza   |  Funzione gruppo di ridondanza      |
| :---          |    :---         |
| redundancy-group 0   |  Gruppo di ridondanza per il piano di controllo |
| redundancy-group 1   |  Gruppo di ridondanza per il piano di dati |

La priorità nel gruppo di ridondanza decide quale nodo vSRX è attivo. Per impostazione predefinita, il nodo 0 è attivo sia per il piano di controllo che di dati.
