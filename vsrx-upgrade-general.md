---

copyright:
  years: 2019
lastupdated: "2023-02-14"

keywords: reloading, os, upgrading, kvm, ha, stand-alone

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# General upgrade considerations
{: #general-upgrade}

Before you perform a vSRX upgrade, be aware of the following considerations:
{: shortdesc}

* You might experience network disruptions when upgrading your vSRX version. To avoid disruptions, perform the upgrade during a maintenance window that supports potential network downtime. Failover is not available until the upgrade completes, and can take several hours. For High Availability (HA) environments, your vSRX configuration settings are migrated; however, it is recommended to export your settings before the upgrade.

* For a stand-alone environment, the previous configuration is not restored, so you should export and import your configuration. For more information, see [Importing and exporting a vSRX configuration](/docs/vsrx?topic=vsrx-importing-exporting-vsrx-configuration).

* For a successful reload on a HA vSRX, the root password for the provisioned vSRX gateway must match the root password that is defined in the vSRX portal. In addition, you must enable root SSH login to the vSRX Private IP.

    You defined the password in the portal when you provisioned your gateway. This might not match the current gatewaypassword. If the password was changed after provisioning, then use SSH to connect to the vSRX gateway and changethe root password to match. The Readiness Check fails if there is a password mismatch.
    {: important}

* Do not modify the vSRX configuration during an OS reload. The upgrade process captures a snapshot of the current vSRX cluster configuration at the beginning of the process. Therefore, modifying the vSRX configuration during the upgrade process can result in a failure, or unpredictable results. For example, automated software agents attempting to modify one or both vSRX nodes. Configurations changes can corrupt the OS reload process. Additionally, these configuration changes are not preserved if a rollback is initiated.

* Before performing an OS reload upgrade on an HA cluster, run the command `show chassis cluster status`. The nodes should be clustered with one node that is listed as the primary and the other as secondary. Ensure that there are no `monitor failures`. If the cluster is not healthy prior to the upgrade, then the upgrade can fail, causing an extended traffic outage.

   Example of a healthy cluster:

   ```text
    root@asloma-19-10g-ha1-vsrx-vSRX-Node0> show chassis cluster status
    Monitor Failure codes:
      CS  Cold Sync monitoring        FL  Fabric Connection monitoring
      GR  GRES monitoring             HW  Hardware monitoring
      IF  Interface monitoring        IP  IP monitoring
      LB  Loopback monitoring         MB  Mbuf monitoring
      NH  Nexthop monitoring          NP  NPC monitoring              
      SP  SPU monitoring              SM  Schedule monitoring
      CF  Config Sync monitoring      RE  Relinquish monitoring
      IS  IRQ storm

    Cluster ID: 2
    Node   Priority Status               Preempt Manual   Monitor-failures

    Redundancy group: 0 , Failover count: 1
    node0  100      primary              no      no       None           
    node1  1        secondary            no      no       None           

    Redundancy group: 1 , Failover count: 1
    node0  100      primary              no      no       None           
    node1  1        secondary            no      no       None           

    {primary:node0}
   ```
   {: screen}

   Example of an unhealthy cluster with monitor failures:
   
   ```text
     root@asloma-tc11-15-10g-pubpriv-ha1-vsrx-vSRX-Node1> show chassis cluster status
     Monitor Failure codes:
       CS  Cold Sync monitoring        FL  Fabric Connection monitoring
       GR  GRES monitoring             HW  Hardware monitoring
       IF  Interface monitoring        IP  IP monitoring
       LB  Loopback monitoring         MB  Mbuf monitoring
       NH  Nexthop monitoring          NP  NPC monitoring              
       SP  SPU monitoring              SM  Schedule monitoring
       CF  Config Sync monitoring
     Cluster ID: 3
     Node   Priority Status         Preempt Manual   Monitor-failures
   
     Redundancy group: 0 , Failover count: 1
     node0  0        lost           n/a     n/a      n/a            
     node1  1        primary        no      no       None           
   
     Redundancy group: 1 , Failover count: 1
     node0  0        lost           n/a     n/a      n/a            
     node1  0        primary        no      no       CS             
   
     {primary:node1}
   ```
   {: screen}

* If your IBM Cloud account has multiple vSRX gateway instances in the same pod, make sure that only one gateway is upgraded at a time. Upgrading more than one vSRX at a time can result in IP collisions, disrupt the upgrade process, and potentially cause failures.

* If you configure your HA cluster to use Intrusion Detection Policies (IDP) and a signature database, it is strongly recommended that you update the signature database after completing the upgrade. This is because the database might be out of date. For information about online and offline database updates, see [Intrusion Detection and Prevention on IBM Cloud](https://public.dhe.ibm.com/cloud/bluemix/network/vsrx/idp.pdf){: external}

* The upgrade process will not backup or restore any vSRX certificates local to the Virtual Machine (VM) being upgraded. The upgrade process will delete the existing VM and create a new one, which will replace the JunOS file system. For example, a local certificate like `IKE_POLICY_CERT` must be backed up prior to the upgrade and manually restored after it completes.

```
set security ike policy MY_VPN_IKE_POLICY certificate local-certificate IKE_POLICY_CERT
```
{: pre}
