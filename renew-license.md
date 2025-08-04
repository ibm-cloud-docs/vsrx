---

copyright:
  years: 2017, 2025
lastupdated: "2025-08-04"

keywords:

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Renewing a vSRX license
{: #license-renewal}

Know the expiration and renewal process for standard and CSB licenses on {{site.data.keyword.vsrx_full}} gateways.
{: shortdesc}

Licenses for the vSRX are obtained from the vendor in batches and IBM Cloud applies the latest license to your device when it is provisioned. If the standard license on your vSRX expires, the standard features that are listed on [Getting started with IBM Cloud Juniper vSRX](/docs/vsrx?topic=vsrx-getting-started-vsrx) continues to function. Make sure to keep your standard license up to date, especially if you use subscription-based services and features such as those that are included with the CSB license. When your standard license expires, it affects the services that are covered by the CSB license.

IBM Cloud console also shows a notification on your device's gateway page when the license expiration date approaches.

Follow the instructions provided here to learn more about viewing and renewing your license expiration date.
{: tip}

To update to the latest license, your vSRX must be version 21.3 or later. If your vSRX version is prior to 21.3, you must update the vSRX version by using the [OS reload](/docs/vsrx?topic=vsrx-reloading-the-os) process. The license is automatically renewed during the version upgrade.
{: important}

When you use OS Reload to upgrade the OS version, the license is also upgraded. However, if you use the action to reload the same OS version as before, the license is not updated.
{: note}

## Viewing your license expiration date
{: #license-view-steps}

To find your current license expiration date, follow these steps:

1. Open the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/infrastructure){: external} and log in to your account.
2. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure > Classic Infrastructure**.
3. Choose **Network > Gateway Appliances**.
4. Click the gateway appliance name to access the gateway appliance details page. You can find the license expiration date in the Details section.

To view your current license expiration from the vSRX CLI, run `show system license`. You must see the 2025 expiration date for each of the license features on each node.
{: tip}

## Renewing your license
{: #license-renew-steps}

To renew your license, first run a [Readiness check](/docs/vsrx?topic=vsrx-vsrx-readiness) for “License update/renew”. After you address any errors that are found, follow these steps:

1. Open the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/infrastructure){: external} and log in to your account.
1. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Infrastructure > Classic Infrastructure**.
1. Choose **Network > Gateway Appliances**.
1. Click the gateway appliance name to access the gateway appliance details page.
1. Click **Renew license**.

The license renewal can take up to 30 minutes to complete. To verify that the process completed successfully, follow the preceding steps in [Viewing your license expiration date](#license-view-steps). Verify that the expiration shows a 2025 expiration. The renewal process doesn't restart hosts or nodes, does not cause outages, and results in minimal traffic disruption as a result of this action.

After the renewal completes, future actions, such as OS Reload and License Update automatically applies the new license.
