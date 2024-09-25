---

copyright:
  years: 2017, 2024
lastupdated: "2024-09-24"

keywords:

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Renewing a vSRX license
{: #license-renewal}

The vSRX standard and CSB licenses for both 1G and 10G that were included with deployments before mid-May 2021 have an expiration date in 2021. After this license expires, updates for some new vSRX features might not take effect. A newer license with an expiration date in 2025 is now available, and you can renew your gateway license to obtain it. If you are using a High Availability vSRX, renewing your license automatically modifies the license on both vSRX nodes. You can find the current expiration date on the gateway appliance details page. Refer to the following instructions on viewing your license expiration date for more information.

To update to the latest license, your vSRX must be version 21.3 or later. To update the license, you must update the vSRX version using the [OS reload](/docs/vsrx?topic=vsrx-reloading-the-os) process. The license will be automatically renewed during the version upgrade.
{: important}

When using OS Reload to upgrade the OS version, the license is also upgraded. If you are, instead, using the action to reload the same OS version as before, the license is not updated.
{: tip}

## Viewing your license expiration date
{: #license-view-steps}

To find your current license expiration date, follow these steps:

1. Open the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/infrastructure){: external} and log in to your account.
2. Select the Menu icon ![Menu icon](../icons/icon_hamburger.svg) from the upper left, then click **Classic Infrastructure**.
3. Choose **Network > Gateway Appliances**.
4. Click the gateway appliance name to access the gateway appliance details page. You can find the license expiration date in the Details section.

To view your current license expiration from the vSRX CLI, run `show system license`. You should see the 2024 expiration date for each of the license features on each node.
{: tip}

## Renewing your license
{: #license-renew-steps}

To renew your license, first run a [Readiness check](/docs/vsrx?topic=vsrx-vsrx-readiness) for “License update/renew”. After you address any errors that are found, follow these steps:

1. Open the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/infrastructure){: external} and log in to your account.
1. Select the Menu icon ![Menu icon](../icons/icon_hamburger.svg) from the upper left, then click **Classic Infrastructure**.
1. Choose **Network > Gateway Appliances**.
1. Click the gateway appliance name to access the gateway appliance details page.
1. Click **Renew license**.

The license renewal can take up to 30 minutes to complete. To verify that the process completed successfully, follow the preceding steps in [Viewing your license expiration date](#license-view-steps). Verify that the expiration shows a 2025 expiration. The renewal process will not reboot the host(s) or node(s) and there should be no outages and minimal traffic disruptions as a result of this action.

After the renewal completes, future actions, such as OS Reload and License Update, automatically apply the new license.
