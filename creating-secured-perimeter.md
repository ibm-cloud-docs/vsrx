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

# Creating a Secured Perimeter
A fundamental aspect of network isolation is the establishment of a secured perimeter.  A secure perimeter controls traffic between the public internet to the customer assets hosted in the IBM Cloud.  The secured perimeter will also enable direct connectivity with the customer enterprise by the use of Virtual Private Network (VPN) tunnels and IBM Cloud Direct Link.

A secured perimeter uses a Secure Perimeter Segment (SPS) to segregate networks between assets inside the secure perimeter. This segregation has several benefits, including access control and service traffic isolation between segments. A Secure Perimeter Segment (SPS) comprises two Virtual Local Area Networks (VLANs), a front-end VLAN and a back-end VLAN, and a VRA connected to the VLANs to manage the traffic into and out of the SPS. A secure perimeter can include multiple Secure Perimeter Segments (for example, for high-availability purposes).

## Setting up the secured perimeter

Following are the steps for setting up a secured perimeter.  For a detailed description of these steps see [Set up a Secure Perimeter in the IBM Cloud] (https://developer.ibm.com/dwblog/2018/ibm-cloud-vyatta-set-up-secure-perimeter)
1) Configure permissions in the IBM Cloud and infrastructure required to access the cloud services and infrastructure components involved in the secure perimeter.
1) Create an outer boundary in the public internet trough a public VLAN and a firewall. This outer boundary will be used to isolate the SPS.
2) Place the SPS inside that boundary
3) Setup a gateway to bridge the public VLAN and SPS
4) Create a configure Virtual Router Appliance (VRA)
5) Create and configure one or more Secured Perimeter Segments (SPS)
6) Create front-end VLAN
7) Create back-end VLAN
8) Create Vyatta pair
9) Configure Vyatta
10) Associate VLANS with a gateway
11) Configure gateway interface for Public VLAN
12) Configure gateway on Vyatta master
13) Configure gateway on Vyatta backup
14) Configure gateway interface for private VLAN
15) Configure gateway on Vyatta master
16) Configure gateway on Vyatta backup
17) Enable network Tuning
18) Set up firewall rules
19) Configure Kubernetes cluster
20) Configure user-provided IP's (optional).
21) Deploy Kubernetes cluster.

## Dedicated solutions in the IBM Cloud
A secured perimeter, along with compute isolation and data encryption, contributes to a complete dedicated solution in the public IBM Cloud.  See [Implementing a Dedicated Solution Pattern] (https://developer.ibm.com/dwblog/2018/ibm-cloud-dedicated-cloud-solution-patterns/) for a description of cloud dedicated solution patterns.
