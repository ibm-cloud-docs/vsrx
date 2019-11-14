---

copyright:
  years: 2018
lastupdated: "2019-11-13"

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

# Known Limitations for IBM Cloud Juniper vSRX
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

There are some limitations to be aware of when using {{site.data.keyword.vsrx_full}}.
{: shortdesc}

* Juniper vSRX Gateway is deployed with networking virtualization using Linux Bridge. Linux Bridge based networking virtualization can only achieve limited throughput and never line-rate throughput.

* There is no support to upgrade from Standalone to High-availability mode.

* {{site.data.keyword.vsrx_full}} Gateway is deployed with the options of Junos OS version `15.1` or `18.4`. Currently, there is no support for upgrading/downgrading to a different version.

* The 60-day evaluation license may cause the kernel to generate ERROR messages, even when there is another (valid) license on the system. You should remove any 60-day evaluation licenses to avoid this issue. To do so, perform the following procedure:

  1. Login to your vSRX gateway device.

  2. Enter CLI mode by running the command `cli` at the console prompt.

  3. Run the command to get the license identifier:

  ```
  show system license
  ```

  The output should be similar to the following:

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

  Copy the identifier of the license that you want to delete and run the command:

  ```
  request system license delete <license identifier>
  ```
