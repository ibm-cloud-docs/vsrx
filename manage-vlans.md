---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: manage, managing, vlan, gateway, route, bypass, disassociate, associate, configuration, disassociating, associating, standalone, ha

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# Managing IBM VLANs
{: #managing-ibm-vlans}

You can perform a variety of actions from the [Gateway Appliance Details screen](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details).

## Associate a VLAN to a Gateway Appliance

A VLAN needs to be associated to a Gateway Appliance before it can be routed. VLAN association is the linking of an eligible VLAN to a Network Gateway so that it can be routed to a Gateway Appliance. This association does not automatically route the VLAN to a Gateway Appliance; the VLAN continues to use front-end and back-end customer routers until it is routed.

VLANs may be associated to only one Gateway at a time and must not have a firewall. Perform the following procedure to associate a VLAN to a Network Gateway.

1. [Access the Gateway Appliance Details screen](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) in the Customer Portal.
2. Select the VLANs tab.
3. Click **Associate VLAN** and select a VLAN from the dropdown.
4. Click **Save** and confirm your selection. The VLAN association action does not route the VLAN through the firewall.

After associating a VLAN to the Gateway Appliance, it appears in the Associated VLANs section of the Gateway Appliance Details screen. From this section, the VLAN may be routed to the Gateway or may be disassociated from the Gateway. Additional eligible VLANs may be associated to a Gateway Appliance at any time by repeating the steps above.

## Route an associated VLAN

Associated VLANs are linked to a Gateway Appliance, but traffic in and out of the VLAN does not hit the Gateway until the VLAN has been routed. After an associated VLAN has been routed, all front and back-end traffic is routed through the Gateway Appliance, as opposed to customer routers.

Perform the following procedure to route an associated VLAN:

1. [Access the Gateway Appliance Details screen](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) in the Customer Portal.
2. Select the VLANs tab.
3. Select the desired VLAN(s) by toggling the checkbox.
4. Click **Route Through** and confirm your selection.

After routing a VLAN, all front-end and back-end traffic moves from the customer routers to the Network Gateway. Additional controls related to traffic and the Gateway Appliance itself may be taken by accessing the Gateway's management tool. Routing through the Network Gateway may be discontinued at any time by [bypassing the Gateway Appliance](#bypass-gateway-appliance-routing-for-a-vlan).

## Bypass Gateway Appliance routing for a VLAN

After a VLAN has been routed, all front and back-end traffic travels through the Network Gateway. At any time, the Gateway Appliance may be bypassed so that traffic will return to the front and back-end customer routers (FCR and BCR).

Bypassing a VLAN allows the VLAN to remain associated to the Network Gateway. If the VLAN should no longer be associated with the Gateway Appliance, refer to [Disassociate a VLAN from a Gateway Appliance](#disassociate-a-vlan-from-a-gateway-appliance).

Perform the following procedure to bypass Gateway routing for a VLAN:

1. [Access the Gateway Appliance Details screen](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) in the Customer Portal.
2. Select the VLANs tab.
3. Select the desired VLAN(s) by toggling the checkbox.
4. Click **Route Around** and confirm your selection.

After bypassing the Network Gateway, all front-end and back-end traffic routes through the FCR and BCR associated with the VLAN. The VLAN will remain associated with the Gateway Appliance and may be routed back to the Gateway Appliance at any time.

## Disassociate a VLAN from a Gateway Appliance

VLANs may be linked to one Gateway Appliance at a time through [association](#associate-a-vlan-to-a-gateway-appliance). Association allows the VLAN to be routed to the Gateway Appliance at any time. If a VLAN should be associated to another Gateway Appliance, or if the VLAN should no longer be associated to its Gateway, disassociation is required. Disassociation removes the "link" from the VLAN to the Gateway Appliance, allowing it to be associated to another Gateway, if necessary.

Perform the following procedure to disassociate a VLAN from a Gateway Appliance:

1. [Access the Gateway Appliance Details screen](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details) in the Customer Portal.
2. Select the VLANs tab.
3. Select the desired VLAN(s) by toggling the checkbox.
4. Click **Disassociate** and confirm your selection.

After disassociating a VLAN from a Gateway Appliance, the VLAN may be associated to another Gateway. The VLAN may also be associated back to the Gateway Appliance at any time. After disassociating a VLAN from a Gateway Appliance, the VLAN's traffic cannot be routed through the Gateway. VLANs must be associated to a Gateway Appliance before they can be routed.

## Route Multiple VLANs over the same network interface
The IBM® Cloud Juniper vSRX can operate with multiple VLANs over the same network interface. It can also handle both untagged and tagged traffic at the same time. This is accomplished on the standalone device by setting the interface encapsulation to `flexible-vlan-tagging`, or on the High-Availability devices by using reth2 and reth3 as tagged interfaces. This is done as part of the default configuration and does not need to be modified.  On the standalone devices, Unit 0 is the sub-interface that is untagged; other, non-zero units are tagged.

Use the following set of commands to configure additional tagged interfaces:

Standalone Case:
```
set interfaces ge-0/0/0 unit 50 vlan-id 50
set interfaces ge-0/0/0 unit 50 family inet address <IP/MASK>
```

HA Case:
```
set interfaces reth2 unit 50 vlan-id 50
set interfaces reth2 unit 50 family inet address <IP/MASK>
```

**NOTE:** Even though unit 0 is untagged, `JunOS` needs it to reference the VLAN ID that is configured as `native-vlan`. In the example, since `native-vlan-id` is `10`, unit 0 should have a `vlan-id` of `10` as well. This way, `JunOS` is informed that unit 0 should be untagged.

## Sample VLAN Configuration for vSRX

Below is a sample configuration for vSRX which defines two private interfaces and one customer zone.
With this sample configuration Private VLAN1 and Private VLAN2 can communicate with each other. Stand alone vSRX interfaces are defined as ge-0/0/0 (private) and ge-0/0/1 (public), and for High Availability instance, they are defined as reth2 (HA private) and reth3 (HA public).

<img src="images/Sample-Topology-VLAN-to-VLAN.png" alt="drawing" style="width: 500px;"/>

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
