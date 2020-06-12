---

copyright:
  years: 2018
lastupdated: "2020-06-12"

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

# Migrating legacy configurations to the current vSRX architecture
{: #migrating-config}

Migrating {{site.data.keyword.vsrx_full}} configurations from the legacy to the current architecture requires careful consideration.
{: shortdesc}

vSRX 18.4 deployments leverage the current architecture in most cases. This includes the vSRX 18.4 1G SR-IOV offering. The older vSRX 18.4 1G Standard offering is based on Linux Bridging and has different network configurations on the Ubuntu host, the KVM hypervisor, and in the vSRX configuration. The host and KVM settings do not require any special migration steps, as the automation process handles the configuration changes. However, if you want to import the vSRX configuration from the legacy architecture into the current vSRX configuration, you likely need to refactor some of the configuration.

## Migrating 1G vSRX standalone configurations
{: #migrating-1g-standalone}

There are some steps you potentially need to convert vSRX configuration settings on a Standalone 18.4 1G Public+Private Linux Bridge (legacy architecture) instance to a Standalone 18.4 1G Public+Private SR-IOV (current architecture) instance.

You can find a sample default configuration for SR-IOV based current architecture [in this topic](/docs/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration#default-configuration-of-a-sample-standalone-vsrx-gateway).
{: note}

The following is a sample default configuration for the Linux Bridge (legacy architecture). The example shows vSRX instances that were provisioned in different Datacenter pods. As a result, the transit VLAN’s (`native-vlan-id`) are different.

```
## Last commit: 2020-04-16 22:48:33 UTC by root
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
                encrypted-password "$6$vKPIcB3I$XlDRg3Oto9tLa7zRPkalSfonrKUEJI7U16XX2lrke3k2sPaV.CY0CJhSBIPx5aXhqo7h1GWPhhMbv0Ce1WANO."; ## SECRET-DATA
            }
        }
    }
    root-authentication {
        encrypted-password "$6$cbXBMc8b$jHd6LtR4OjXvjmgubQXAlofNonk6lLbNPs35beda7ffEV4XKEUQiEf1XUA3mMvJv2V1YET3kiWBogqz8h2zB7."; ## SECRET-DATA
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
                interface [ fxp0.0 ge-0/0/0.0 ge-0/0/1.0 ];
            }
            session {
                session-limit 100;
            }
        }
    }
    host-name asloma-e2e-tc15-18-1g-1270-sa-vsrx-vSRX;
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
            address SL_PRIV_MGMT 10.129.33.87/32;
            address SL_PUB_MGMT 161.202.136.77/32;
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
        native-vlan-id 1214;
        unit 0 {
            vlan-id 1214;
            family inet {
                address 10.129.33.87/26;
            }
        }
    }
    ge-0/0/1 {
        description PUBLIC_VLAN;
        flexible-vlan-tagging;
        native-vlan-id 764;
        unit 0 {
            vlan-id 764;
            family inet {
                address 161.202.136.77/29;
            }
            family inet6 {
                address 2401:c900:1001:0210:0000:0000:0000:000a/64;
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
                    161.202.136.77/32;
                    10.129.33.87/32;
                }
                protocol icmp;
            }
            then accept;
        }
        term SSH {
            from {
                destination-address {
                    161.202.136.77/32;
                    10.129.33.87/32;
                }
                protocol tcp;
                destination-port ssh;
            }
            then accept;
        }
        term WEB {
            from {
                destination-address {
                    161.202.136.77/32;
                    10.129.33.87/32;
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
        route 166.9.0.0/16 next-hop 10.129.33.65;
        route 0.0.0.0/0 next-hop 161.202.136.73;
        route 161.26.0.0/16 next-hop 10.129.33.65;
        route 10.0.0.0/8 next-hop 10.129.33.65;
    }
}
```

### Converting the interface section
{: #converting-interface}

In the above 1G Public+Private Standalone example, the current architecture adds aggregated interfaces `ae0` and `ae1`. These should map to what the legacy architecture defines as `ge-0/0/0 (private / ae0)` and `ge-0/0/1 (public / ae1)`. Additionally, the new architecture adds `ge-0/0/2` and `ge-0/0/3` to support redundancy within the vSRX interfaces. In the old architecture, redundancy existed at the host (Hypervisor) bond interfaces (`bond0 private / bond1 public`). In the current architecture, SR-IOV VF’s that map directly to the `ge` interfaces are used for redundancy.

You can compare these vSRX configuration differences in [vSRX Standalone interface (current architecture)](/docs/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration#interface-configurations) and [vSRX Standalone interface (legacy architecture)](/docs/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration#vsrx-standalone-interfaces-legacy-architecture-).

Any private VLAN’s that were previously configured for `ge-0/0/0` need to be routed through `ae0`. In addition, any public VLAN’s that you previously configured for `ge-0/0/1` need to be routed through `ae1`.

### Converting the zones section
{: #converting-zones}

Any default security zones that previously referenced `ge-0/0/0` and `ge-0/0/1` should now use the `ae0.0 (SL-PRIVATE)` and `ae1.0 (SL-PUBLIC)` interfaces. The same changes also apply to any zones that previously referenced `ge-0/0/0` and `ge-0/0/1`.

### Other changes
{: #sa-other-changes}

The aggregated device configuration requires the following addition in the current architecture:

```
set chassis aggregated-devices ethernet device-count 10
```

The JWEB configuration will also include the aggregated interfaces as well:

```
set system services web-management https interface ae0.0
set system services web-management https interface ae1.0
```

## Migrating 1G vSRX High Availability configurations
{: #migrating-ha-config}

For High Availability configurations, the main vSRX changes when importing configurations from the legacy architecture to the current architecture are small changes to the interface mappings.

The 1G SR-IOV HA configuration for the current architecture adds additional vSRX interfaces for redundancy, instead of using the host (hypervisor) bond interfaces. This is possible as the host now uses SR-IOV VF’s that can be mapped directly to the vSRX interfaces. Configurations that were exported from the legacy architecture will need to take this into account if they are imported into the current architecture.

The vSRX configuration for the current architecture for 1G HA can be found [in this topic](/docs/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration#vsrx-high-availability-interfaces-current-architecture-). While, the vSRX configuration for the legacy architecture for 1G HA can be found [here](/docs/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration#vsrx-high-availability-interfaces-legacy-architecture-)

The extra `ge-0/*` and `ge-7/*` interfaces were added and associated with the existing `reth` interfaces which have been present in both the legacy and current architecture. These allow for redundancy within the vSRX configuration. Redundancy is also configured for the `fab` interfaces as well.
