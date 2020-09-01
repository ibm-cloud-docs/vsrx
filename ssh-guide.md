---

copyright:
  years: 2018
lastupdated: "2019-11-14"

keywords: vsrx, ssh, allowing, pinging, subnet, public

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank_"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}
{:important: .important}
{:tip: .tip}

# Allowing SSH and pinging to a public subnet
{: #allowing-ssh-and-pinging-to-a-public-subnet}

In this guide, learn how to configure the {{site.data.keyword.vsrx_full}} Standard with a new interface, zone, and address-book. As the default action for all traffic is to drop, this guide shows how to set up traffic flows that allow all traffic within the new zone, all traffic from the new zone to the internet, and allow only SSH and ping from the internet to one subnet on the new VLAN.
{: shortdesc}

In this example, the following values are used.

```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

This step-by-step assumes that a high-availability deployment of the vSRX, with a single Public VLAN and subnet.
{: note}

## What you'll accomplish
{: #what-you-ll-accomplish}

In this step-by-step guide learn how to configure the service:

Task  | Description
------------- | -------------
[Create a new interface, zone, and address-book subnet](/docs/vsrx?topic=vsrx-creating-the-new-interface-zone-and-address-book-subnet) | Create the tagged interface unit and security zone for the new VLAN.
[Creating your new traffic flows](/docs/vsrx?topic=vsrx-creating-your-new-traffic-flows) | Create the new traffic flows to allow inbound pinging and SSH.
[Confirm the output and commit the changes](/docs/vsrx?topic=vsrx-confirming-the-output-and-commiting-the-changes) | Check the output to confirm what will be committed to the active configuration.
