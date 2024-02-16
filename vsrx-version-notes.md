---

copyright:
  years: 2017, 2021
lastupdated: "2023-10-05"

keywords: version, base version, release notes, juniper

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# IBM Cloud Juniper vSRX supported versions
{: #vsrx-versions}

This document lists the currently supported vSRX versions.
{: shortdesc}

You can click the **Version information** link for each entry to get more details about that version.

| Base version | Release version | Architecture model | Hypervisor | Release date | Version information |
| --- | --- | --- | --- | --- | --- |
| 23.2R1-S1 | 23.2R1-S1.6 | 3.0 | Ubuntu 20.04 with KVM | 10 October 2023 | [More information](https://supportportal.juniper.net/s/article/23-2R1-S1-SRN?language=en_US){: external} |
| 22.2R2-S2 | 22.2R2-S2.3 | 3.0 | Ubuntu 20.04 with KVM | 2 May 2 2023 | [More information](https://supportportal.juniper.net/s/article/22-2R2-S2-SRN?language=en_US){: external} |
| 21.4R3 | 21.4R3.15 | 3.0 | Ubuntu 20.04 with KVM | 2 November 2022 | [More information](https://www.juniper.net/documentation/us/en/software/junos/release-notes/21.4/junos-release-notes-21.4r3/topics/concept/vsrx-release-notes.html){: external} |
| 21.3R2-S1 | 21.3R2-S1.2 | 3.0 | Ubuntu 18.04 with KVM | 28 July 2022 | [More information](https://supportportal.juniper.net/s/article/21-3R2-S1-Software-Release-Notification-for-JUNOS-Software-Version-21-3R2-S1?language=en_US){: external} |
| 20.4R2-S2 | 20.4R2-S2.2 | 2.0 | Ubuntu 18.04 with KVM | 21 September 2021 | [More information](https://supportportal.juniper.net/s/article/20-4R2-S2-Software-Release-Notification-for-JUNOS-Software-Version-20-4R2-S2?language=en_US){: external} |
| 19.4R3-S2 | 19.4R3-S2.2 | 2.0 | Ubuntu 18.04 with KVM | 25 March 2021 | [More information](https://supportportal.juniper.net/s/article/19-4R3-S2-Software-Release-Notification-for-JUNOS-Software-Version-19-4R3-S2?language=en_US){: external} |
| 19.4R2-S3 | 19.4R2-S3.1 | 2.0 | Ubuntu 18.04 with KVM | 8 December 2020 | [More information](https://supportportal.juniper.net/s/article/19-4R2-S3-Software-Release-Notification-for-JUNOS-Software-Version-19-4R2-S3?language=en_US){: external} |
| 19.4 | 19.4R2-S1 | 2.0 | Ubuntu 18.04 with KVM | 21 September 2020 | [More information](https://supportportal.juniper.net/s/article/19-4R2-S1-Software-Release-Notification-for-JUNOS-Software-Version-19-4R2-S1?language=en_US){: external} |
| 18.4 | 18.4R1-S1 | 2.0 | Ubuntu 18.04 with KVM | 8 April 2019 | [More information](https://supportportal.juniper.net/s/article/18-4R1-S1-Software-Release-Notification-for-Junos-Software-Service-Release-version-18-4R1-S1?language=en_US){: external} |
| 15.1 | 15.1X49 | 2.0 | Ubuntu 16.04 with KVM | 25 October 2018 | [More information](https://www.juniper.net/documentation/product/us/en/junos-os/){: external} |
{: caption="Table 1. IBM Cloud Juniper vSRX supported versions" caption-side="bottom"}

It's critical that you review the [Junos OS dates and milestones](https://support.juniper.net/support/eol/software/junos/){: external} to determine whether Juniper still supports your Junos version. If your installed version is approaching its end of support from Juniper, then [Upgrade your vSRX](/docs/vsrx?topic=vsrx-upgrading-the-vsrx) immediately to maintain full support.
{: important}

All versions before 19.4R3-S2 are prone to clustering issues and crashing. As a result, it is critical that you upgrade to the latest available version, especially if you are using 19.4R2-S3 or below.
{: important}
