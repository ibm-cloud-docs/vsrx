---

copyright:
  years: 2018
lastupdated: "2021-08-02"

keywords:  

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# Known limitations for {{site.data.keyword.cloud_notm}} Juniper vSRX
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

There are some limitations to be aware of when using {{site.data.keyword.vsrx_full}}.
{: shortdesc}

* Due to incompatible networking elements, the Juniper vSRX solution is not available as follows:

   - 10 Gbps version in WDC01
   - 1G and 10G High Availability versions in: DAL05, HOU02, SJC01, and WDC01
   - 10G High Availability versions in: AMS01, DAL06, HKG02 Pod 1

* Only IBM Cloud certified versions of vSRX are supported. The list of supported versions can be found [here](/docs/vsrx?topic=vsrx-vsrx-versions).

* There is no support to upgrade from Standalone to High Availability mode.

* There is no support to downgrade from High Availability to Standalone mode.

* There is no support to upgrade from 1G to 10G or downgrade from 10G to 1G.

* Only the latest IBM Cloud certified vSRX release is available for new orders and upgrades. Requests for older IBM Cloud certified vSRX releases should be made through an IBM Support ticket. Limitations for upgrading and downgrading can be found in [Upgrading the vSRX](/docs/vsrx?topic=vsrx-upgrading-the-vsrx).

* Older Juniper vSRX gateways were deployed with Linux Bridge based networking virtualization. This virtualization can achieve only limited throughput and never line-rate throughput. Most deployments of vSRX 18.4 and later leverage SR-IOV, which provides improved throughput.

* Older Juniper vSRX gateways were deployed with a 60-day evaluation license, which might cause the kernel to generate error messages even when another (valid) license is on the system. Remove any 60-day evaluation licenses to avoid this issue. To do so, follow these steps:

   1. Log in to your vSRX gateway device.

   2. Enter CLI mode by running the command `cli` at the console prompt.

   3. Run the following command to get the license identifier:

      ```
      show system license
      ```
      {: pre}

      Output is similar to the following:

      ```
      License usage:
                                     Licenses     Licenses    Licenses    Expiry
      Feature name                       used    installed      needed
      logical-system                        0            3           0    permanent
      Virtual Appliance                     1            1           0    2021-10-18 00:00:00 UTC
      remote-access-ipsec-vpn-client        0            2           0    permanent

      Licenses installed:
      License identifier: E2018101804
      License version: 4
      Software Serial Number: SUB00024128768
      Customer ID: IBM_SL_10G
      Features:
        Virtual Appliance - Virtual Appliance
          date-based, 2018-10-18 00:00:00 UTC - 2021-10-18 00:00:00 UTC
      ```
      {: screen}

   4. Copy the identifier of the license that you want to delete, then run the command:

      ```
      request system license delete <license identifier>
      ```
      {: pre}
