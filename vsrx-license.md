---

copyright:
  years: 2018, 2020
lastupdated: "2024-06-10"

keywords: license, viewing, changing

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Viewing and changing vSRX licenses
{: #vsrx-licenses}

The vSRX has both required and optional licenses. A required license must be included when ordering a vSRX, while optional licenses are not necessary to be included. Both required and optional license settings can be changed.   

The vSRX has two available required licenses (you must select one or the other when ordering:

* Standard
* Content Security Bundle (CSB)

The only optional license for the vSRX is "Remote access VPN". 

For more information on these licenses, refer to [Choosing a vSRX license](/docs/vsrx?topic=vsrx-getting-started#choosing-license).
{: tip}

To view your current licenses, follow these steps:

1. From your browser, open the [IBM Cloud console](/login){: external} and log in to your account.
1. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Classic Infrastructure**.
1. Choose **Network > Gateway Appliances**.
1. Click the Gateway Appliance Name to access the Gateway Appliance Details page.

To change a current license, complete the previous steps, then:

1. Run a [readiness check](/docs/vsrx?topic=vsrx-vsrx-readiness) for “License update/renew” and address any errors that are found.
1. Click **Update License** for the license you want to change. 

   If you cannot access the button, then the readiness check is incomplete.
   {: tip}
   
1. For required licenses, select the type of license you want. For optional licenses, select the number of licenses you want to install. In both cases, pricing information displays next to the selection.
1. Click **Submit** to initiate your change request. 

The removal of optional licenses occurs at the end of the month.
{: note}
