---

copyright:
  years: 2018
lastupdated: "2020-02-21"

keywords: limitations, problems

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

# Known limitations for IBM Cloud Juniper vSRX
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

There are some limitations to be aware of when using {{site.data.keyword.vsrx_full}}.
{: shortdesc}

* Due to incompatible networking elements, the Juniper vSRX solution is not available as follows:

      - Neither 1 Gbps or 10 Gbps versions in the SEA01 (Seattle, WA) data center
      - 10 Gbps version in WDC01 (Washington, DC)
      - 1G and 10G High Availability versions in: AMS01, DAL05, DAL06, DAL07, HKG02, HOU02, SJC01, SNG01, and WDC01

* Juniper vSRX gateway is deployed with networking virtualization by using Linux Bridge. Linux Bridge based networking virtualization can achieve only limited throughput and never line-rate throughput.

* There is no support to upgrade from Standalone to High-availability mode.

* {{site.data.keyword.vsrx_full}} Gateway is deployed with the options of Junos OS version `15.1` or `18.4`. Currently, upgrading/downgrading to a different version is not supported.

* The 60-day evaluation license might cause the kernel to generate error messages, even when another (valid) license is on the system. Remove any 60-day evaluation licenses to avoid this issue. To do so, follow these steps:

   1. Log in to your vSRX gateway device.

   2. Enter CLI mode by running the command `cli` at the console prompt.

   3. Run the command to get the license identifier:

      ```
      show system license
      ```

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

   4. Copy the identifier of the license that you want to delete and run the command:

      ```
      request system license delete <license identifier>
      ```
