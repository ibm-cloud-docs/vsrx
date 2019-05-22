---

copyright:
  years: 2018
lastupdated: "2018-11-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# 開始使用 IBM Cloud Juniper vSRX Gateway
{: #getting-started}

若要開始使用 IBM® Cloud Juniper vSRX Gateway，請先判定您的帳戶是否鏈結至 IBM Cloud。

## 開始之前

若要瞭解您是否有已鏈結帳戶，請在瀏覽器中導覽至[客戶入口網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){: new_window} 並登入。如果您的帳戶已解除鏈結，您會在右上方看到**進一步瞭解 Bluemix！**按鈕。

## 訂購步驟

您可以使用下列其中一種方法來訂購「閘道應用裝置」：

如需 IBM Cloud Juniper vSRX Gateway 的「已知限制」清單，請參閱[已知限制主題](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx)。
{:note}

### 使用已鏈結帳戶訂購
如果您的帳戶已鏈結，請遵循下列程序：

1.	開啟 [IBM Cloud 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.bluemix.net/){: new_window}，並登入您的帳戶。
2.	在左導覽中，選取**基礎架構 > 網路 > 閘道應用裝置**。
3.	從**閘道應用裝置**清單中，按一下**建立閘道**。
4. 從**訂單**頁面中，選擇**主機名稱**和**網域**。
5. 需要時，請選取**高可用性配對**選項。

	<img src="images/linked_order.png" alt="圖片" style="width: 700px;"/>

5. 接下來，選取**位置**和關聯的 **Pod**，然後選擇**伺服器**，以及所需的 **RAM** 數量。

	如果您計劃使用「雙重處理器多核心伺服器」，則必須選取 **Intel Xeon 5120** 作為伺服器類型。{:note:}

	<img src="images/linked_server.png" alt="圖片" style="width: 600px;"/>

6. 如果您想要使用 SSH 金鑰來鑑別新閘道的存取，請選取 SSH 金鑰。
7. 在**映像檔**下，選取 **Juniper vSRX 15.x（最高 1 Gbps）Standard**（若為單一處理伺服器）或 **Juniper vSRX 15.x（最高 10 Gbps）Standard**（若為雙重處理伺服器）。
8. 選取任何選用的附加程式、新增任何其他**儲存空間磁碟**，然後選擇您所需的**上行鏈路埠速度**。
8. 檢閱您在**訂購摘要**中的選項，然後閱讀並同意「協力廠商軟體條款」。
9. 最後，按一下**佈建**。

### 使用已解除鏈結的帳戶訂購
如果您的帳戶已解除鏈結，請遵循下列程序：

1.	開啟[客戶入口網站 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){: new_window}，並登入您的帳戶。
2.	在「客戶入口網站」導覽中，選取**網路 > 閘道應用裝置**。
3.	從**閘道應用裝置**清單中，按一下**訂購閘道**。
4.	從**訂購**頁面的下拉功能表中，選取您所需的資料中心，然後選擇所需類型的伺服器硬體，將在其中佈建 Juniper vSRX。

	如果您計劃使用「雙重處理器多核心伺服器」，則必須選取 **Intel Xeon 5120** 作為伺服器類型。{:note}

5.	在**訂購**頁面上，需要時，請選取**高可用性配對**選項，然後選取**記憶體**大小。
6. 	接下來，按一下**作業系統**下的 **Juniper** 標籤、選取 **Juniper vSRX 15.x（最高 1 Gbps）Standard**（若為單一處理伺服器）或 **Juniper vSRX 15.x（最高 10 Gbps）Standard**（若為雙重處理伺服器）。
7. 	最後，選取所需的網路上行鏈路速度。
8.	檢閱您的選項，然後按一下**新增至訂單**。即會自動驗證您的訂單。
9.	在**結帳**頁面上，如果您在選取的資料中心已擁有 VLAN，請選取您要保護的後端 VLAN。請務必：
	* 提供伺服器的主機名稱及網域名稱
	* 選取 SSH 金鑰進行存取鑑別（需要時）
	* 檢查 IBM  Cloud 服務條款及「協力廠商軟體條款」的所有方框
10. 按一下**提交訂單**。

## 下一步為何？
在核准訂單之後，即會自動開始 vSRX 的佈建。當佈建程序完成時，閘道將出現在**閘道應用裝置**清單中。

按一下閘道名稱，以開啟**閘道詳細資料**頁面。您會找到裝置的 IP 位址、登入使用者名稱及密碼。

<img src="images/after_order.png" alt="圖片" style="width: 700px;"/>
