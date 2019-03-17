---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords:

subcollection: vsrx, ssh, allowing, pinging, subnet, public

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Allowing SSH and Pinging to a Public Subnet
{: #allowing-ssh-and-pinging-to-a-public-subnet}

In this guide you will learn how to configure the IBM® Cloud Juniper vSRX Standard with a new interface, zone, and address-book. As the default action for all traffic is to drop, this guide will show how to set up traffic flows that allow all traffic within the new zone, all traffic from the new zone to the internet, and allow only ssh and ping from the internet to one subnet on the new VLAN.

In this example, the following values are used.
```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

**NOTE:** This Step-by-Step assumes that a high-availability deployment of the vSRX, with a single Public VLAN and subnet.

## What you'll accomplish

In this Step-by-Step guide you will learn how to configure the service:

Task  | Description
------------- | -------------
[Create a new interface, zone, and address-book subnet](/docs/infrastructure/vsrx?topic=vsrx-creating-the-new-interface-zone-and-address-book-subnet) | Create the tagged interface unit and security zone for the new VLAN.
[Creating your new traffic flows](/docs/infrastructure/vsrx?topic=vsrx-creating-your-new-traffic-flows) | Create the new traffic flows to allow inbound pinging and SSH.
[Confirm the output and commit the changes](/docs/infrastructure/vsrx?topic=vsrx-confirming-the-output-and-commiting-the-changes) | Check the output to confirm what will be committed to the active configuration.
