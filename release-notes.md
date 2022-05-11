---

copyright:
  years: 2017, 2022
lastupdated: "2022-05-05"

keywords: updates, changes, additions

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for IBM Cloud Juniper vSRX
{: #vsrx-release-notes}

Find out about new and updated features in {{site.data.keyword.vsrx_full}}.
{: shortdesc}

## 21 May 2021
{: #vsrx-may2121}
{: release-note}

Renewing a vSRX license
:    The vSRX standard and CSB licenses for both 1G and 10G that were included with deployments before mid-May 2021 have an expiration date in 2021. After this license expires, updates for some new vSRX features might not take effect. A newer license with an expiration date in 2024 is now available, and you can renew your gateway license to obtain it. If you are using a High Availability vSRX, renewing your license automatically modifies the license on both vSRX nodes. You can find the current expiration date on the gateway appliance details page. 

: For more information, refer to [Renewing a vSRX license](/docs/vsrx?topic=vsrx-license-renewal).

## 20 April 2020
{: #vsrx-apr2020}
{: release-note}

Checking vSRX readiness
:    You can now run readiness checks to verify the ability of your {{site.data.keyword.vsrx_full}} to perform certain gateway actions. They include:
    * OS reloads
    * License upgrades
    * Version upgrades

:    After you run a readiness check, errors alert you to any necessary actions that you should take before beginning one of these actions, or inform you that you're ready to proceed.

: For more information, refer to [Checking vSRX readiness](/docs/vsrx?topic=vsrx-vsrx-readiness#vsrx-readiness).
