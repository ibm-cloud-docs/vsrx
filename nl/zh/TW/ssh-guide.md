---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# 容許對公用子網路進行 SSH 及 ping
{: #allowing-ssh-and-pinging-to-a-public-subnet}

在本手冊中，您將瞭解如何使用新的介面、區域及通訊錄，來配置 IBM® Cloud Juniper vSRX Standard。因為要捨棄所有資料流量的預設動作，本手冊將顯示如何設定資料傳輸流，以容許新區域內的所有資料流量、從新區域到網際網路的所有資料流量，以及僅容許從網際網路至新 VLAN 上某個子網路的 SSH 和 ping。

在此範例中，使用下列值。
```
Public vlan: 1523
Public subnet: 169.47.211.152/29
```

**附註：**此「逐步」假設使用單一「公用 VLAN」及子網路，進行 vSRX 的高可用性部署。

## 您將達成的目標

在此「逐步」手冊中，您將瞭解如何部署服務：

作業  | 說明
------------- | -------------
[建立新的介面、區域及通訊錄子網路](/docs/infrastructure/vsrx?topic=vsrx-creating-the-new-interface-zone-and-address-book-subnet) | 為新的 VLAN 建立標記的介面單元和安全區域。
[建立新的資料傳輸流](/docs/infrastructure/vsrx?topic=vsrx-creating-your-new-traffic-flows) | 建立新的資料傳輸流，以容許入埠 ping 及 SSH。
[確認輸出及確定變更](/docs/infrastructure/vsrx?topic=vsrx-confirming-the-output-and-commiting-the-changes) | 檢查輸出，以確認要向作用中配置確定的內容。
