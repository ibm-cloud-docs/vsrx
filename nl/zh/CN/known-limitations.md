---

copyright:
  years: 2018
lastupdated: "2018-11-06"

keywords: limitations, problems

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}

# IBM Cloud Juniper vSRX 的已知限制
{: #known-limitations-for-ibm-cloud-juniper-vsrx}

{{site.data.keyword.cloud}} IBM® Cloud Juniper vSRX 的当前限制：

* Juniper vSRX 网关使用 Linux Bridge 通过联网虚拟化进行部署。基于 Linux Bridge 的联网虚拟化只能实现有限的吞吐量，而绝不能实现线路速率吞吐量。

* 不支持从独立方式升级到高可用性方式。

* IBM Cloud Juniper vSRX 网关通过选项 Junos OS V`15.1` 或 `18.4` 进行部署。目前，不支持升级/降级为其他版本。

* 即使系统上有其他（有效）许可证，60 天评估许可证也可能导致内核生成 ERROR 消息。因此，您应该除去任何 60 天评估许可证以避免此问题。为此，请执行以下过程：

1. 登录到 vSRX 网关设备。

2. 通过在控制台提示符处运行 `cli` 命令来进入 CLI 方式。

3. 运行以下命令来获取许可证标识：

```
show system license
```
输出应类似于以下内容：

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

4. 复制要删除的许可证的标识，并运行以下命令：

```
request system license delete <license identifier>
```
