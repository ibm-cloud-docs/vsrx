---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: reloading, os, upgrading, kvm, ha, standalone

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

# 重新載入作業系統
{: #reloading-the-os}

作業系統重新載入程序是用來重建閘道伺服器。此處理程序會執行下列動作：

* 重新載入伺服器主機的作業系統
* 在作業系統中安裝 KVM
* 在 KVM 中建立 vSRX VM
* 使用 IBM® Cloud 的預設配置重新配置 vSRX

此處理程序通常需要 1 小時 40 分鐘才能完成。在此期間，「獨立式閘道」將無法運作。若為「Juniper 高可用性 (HA) 閘道」，當您在其中一部伺服器上重新載入作業系統時，vSRX 將失效接手至叢集中的另一部伺服器，並繼續處理資料流量。一旦重新載入完成，伺服器就會重新加入叢集。

若要在 HA vSRX 上順利重新載入或重建叢集，請執行下列動作：

* 佈建 vSRX 閘道的 root 使用者密碼必須與 vSRX 入口網站中定義的 root 使用者密碼相符。入口網站中的密碼是在閘道佈建之初定義的，因此可能與現行的閘道密碼不符。如果在初始佈建後變更了密碼，請使用 SSH 連接至 vSRX 閘道，並變更 root 使用者密碼以進行比對。更改密碼後，可以繼續執行作業系統重新載入或重建叢集作業。

  <img src="images/gw-vsrx-password.png" alt="圖片" style="width: 700px;"/>

* **不要**在高可用性閘道的兩個伺服器上同時執行作業系統重新載入。

在 HA 閘道的兩個伺服器上同時執行作業系統重新載入將破壞 vSRX 叢集，並導致閘道無法運作。如果 vSRX 叢集已毀損，您必須使用**重建叢集**選項（詳述如下），來重新佈建 vSRX 並重建 HA 叢集。
{: important}

## 執行作業系統重新載入
{: #performing-an-os-reload}

若要重新載入閘道伺服器的作業系統，請執行下列程序：

1. 在「客戶入口網站」中[存取「閘道應用裝置」畫面](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances)，並藉由選取所需的「閘道」名稱來導覽至「閘道」詳細資料頁面。

  <img src="images/gw-sa-details.png" alt="圖片" style="width: 700px;"/>

2. 按一下「硬體畫面」中的伺服器名稱。

  ![硬體伺服器](images/os_hardware.png)

3. 在裝置的頁面上，按一下「動作」下拉功能表中的**作業系統重新載入**以存取「伺服器配置」頁面。

  ![裝置詳細資料](images/os_device_page.png)

4. 在「伺服器配置」頁面上，您可以配置並啟動重新載入。如果您是從不同的作業系統重新載入，請按一下**作業系統**旁邊的**編輯**、選取 **Juniper**，然後挑選其中一個 Juniper vSRX 15.x Standard 選項。完成修改您的設定時，請選取**重新載入上方配置**以繼續。

5. 即會顯示「作業系統重新載入」詳細資料畫面。檢閱您已選擇的設定，如果需要變更，請按一下**編輯設定**。否則，請按**下一步**繼續進行。

6. 在「作業系統重新載入」確認畫面上，同意「主要服務合約」的條款，然後藉由按一下**確認作業系統重新載入**來開始「作業系統重新載入」處理程序。如果您不想要繼續重新載入，請按一下**取消**。

## 重建 HA VSRX 叢集
{: #rebuilding-an-ha-vsrx-cluster}

若要重建其中一個 HA vSRX 叢集，請執行下列程序：

1. 在「客戶入口網站」中[存取「閘道應用裝置」畫面](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances)，並藉由選取所需的「HA 閘道」名稱來導覽至「閘道」詳細資料頁面。

2. 按一下**動作**下拉清單，並選取**重建叢集**。

3. 仔細閱讀警告訊息。重建叢集的作業具有破壞性。如果要繼續，請先儲存 vSRX 配置，然後按一下**重建**以啟動該程序。

  ![確認重建叢集](images/rebuild_cluster_confirm.png)
