---

copyright:
  years: 2017, 2026
lastupdated: "2026-06-11"

keywords: reloading, os, upgrading, kvm, ha, stand-alone

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# General upgrade considerations
{: #general-upgrade}

Before you perform a vSRX upgrade, be aware of the following considerations:
{: shortdesc}

* You might experience network disruptions when you upgrade your vSRX version. To avoid disruptions, perform the upgrade during a maintenance window that supports potential network downtime. Failover is not available until the upgrade completes, and can take several hours. For High Availability (HA) environments, your vSRX configuration settings are migrated; however, it is recommended to export your settings before the upgrade.

* For a stand-alone environment, the previous configuration is not restored, so you should export and import your configuration. For more information, see [Importing and exporting a vSRX configuration](/docs/vsrx?topic=vsrx-importing-exporting-vsrx-configuration).

* For a successful reload on a HA vSRX, the root password for the provisioned vSRX gateway must match the root password that is defined in the vSRX portal. In addition, you must enable root SSH login to the vSRX Private IP.

    You defined the password in the portal when you provisioned your gateway. This might not match the current gateway password. If the password was changed after provisioning, then use SSH to connect to the vSRX gateway and change the root password to match. The Readiness Check fails if there is a password mismatch.
    {: important}

* Do not modify the vSRX configuration during an OS reload. The upgrade process captures a snapshot of the current vSRX cluster configuration at the beginning of the process. Therefore, modifying the vSRX configuration during the upgrade process can result in a failure, or unpredictable results. For example, automated software agents attempting to modify one or both vSRX nodes. Configurations changes can corrupt the OS reload process. Additionally, these configuration changes are not preserved if a rollback is initiated.

* Before performing an OS reload upgrade on an HA cluster, run the command `show chassis cluster status`. The nodes should be clustered with one node that is listed as the primary and the other as the secondary. Ensure that there are no `monitor failures`. If the cluster is not healthy before the upgrade, then the upgrade can fail, causing an extended traffic outage.

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

* If you configure your HA cluster to use Intrusion Detection Policies (IDP) and a signature database, it is recommended that you update the signature database after you complete the upgrade. This is because the database might be out of date. For information about online and offline database updates, see [Intrusion Detection and Prevention on IBM Cloud](https://public.dhe.ibm.com/cloud/bluemix/network/vsrx/idp.pdf){: external}

* The upgrade process does not backup or restore any vSRX certificates local to the virtual machine (VM) being upgraded. The upgrade process deletes the existing VM and creates a new one, which replaces the JunOS file system. For example, a local certificate like `IKE_POLICY_CERT` must be backed up before the upgrade and manually restored after it completes.

```sh
set security ike policy MY_VPN_IKE_POLICY certificate local-certificate IKE_POLICY_CERT
```
{: pre}

## Ubuntu hypervisor upgrade considerations
{: #ubuntu-hypervisor-upgrade-considerations}

The vSRX runs as a VM on a Ubuntu hypervisor. Generally, this hypervisor operating system is reloaded as part of a vSRX update.  However, there are times where only the Ubuntu hypervisor requires maintenance, such as applying kernel updates, security patches, or vulnerability fixes, without upgrading the vSRX virtual machine itself.

In these cases, the standard `apt update` command is typically sufficient with some important caveats that you must be aware of. Upgrading only the Ubuntu hypervisor is generally considered a safe maintenance operation and can usually be performed with minimal disruption to running vSRX VMs. Most package updates, including standard user-space libraries and utilities, don't require interruption of guest VM operations.

However, administrators must carefully review the packages included in an upgrade before proceeding. Certain updates can affect the stability or connectivity of running virtual machines until the hypervisor is rebooted.

The following types of updates require special attention:

- Kernel packages
- `systemd` and `udev` updates
- `libvirt` packages
- Networking-related packages such as `nftables`, bridges, or other virtualization networking components
- `qemu` and `kvm` package updates

In some cases, when you upgrade virtualization or network-related packages while keeping VMs active can result in degraded VM networking, stalled interfaces, or an inconsistent `libvirt` state until the hypervisor node is restarted. A restart of the Ubuntu hypervisor typically restores normal operation.

When performing an `apt upgrade` on the hypervisor, consider the following recommendations:

- Review pending packages before applying updates.
- Schedule a maintenance window if kernel, `libvirt`, or networking components are being upgraded.
- Plan for a hypervisor reboot when required.
- Avoid performing simultaneous maintenance on multiple HA nodes when possible.

Example:

```sh
apt update
apt list --upgradable
apt upgrade
```
