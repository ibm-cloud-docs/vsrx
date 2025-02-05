---

copyright:
  years: 2017, 2025
lastupdated: "2025-02-05"

keywords: reloading, os, upgrading, kvm, ha, standalone

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Rollback options
{: #rollback-options}

In the standalone environment a rollback is not supported.

In the high availability environment that is upgrading from vSRX version, a rollback is supported only after the first node has been OS Reloaded and before the second node has been OS Reloaded. The Gateway is in an “Upgrade Active” state at this point. The following steps should be followed to rollback the first node to the previous version.

Be aware that a traffic disruption occurs while waiting for the secondary node to power on and for the traffic to failover to this node.
{: important}

1. SSH to the bare-metal server hosting the vSRX node that is being rolled-back (the current primary node). Power off the vSRX on the node and disable autostart to avoid the VM starting up if the host reboots.

   This would cause a "split brain cluster" and most likely an outage.
   {: important}

   Use the following commands:

   ```
   virsh shutdown vSRXvM3
   virsh autostart vSRXvM3 --disable
   ```

   Wait for the node to completely power off before proceeding.

2. SSH to the bare-metal server hosting the vSRX node that was not rolled-back. Power on the vSRX. This returns the primary node back to the original vSRX version. Use the following commands:

```
# Restore the original qcow2 file.
cd /var/lib/libvirt/images/vSRXvM3
cp vSRX_Image.qcow2.backup vSRX_Image.qcow2

# Start the VM
virsh start vSRXvM3

# Enable autostart
virsh autostart vSRXvM3
```

3.	Run the [OS reload readiness check](/docs/vsrx?topic=vsrx-vsrx-readiness), if necessary, and resolve any issues.

4.	Perform an OS reload on the host that you want rollback and return to the original vSRX version. Do not run an OS Reload on the current primary node.

  	If you followed the steps above the node being rolled back should have a vSRX that is powered off and not a part of the cluster. This is the node that you should run the OS Reload on. Doing so allows both nodes in the cluster to run on the same vSRX version, which is required for a functioning vSRX cluster.
  	{: note}

Once the OS Reload completes, the cluster will run using its original configuration.
