---

copyright:
  years: 2017, 2025
lastupdated: "2025-04-04"

keywords:

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Known limitations for {{site.data.keyword.cloud_notm}} Juniper vSRX
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

There are some limitations to be aware of when using {{site.data.keyword.vsrx_full}}.
{: shortdesc}

* Only IBM Cloud certified versions of vSRX are supported. The list of supported versions can be found [here](/docs/vsrx?topic=vsrx-vsrx-versions).

* Upgrading from Stand-alone to High Availability mode is not supported.

* Downgrading from High Availability to Stand-alone mode is not supported.

* Upgrading from 1G to 10G or downgrading from 10G to 1G is not supported.

* Migrating the primary public or private IP addresses on the vSRX VM to another vSRX VM or other gateway appliance is not supported.

   This is a common request when upgrading to different hardware. When configuring IPSec VPN tunnels, you will often use the primary public IP of the vSRX as the IKE gateway local-address. However, it is recommended that you first [order a public static subnet or IP](/docs/subnets?topic=subnets-order-subnets&interface=ui) and route it to the primary public IP of the vSRX. You should then use that IP address as the IKE gateway local address. If migrating the IPSec VPN tunnels becomes necessary in the future, it is then possible to keep that IP address as well as route it to a new or different gateway appliance.

   While migrating the primary IP of a vSRX or gateway appliance to a different one is not supported, [migrating a secondary static subnet](/docs/subnets?topic=subnets-re-routing-secondary-subnets&interface=ui) within the same datacenter is.
   {: tip}

* Remote VPN licenses are only supported on versions 22.2 and later.

* Only the latest IBM Cloud certified vSRX release is available for new orders and upgrades. Requests for older IBM Cloud certified vSRX releases should be made through an IBM Support case. Limitations for upgrading and downgrading can be found in [Upgrading the vSRX](/docs/vsrx?topic=vsrx-upgrading-the-vsrx).

* Older Juniper vSRX gateways were deployed with Linux Bridge based networking virtualization. This virtualization can achieve only limited throughput and never line-rate throughput. Most deployments of vSRX 18.4 and later use SR-IOV, which provides improved throughput.

* The speed shown for a single GE interface within the vSRX will generally show 1G for the single interfaces even when ordered as 10G. This is cosmetic and does not reflect the actual speed capability on 10Gbps vSRX appliances. You should perform speed checks on the Ubuntu host rather than on the vSRX VM. In addition, running speed tests with tools like Iperf3 can also help verify traffic throughput. Another way to verify is through the bandwidth graphs associated to the primary node vSRX. This shows the maximum and minimum throughput reached using the samples taken for the graphs.

* Older Juniper vSRX gateways were deployed with a 60-day evaluation license, which might cause the kernel to generate error messages even when another (valid) license is on the system. Remove any 60-day evaluation licenses to avoid this issue. To do so, follow these steps:

   1. Log in to your vSRX gateway device.

   2. Enter CLI mode by running the command `cli` at the console prompt.

   3. Run the following command to get the license identifier:

      ```sh
      show system license
      ```

      The output is similar to the following:

      ```text
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

      ```sh
      request system license delete <license identifier>
      ```

   ```text
    > show system license
  License usage:s
                                 Licensed     Licensed    Licensed
                                  Feature      Feature     Feature
  Feature name                       used    installed      needed    Expiry
  Virtual Appliance                     1            1           0    2025-10-01 00:00:00 UTC
  remote-access-ipsec-vpn-client        0            2           0    permanent
  remote-access-juniper-std             0            2           0    permanent
  VCPU Scale                            6            6           0    2025-10-01 00:00:00 UTC
   ```

The `remote-access-ipsec-vpn-client` and `remote-access-juniper-std` are two different access licenses. Your license comes with two client connections at no extra cost. If you need more users to connect at the same time, you can purchase more Juniper Connect licenses. This increases the count for `remote-access-juniper-std`, which is the license count for Juniper connect. The other license `remote-access-ipsec-vpn-client` is for third-party IPsec VPN clients, and any connections that are made by those clients count against this license.
{:note: .note}
