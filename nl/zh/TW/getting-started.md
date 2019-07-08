---

copyright:
  years: 2018
lastupdated: "2019-05-03"

keywords: vsrx, ordering, gateway, appliance

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}

# 開始使用 IBM Cloud Juniper vSRX Gateway
{: #getting-started}

若要開始使用 IBM® Cloud Juniper vSRX Gateway，請先判定您的帳戶是否鏈結至 IBM Cloud。

若要瞭解您是否有已鏈結帳戶，請在瀏覽器中導覽至[客戶入口網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){: new_window} 並登入。如果您的帳戶已鏈結，那麼不會在右上角看到**進一步瞭解 Bluemix 的相關資訊！**按鈕。

## 訂購步驟
{: #steps-for-ordering}

您可以使用下列其中一種方法來訂購「閘道應用裝置」：

如需 IBM Cloud Juniper vSRX Gateway 的「已知限制」清單，請參閱[已知限制主題](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx)。
{: note}

### 使用已鏈結帳戶訂購
{: #ordering-with-a-linked-account}

如果您的帳戶已鏈結，請遵循下列程序：

1. 從您的瀏覽器開啟 [Cloud 型錄 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/gen1/infrastructure/provision/gateway){: new_window}中的閘道應用裝置頁面，並登入到您的帳戶。

  您還可以通過登入到 [IBM Cloud 使用者介面主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com)，並選取**標準基礎架構 > 網路 > 閘道應用裝置**來訪問此頁面。
或者，從 [IBM Cloud 型錄 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/catalog) 中，選取**網路**種類，然後選取**閘道應用裝置**磚。

2. 在**閘道供應商**下，選擇 **Juniper vSRX（最多 1 Gbps）**或 **Juniper vSRX（最多 10 Gbps）**。

3. 從**閘道應用裝置**區段中，輸入**主機名稱**和**網域名稱**資訊。這些欄位已移入預設資訊，因此請確定這些值是否正確。

	<img src="images/linked_order.png" alt="圖片" style="width: 700px;"/>

4. 根據需要勾選**高可用性**選項，然後選取所需的資料中心**位置**，並且從下拉功能表選取所需的特定 **pod**。

  此功能表中只會顯示已具有相關聯 VLAN 的 Pod。如果想要在未列出的 Pod 中佈建閘道應用裝置，請先在該 Pod 中建立 VLAN。
  {: note}

	<img src="images/linked_server.png" alt="圖片" style="width: 600px;"/>

4. 從**配置**區段中，通過選取 RAM 和 SSH 金鑰（如果要使用 SSH 金鑰來鑑別對新閘道的存取權）來選取處理器。

  根據您在步驟 2 中選取的授權版本，系統會選取適當的處理器。不過，您可以選擇其他 RAM 配置。
  {: note}

5. 從**儲存空間磁碟**區段中，選擇符合儲存空間需求的選項。

  RAID0 和 RAID1 選項可用於提升資料遺失的保護能力，還增強了緊急備用（主要元件發生故障時，可以立即投入服務的備份元件）的功能。
  {: note}

  每個 vSRX 最多可以有四個磁碟。使用 RAID 配置的「磁碟大小」是可用磁碟大小，因為 RAID 配置是鏡像的。
  {: note}

  如果計劃執行產生詳細日誌的網路診斷程式，請保留大於預設的磁碟空間設定。
  {: tip}

6. 從**網路介面**區段中，選取**上行鏈路埠速度**。預設選擇是單一介面，但還有冗餘和僅專用選項。請選擇最適合您需求的選項。

  「網路介面」的**額外組件**區段容許您根據需要選取 IPv6 位址，並顯示任何其他包含的預設選項。

8. 檢閱選擇，勾選您已閱讀協力廠商服務合約，然後按一下**建立**。這將自動驗證訂單。

訂單被已核准後，IBM Cloud Juniper vSRX 閘道的佈建會自動啟動。佈建程序完成後，新的 vSRX 會顯示在「閘道應用裝置」清單頁面中。按一下閘道名稱可開啟「閘道詳細資料」頁面。您將會找到裝置的 IP 位址、登入使用者名稱及密碼。  

請注意，一旦您從 IBM Cloud 型錄訂購和配置閘道後，還必須使用相同設定來配置裝置本身。
{: tip}

### 使用已解除鏈結的帳戶訂購
{: #ordering-with-a-unlinked-account}

如果您的帳戶已解除鏈結，請遵循下列程序：

1.	開啟[客戶入口網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){: new_window}，並登入您的帳戶。
2.	在「客戶入口網站」導覽中，選取**網路 > 閘道應用裝置**。
3.	從**閘道應用裝置**清單中，按一下**訂購閘道**。
4.	從**訂購**頁面的下拉功能表中，選取您所需的資料中心，然後選擇所需類型的伺服器硬體，將在其中佈建 Juniper vSRX。

	如果您計劃使用「雙重處理器多核心伺服器」，則必須選取 **Intel Xeon 5120** 作為伺服器類型。
  {: note}

5.	在**訂購**頁面上，需要時，請選取**高可用性配對**選項，然後選取**記憶體**大小。
6. 	接下來，按一下**作業系統**下的 **Juniper** 標籤，選取單一處理器伺服器的 **Juniper vSRX（最多 1 Gbps）Standard**，或選取雙重處理器伺服器的 **Juniper vSRX（最多 10 Gbps）Standard**。
7. 	最後，選取所需的網路上行鏈路速度。
8.	檢閱您的選項，然後按一下**新增至訂單**。即會自動驗證您的訂單。
9.	在**結帳**頁面上，如果您在選取的資料中心已擁有 VLAN，請選取您要保護的後端 VLAN。請務必：
	* 提供伺服器的主機名稱和網域名稱。
	* 根據需要，選取用於存取鑑別的 SSH 金鑰。
	* 勾選 IBM Cloud 服務條款和「第三方軟體條款」的所有方框。
10. 按一下**提交訂單**。

## 下一步為何？
{: #what-s-next-}

在核准訂單之後，即會自動開始 vSRX 的佈建。當佈建程序完成時，閘道將出現在**閘道應用裝置**清單中。

按一下閘道名稱，以開啟**閘道詳細資料**頁面。您會找到裝置的 IP 位址、登入使用者名稱及密碼。

<img src="images/after_order.png" alt="圖片" style="width: 700px;"/>
