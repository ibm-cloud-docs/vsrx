---

copyright:
  years: 2018
lastupdated: "2018-11-06"

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

# 收回閘道
{: #reclaiming-a-gateway}

請執行下列程序來收回閘道：

1. 在「客戶入口網站」中[存取「閘道應用裝置」畫面](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances)，並藉由選取所需的閘道名稱來導覽至「閘道詳細資料」頁面。

2. 按一下「硬體畫面」中的伺服器名稱。

	![硬體伺服器](images/os_hardware.png)

	在收回閘道之前，請先確定所有受保護的 VLAN 都已與它[取消關聯](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans)。

3. 在裝置的頁面上，按一下「動作」下拉功能表中的**取消裝置**，來存取「伺服器配置」頁面。  

4. 在「取消裝置」確認畫面上，按一下**繼續**，以開始收回處理程序。如果您不想要繼續收回，請按一下**關閉**。

若為 HA 配對，則需要在這兩個裝置上執行這些動作。
