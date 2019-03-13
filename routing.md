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

# Working with Routing
{: #working-with-routing}

The IBM® Cloud Juniper vSRX is based on `JunOS`, giving you access to the full Juniper routing stack.

##Static Routing
To configure static routes, run the following commands:

###Setting a default route
```
set routing-options static route 0/0 next-hop <Gateway IP>
```

### Creating a static route
```
set routing-options static route <PREFIX/MASK> next-hop <Gateway IP>
```  

###Basic OSPF routing
To setup basic OSPF routing, only using area 0, run the following commands using md5 authentication:

```
set protocols ospf area 0 interface ge-0/0/1.0 authentication md5 0 key <KEY>
```

### Basic BGP routing
To setup basic BGP routing, first define the local AS:

```
set routing-options autonomous-system 65001
```

Then configure the BGP neighbor and its session attributes:

```
set protocols bgp group CUSTOMER local-address 1.1.1.1
set protocols bgp group CUSTOMER family inet unicast
set protocols bgp group CUSTOMER family inet6 unicast
set protocols bgp group CUSTOMER peer-as 65002
set protocols bgp group CUSTOMER neighbor 2.2.2.2
```

In this example, BGP is configured for the following:

* To use source IP address of `1.1.1.1` to establish the session
* To negotiate both ipv4 and ipv6 unicast families
* To peer with a neighbor that belongs to `AS 65002`
* Peer neighbor IP `2.2.2.2`

Additional configurations can be found on the [Juniper website ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.juniper.net/documentation/en_US/junos11.4/information-products/topic-collections/config-guide-routing/config-guide-routing.pdf){: new_window}.
