---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords:

subcollection: vsrx, firewalls, working, policy, policies, rules, zones, standalone, ha

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

# Working with Firewalls
{: #working-with-firewalls}

The IBM® Cloud Juniper vSRX uses the concept of security zones, where each vSRX interface is mapped to a "zone" for handling stateful firewalls. Stateless firewalls are controlled by firewall filters.

Policies are used to allow and block traffic between these defined zones, and the rules defined here are stateful.

In the IBM Cloud, a vSRX is designed to have four different security zones:

| Zone                     | Standalone Interface | HA Interface |
| :---                     |        :----:        |         ---: |
| SL-Private (untagged)    | ge-0/0/0.0           | reth0.0      |
| SL-Public (untagged)     | ge-0/0/1.0           | reth1.0      |
| Customer-Private (tagged)| ge-0/0/0.1           | reth2.1      |
| Customer-Public (tagged) | ge-0/0/1.1           | reth3.1      |

## Zone Policies
{: #zone-policies}

To configure a stateful firewall, perform the following procedure:

1. Create security zones and assign the respective interfaces:

	Standalone scenario:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces ge-0/0/1.1
	```
	High Availability scenario:
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces reth2.1
	```
2. Define the policy and rules between two different zones.

	The following example illustrates pinging traffic from the zone `Customer-Private` to `Customer-Public`:

	```
	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP match source-address any destination-address any application junos-icmp

	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP then permit
	```

These are some of the attributes that can be defined in your policies:

* Source addresses
* Destination addresses
* Applications
* Action (permit/deny/reject/count/log)

Since this is a stateful operation, there is no need to allow return packets (in this case, the echo replies).

Use the following commands to allow traffic that is directed to the vSRX:

Standalone Case:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.0 host-inbound-traffic system-services all
```
HA Case:
```
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.0 host-inbound-traffic system-services all
```

To allow protocols, such as OSPF or BGP, use the following command:

Standalone Case:
```
set security zones security-zone trust interfaces ge-0/0/0.0 host-inbound-traffic protocols all
```
HA Case:
```
set security zones security-zone trust interfaces reth2.0 host-inbound-traffic protocols all
```

## Firewall Filters
{: #firewall-filters}

By default the IBM Cloud Juniper vSRX allows ping, SSH, and HTTPS to itself and drops all other traffic by applying the `PROTECT-IN` filter to the `lo` interface.

To configure a new stateless firewall, perform the following procedure:

1. Create the firewall filter and term (the following filter will allow only ICMP and drop all other traffic)
	```
	set firewall filter ALLOW-PING term ICMP from protocol icmp
	set firewall filter ALLOW-PING term ICMP then accept
	```

2. Apply the filter rule to the interface (the following command will apply the filter to all private network traffic)
	```
	set interfaces ge-0/0/0 unit 0 family inet filter input ALLOW-PING
	```
