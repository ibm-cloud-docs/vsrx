---

copyright:
  years: 2018
lastupdated: "2019-11-14"

keywords: manage, managing, vlan, gateway, route, bypass, disassociate, associate, configuration, disassociating, associating, standalone, ha

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# Managing IBM VLANs
{: #managing-ibm-vlans}

You can perform various actions from the [Gateway Appliance Details page](/docs/vsrx?topic=gateway-appliance-viewing-gateway-appliance-details) for your {{site.data.keyword.vsrx_full}}.
{: shortdesc}

## Associating a VLAN to a gateway appliance
{: #associate-a-vlan-to-a-gateway-appliance}

A VLAN needs to be associated to a gateway appliance before it can be routed. VLAN association is the linking of an eligible VLAN to a network gateway so that it can be routed to a gateway appliance. This association does not automatically route the VLAN to a gateway appliance; the VLAN continues to use front-end and back-end customer routers until it is routed.

VLANs can be associated to only one gateway at a time and must not have a firewall. Follow these steps to associate a VLAN to a network gateway.

1. [Access the Gateway Appliance Details page](/docs/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) in the IBM Cloud console.
2. Select the VLANs tab.
3. Click **Associate VLAN** and select a VLAN from the menu.
4. Click **Save** and confirm your selection. The VLAN association action does not route the VLAN through the firewall.

After associating a VLAN to the gateway appliance, it appears in the Associated VLANs section of the Gateway Appliance Details page. From this section, the VLAN can be routed to the gateway or can be disassociated from the gateway. Additional eligible VLANs can be associated to a gateway appliance at any time by repeating these steps.

## Routing an associated VLAN
{: #route-an-associated-vlan}

Associated VLANs are linked to a gateway appliance, but traffic in and out of the VLAN does not hit the gateway until the VLAN is routed. After an associated VLAN has been routed, all front and back-end traffic is routed through the gateway appliance, as opposed to customer routers.

Follow these steps to route an associated VLAN:

1. [Access the Gateway Appliance Details page](/docs/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) in the IBM Cloud console.
2. Select the VLANs tab.
3. Select one or more VLANs by toggling the checkbox.
4. Click **Route Through** and confirm your selection.

After routing a VLAN, all front-end and back-end traffic moves from the customer routers to the network gateway. Additional controls that are related to traffic and the gateway appliance itself can be taken by accessing the gateway's management tool. Routing through the network gateway can be discontinued at any time by [bypassing the gateway appliance](#bypass-gateway-appliance-routing-for-a-vlan).

## Bypassing gateway appliance routing for a VLAN
{: #bypass-gateway-appliance-routing-for-a-vlan}

After a VLAN has been routed, all front and back-end traffic travels through the network gateway. At any time, the gateway appliance can be bypassed so that traffic returns to the front and back-end customer routers (FCR and BCR).

Bypassing a VLAN allows the VLAN to remain associated to the network gateway. If the VLAN should not be associated with the gateway appliance, see [Disassociating a VLAN from a gateway appliance](#disassociate-a-vlan-from-a-gateway-appliance).

Follow these steps to bypass gateway routing for a VLAN:

1. [Access the Gateway Appliance Details page](/docs/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) in the IBM Cloud console.
2. Select the VLANs tab.
3. Select one or more VLANs by toggling the checkbox.
4. Click **Route Around** and confirm your selection.

After bypassing the network gateway, all front-end and back-end traffic routes through the FCR and BCR associated with the VLAN. The VLAN remains associated with the gateway appliance and can be routed back to the gateway appliance at any time.

## Disassociating a VLAN from a gateway appliance
{: #disassociate-a-vlan-from-a-gateway-appliance}

VLANs can be linked to one gateway appliance at a time through [association](#associate-a-vlan-to-a-gateway-appliance). Association allows the VLAN to be routed to the gateway appliance at any time. If a VLAN should be associated to another gateway appliance, or if the VLAN should not be associated to its gateway, disassociation is required. Disassociation removes the "link" from the VLAN to the gateway appliance, allowing it to be associated to another gateway, if necessary.

Follow these steps to disassociate a VLAN from a gateway appliance:

1. [Access the Gateway Appliance Details page](/docs/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) in the IBM Cloud console.
2. Select the VLANs tab.
3. Select one or more VLANs by toggling the checkbox.
4. Click **Disassociate** and confirm your selection.

After disassociating a VLAN from a gateway appliance, the VLAN can be associated to another Gateway. The VLAN can also be associated back to the gateway appliance at any time. After disassociating a VLAN from a gateway appliance, the VLAN's traffic cannot be routed through the Gateway. VLANs must be associated to a gateway appliance before they can be routed.

## Routing multiple VLANs over the same network interface
{: #route-multiple-vlans-over-the-same-network-interface}

The {{site.data.keyword.vsrx_full}} can operate with multiple VLANs over the same network interface. It can also handle both untagged and tagged traffic at the same time. This is accomplished on the Standalone device by setting the interface encapsulation to `flexible-vlan-tagging`, or on the High-Availability devices by using reth2 and reth3 as tagged interfaces. This is done as part of the default configuration and does not need to be modified.  On the Standalone devices, Unit 0 is the subinterface that is untagged; other, nonzero units are tagged.

Use the following set of commands to configure additional tagged interfaces:

Standalone case:
```
set interfaces ge-0/0/0 unit 50 vlan-id 50
set interfaces ge-0/0/0 unit 50 family inet address <IP/MASK>
```

HA case:
```
set interfaces reth2 unit 50 vlan-id 50
set interfaces reth2 unit 50 family inet address <IP/MASK>
```

Even though unit 0 is untagged, `JunOS` needs it to reference the VLAN ID that is configured as `native-vlan`. In the example, since `native-vlan-id` is `10`, unit 0 must a `vlan-id` of `10` as well. This way, `JunOS` is informed that unit 0 should be untagged.
{: note}

## Sample VLAN configuration for vSRX
{: #sample-vlan-configuration-for-vsrx}

The following sample configuration for vSRX defines two private interfaces and one customer zone.
With this sample configuration, Private VLAN1 and Private VLAN2 can communicate with each other. Stand alone vSRX interfaces are defined as ge-0/0/0 (private) and ge-0/0/1 (public), and for High Availability instance, they are defined as reth2 (HA private) and reth3 (HA public).

![Sample Topology](images/Sample-Topology-VLAN-to-VLAN.png "Sample Topology")

```
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


# show security zones security-zone CUSTOMER-PRIVATE
interfaces {
   ge-0/0/0.10 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
   ge-0/0/0.20 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
}
# show security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PRIVATE
policy Allow_C_C {
   match {
       source-address any;
       destination-address any;
       application any;
   }
   then {
       permit;
   }
}
```
