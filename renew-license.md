---

copyright:
  years: 2021
lastupdated: "2021-07-12"

keywords:

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Renewing a vSRX license
{: #license-renewal}

The vSRX standard and CSB licenses for both 1G and 10G that were included with deployments before mid-May 2021 have an expiration date in 2021. After this license expires, updates for some new vSRX features might not take effect. A newer license with an expiration date in 2024 is now available, and you can renew your gateway license to obtain it. If you are using a High Availability vSRX, renewing your license automatically modifies the license on both vSRX nodes. You can find the current expiration date on the gateway appliance details page. See the view license steps below.

Actions such as OS Reload will re-apply the license currently applied to the node(s). It will not update the license.  

For vSRX instances running with version 15.1 the license renewal is not available. Follow the steps [here](/docs/vsrx?topic=vsrx-upgrading-the-vsrx) to upgrade to a newer vSRX version.
{: important}

## Viewing your license expiration date
{: #license-view-steps}

To find your current license expiration date, follow these steps:

1. Open the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/vpc-ext){: external} and log in to your account.
2. Select the Menu icon ![Menu icon](../icons/icon_hamburger.svg) from the upper left, then click **Classic Infrastructure**.
3. Choose **Network > Gateway Appliances**.
4. Click the gateway appliance name to access the gateway appliance details page. You can find the license expiration date in the Details section.

To view your current license expiration from the vSRX CLI, run `show system license`. You should see the 2024 expiration date for each of the license features on each node.
{: tip}

## Renewing your license
{: #license-renew-steps}

To renew your license, first run a [Readiness check](/docs/vsrx?topic=vsrx-vsrx-readiness) for “License update/renew”. After you address any errors that are found, follow these steps:

1. Open the [{{site.data.keyword.cloud_notm}} console](https://{DomainName}/vpc-ext){: external} and log in to your account.
1. Select the Menu icon ![Menu icon](../icons/icon_hamburger.svg) from the upper left, then click **Classic Infrastructure**.
1. Choose **Network > Gateway Appliances**.
1. Click the gateway appliance name to access the gateway appliance details page.
1. Click **Renew license**.

![Renew license](images/license-renew.png "License renew"){: caption="Renew license" caption-side="bottom"}

The license renewal can take up to 30 minutes to complete. To verify that the process completed successfully, follow the preceding steps in [Viewing your license expiration date](#license-view-steps). Verify that the expiration shows a 2024 expiration. The renewal process will not reboot the host(s) or node(s) and there should be no outages and minimal traffic disruptions as a result of this action.

After the renewal completes, future actions, such as OS Reload and License Update, automatically apply the new license.
