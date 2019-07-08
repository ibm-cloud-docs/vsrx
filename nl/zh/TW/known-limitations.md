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

{{site.data.keyword.cloud}}IBM® Cloud Juniper vSRX 的現行限制：

* Juniper vSRX Gateway 是使用 Linux Bridge 搭配網路虛擬化進行部署。Linux Bridge 型網路虛擬化只能達到有限的傳輸量且永達不到線路速率傳輸量。

* 不支援從「獨立式」升級至「高可用性」模式。

* 使用 Junos OS `15.1` 版或 `18.4` 版的選項來部署 IBM Cloud Juniper vSRX 閘道。目前，不支援升級/降級為其他版本。

* 即使系統上有其他（有效）授權，60 天評估授權也可能導致核心產生錯誤訊息。因此，您應該移除任何 60 天評估授權以避免此問題。若要這樣做，請執行下列程序：

1. 登入到 vSRX 閘道裝置。

2. 在主控台提示中執行 `cli` 指令，以進入 CLI 模式。

3. 執行以下指令來取得授權 ID：

```
show system license
```
其輸出應該類似於下列內容：

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

4. 複製要刪除的授權的 ID，並執行以下指令：

```
request system license delete <license identifier>
```
