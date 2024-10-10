---

copyright:
  years: 2017, 2024
lastupdated: "2024-10-10"

keywords: reloading, os, upgrading, kvm, ha, standalone

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Upgrading the vSRX
{: #upgrading-the-vsrx}

There are several methods and considerations that you must understand before you upgrade your {{site.data.keyword.cloud}} Juniper vSRX:
{: shortdesc}

*	vSRX version level
*	Bare-metal server processor model
*	Bandwidth: 1G versus 10G
*	Stand-alone or High Availability (HA)

Using these factors, the following table lists whether you can use the OS reload option to upgrade your vSRX. The table also describes whether rollback is supported for the upgrade. Other considerations include whether you need a manual vSRX configuration migration to complete the upgrade.

Reference the following table to determine whether you can upgrade your vSRX by using OS reload. For more information, see [General upgrade considerations](/docs/vsrx?topic=vsrx-general-upgrade).

For more information, see [IBM Cloud Juniper vSRX supported versions](/docs/vsrx?topic=vsrx-vsrx-versions).

The upgrade reapplies the license that is currently applied to the nodes. It does not update the license. To update to a newer license, you must separately run the license renewal steps. For more information, see [Renewing a vSRX license](/docs/vsrx?topic=vsrx-license-renewal).
{: tip}

| Current vSRX version  | Processor model and speed | Stand-alone or HA | Upgrade method  | Rollback supported |
| ------------- | ------------- | ------------- | ------------- | ------------- |	 			
| 15.1	| 1270v6 (All 1G deployments)	| Stand-alone and HA	| [Not Supported](/docs/vsrx?topic=vsrx-unsupported-upgrade) | N/A|
| 15.1 | All 10G Deployments | Stand-alone and HA | [OS Reload](/docs/vsrx?topic=vsrx-os-reload-upgrade) |	**Stand-alone:** No  \n **HA:** * Manual (not automated) rollbacks are allowed after the first server completes the OS reload.  \n * Rollbacks are not allowed after the second server completes its OS reload. |
| 18.4 | 1270v6 (Some 1G Deployments) |	Stand-alone and HA |	[Not Supported](/docs/vsrx?topic=vsrx-unsupported-upgrade) |	N/A |
| 18.4 | 4210 (Some 1G Deployments) | Stand-alone | [OS Reload](/docs/vsrx?topic=vsrx-os-reload-upgrade) | No |
| 18.4 | 4210 (Some 1G Deployments) |	HA | [OS Reload](/docs/vsrx?topic=vsrx-os-reload-upgrade) | **Yes** – If you are running version 18.4 with new architecture, manual (not automated) rollbacks are allowed after the first server completes the OS reload. For more information, see [Rollback options](/docs/vsrx?topic=vsrx-rollback-options)  \n **No** – If you are running version 18.4 without the new architecture. |
| 18.4 | All 10G Deployments | Stand-alone |	[OS Reload](/docs/vsrx?topic=vsrx-os-reload-upgrade) | No |
| 18.4 | All 10G Deployments | HA |	[OS Reload](/docs/vsrx?topic=vsrx-os-reload-upgrade)	| **Yes** – If you are running version 18.4 with new architecture, manual (not automated) rollbacks are allowed after the first server completes the OS reload. For more information, see [Rollback options](/docs/vsrx?topic=vsrx-rollback-options)  \n  **No** – If you are running version 18.4 without the new architecture. |
| 19.4 and newer | All 1G and 10G Deployments | Stand-alone  \n HA | [OS Reload](/docs/vsrx?topic=vsrx-os-reload-upgrade) | **Yes** – Manual (not automated) rollbacks are allowed after the first server completes the OS reload. For more information, see [Rollback options](/docs/vsrx?topic=vsrx-rollback-options) |
{: caption="Upgrading your vSRX using OS reload" caption-side="bottom"}
