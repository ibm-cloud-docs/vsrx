---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: understanding, default, configuration, standalone, ha

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

# Visión general de la configuración predeterminada de vSRX
{: #understanding-the-vsrx-default-configuration}

Los dispositivos de pasarela Juniper vSRX en IBM Cloud vienen con la siguiente configuración predeterminada:

* SSH y Ping están permitidos en las direcciones IP de pasarela pública y privada de vSRX
* El acceso de la interfaz de usuario de Juniper Web Management (J-Web) está permitido en el puerto HTTPS 8443 para direcciones IP de pasarela pública y privada
* Hay un address-set `SERVICE` predefinido para las redes de servicio de SoftLayer
* Hay dos zonas de seguridad, `SL-PRIVATE` y `SL-PUBLIC`, predefinidas.
* El acceso desde la zona `SL-PRIVATE` a todos los servicios se proporciona mediante SoftLayer y se permite address-set `SERVICE`
* Todos los demás acceso a la red se deniegan

## Configuración predeterminada de una pasarela vSRX autónoma de ejemplo de la última SR-IOV
{: #default-configuration-of-a-sample-standalone-vsrx-gateway}

Los siguientes ejemplos de código son ejemplos del último release de código.
{: note}

```
## Last changed: 2019-04-04 19:29:45 UTC
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
                encrypted-password "xxxxxxxxxxxxxxxxxxxxxxzx"; ## SECRET-DATA
            }
        }
    }
    root-authentication {
        encrypted-password "xxxxxxxxxxxxxxxxxxxxxxzx"; ## SECRET-DATA
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
    host-name cicd-gw1-vSRX;
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
    license {
        autoupdate {
            url https://ae1.juniper.net/junos/key_retrieval;
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
            address SL_PRIV_MGMT 10.184.108.150/32;
            address SL_PUB_MGMT 169.48.2.5/32;
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
        from-zone trust to-zone trust {
            policy default-permit {
                match {
                    source-address any;
           destination-address any;
           application any;
       }
       then {
                    permit;
                }
            }
        }
        from-zone trust to-zone untrust {
            policy default-permit {
                match {
                    source-address any;
           destination-address any;
           application any;
       }
       then {
                    permit;
                }
            }
        }
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
        security-zone trust {
            tcp-rst;
        }
        security-zone untrust {
            screen untrust-screen;
        }
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
    native-vlan-id 1121;
    unit 0 {
            vlan-id 1121;
        family inet {
                address 10.184.108.150/26;
            }
        }
    }
    ae1 {
        description PUBLIC_VLAN;
        flexible-vlan-tagging;
        native-vlan-id 1294;
        unit 0 {
            vlan-id 1294;
            family inet {
                address 169.48.2.5/27;
            }
            family inet6 {
                address 2607:f0d0:1f01:d7::c/64;
            }
        }
    }
    fxp0 {
        unit 0 {
            family inet {
                address 192.168.68.150/24;
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
}
firewall {
    filter PROTECT-IN {
        term PING {
            from {
                destination-address {
                    169.48.2.5/32;
                    10.184.108.150/32;
                    192.168.68.0/24;
                }
                protocol icmp;
            }
            then accept;
        }
        term SSH {
            from {
                destination-address {
                    169.48.2.5/32;
                    10.184.108.150/32;
                    192.168.68.0/24;
                }
                protocol tcp;
                destination-port [ ssh 830 ];
            }
            then accept;
        }
        term WEB {
            from {
                destination-address {
                    169.48.2.5/32;
                    10.184.108.150/32;
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
        route 166.9.0.0/16 next-hop 10.184.108.129;
        route 0.0.0.0/0 next-hop 169.48.2.97;
        route 161.26.0.0/16 next-hop 10.184.108.129;
        route 10.0.0.0/8 next-hop 10.184.108.129;
    }
}
```

En la tabla siguiente se muestran las definiciones de interfaz de red para la configuración anterior:

| Nombre de interfaz    |  Función de la interfaz      |
| :---          |   :---         |
| ge-0/0/0      |   Interfaz Gigabit ethernet para VLAN de tránsito SL-PRIVATE |
| ge-0/0/1      |   Interfaz Gigabit ethernet para VLAN de tránsito SL-PUBLIC  |
| ae0.0         |   Interfaz Ethernet agregada|
| ae1.0         |   Interfaz Ethernet agregada|
| fxp0          |   Interfaz de gestión        |
| lo0           |   Interfaz bucle retorno          |

## Configuración predeterminada de una pasarela de alta disponibilidad (HA) vSRX de ejemplo
{: #default-configuration-of-a-sample-highly-available-ha-vsrx-gateway}

```
## Last changed: 2019-04-04 20:03:36 UTC
version 18.4R1-S1.3;
groups {
    node0 {
        system {
            host-name cicd-gw2-vSRX-Node0;
        }
        interfaces {
            fxp0 {
                unit 0 {
                    family inet {
                        address 192.168.59.150/24;
                    }
                }
            }
        }
    }
    node1 {
        system {
            host-name cicd-gw2-vSRX-Node1;
        }
        interfaces {
            fxp0 {
                unit 0 {
                    family inet {
                        address 192.168.59.151/24;
                    }
                }
            }
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
                encrypted-password "xxxxxxxxxxxxxxxxxxxxxxzx"; ## SECRET-DATA
            }
        }
    }
    root-authentication {
        encrypted-password "xxxxxxxxxxxxxxxxxxxxxxzx"; ## SECRET-DATA
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
    license {
        autoupdate {
            url https://ae1.juniper.net/junos/key_retrieval;
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
        redundancy-group 0 {
            node 0 priority 100;
            node 1 priority 1;
        }
        redundancy-group 1 {
            node 0 priority 100;
            node 1 priority 1;
            preempt;
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
            address SL_PRIV_MGMT 10.127.152.144/32;
            address SL_PUB_MGMT 159.8.12.5/32;
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
        from-zone trust to-zone trust {
            policy default-permit {
                match {
                    source-address any;
           destination-address any;
           application any;
       }
       then {
                    permit;
                }
            }
        }
        from-zone trust to-zone untrust {
            policy default-permit {
                match {
                    source-address any;
           destination-address any;
           application any;
       }
       then {
                    permit;
                }
            }
        }
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
        security-zone trust {
            tcp-rst;
        }
        security-zone untrust {
            screen untrust-screen;
        }
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
                address 10.127.152.144/26;
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
                address 159.8.12.5/29;
            }
            family inet6 {
                address 2a03:8180:1301:101::4/64;
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
                    159.8.12.5/32;
                    10.127.152.144/32;
                    192.168.59.0/24;
                }
                protocol icmp;
            }
            then accept;
        }
        term SSH {
            from {
                destination-address {
                    159.8.12.5/32;
                    10.127.152.144/32;
                    192.168.59.0/24;
                }
                protocol tcp;
                destination-port [ ssh 830 ];
            }
            then accept;
        }
        term WEB {
            from {
                destination-address {
                    159.8.12.5/32;
                    10.127.152.144/32;
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
        route 166.9.0.0/16 next-hop 10.127.152.129;
        route 0.0.0.0/0 next-hop 159.8.12.73;
        route 161.26.0.0/16 next-hop 10.127.152.129;
        route 10.0.0.0/8 next-hop 10.127.152.129;
    }
}
```

En la tabla siguiente se muestran las definiciones de interfaz de red para la configuración anterior:

| Nombre de interfaz   |  Función de la interfaz      |
| :---          |    :---         |
| ge-0/0/1 / ge-0/0/2   |  Interfaz Gigabit ethernet para VLAN privada en nodo primario |
| ge-0/0/3 / ge-0/0/4   |  Interfaz Gigabit ethernet para VLAN pública en nodo primario |
| ge-7/0/1 / ge-7/0/2  |  Interfaz Gigabit ethernet para VLAN privada en nodo secundario |
| ge-7/0/3 / ge-7/0/4  |  Interfaz Gigabit ethernet para VLAN pública en nodo secundario |
| reth0         |   Interfaz ethernet redundante para VLAN de tránsito SL-PRIVATE |
| reth1         |   Interfaz ethernet redundante para VLAN de tránsito SL-PUBLIC  |
| reth2         |   Interfaz ethernet redundante para VLAN privadas de CLIENTE  |
| reth3         |   Interfaz ethernet redundante para VLAN públicas de CLIENTE   |
| fab0 / fab1   |   Enlace de entramado de clúster de chasis |
| fxp0          |   Interfaz de gestión        |
| lo0           |   Interfaz bucle retorno          |

Además, se configuran dos grupos de redundancia. En la tabla siguiente se muestran estos grupos de redundancia:

| Grupo redundancia   |  Función de grupo de redundancia      |
| :---          |    :---         |
| redundancy-group 0   |  Grupo redundancia para plano control |
| redundancy-group 1   |  Grupo redundancia para plano datos |

La prioridad del grupo de redundancia decide qué nodo vSRX está activo. De forma predeterminada, el nodo 0 está activo tanto para el plano de control como para el plano de datos.
