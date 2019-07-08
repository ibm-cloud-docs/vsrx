---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: basics, performing, accessing, ssh, device, gateway, configuration, mode, juniper, ui, dns, htp, password

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

# 執行 IBM Cloud Juniper vSRX Basics
{: #performing-ibm-cloud-juniper-vsrx-basics}

可以透過 SSH 或藉由登入 Juniper Web 管理 GUI，使用遠端主控台階段作業來配置 IBM® Cloud Juniper vSRX 閘道。

在 vSRX 的 Shell 和介面外部配置 vSRX 可能會產生非預期結果，因此建議不要這樣做。
{: note}

## 使用 SSH 存取裝置
{: #accessing-the-device-using-ssh}

如果您位於 SoftLayer VPN，則可以透過公用 IP 位址或透過專用 IP 位址，使用 SSH 來存取 vSRX：

1. 移至「閘道應用裝置詳細資料」畫面，並取得「公用閘道 IP」或「專用閘道 IP」。

  <img src="images/gw-sa-details.png" alt="圖片" style="width: 700px;"/>

2. 按一下「眼睛」圖示，以顯示管理使用者的密碼。

3. 執行 `ssh admin@<gateway-ip>` 指令，然後輸入管理使用者的密碼。

如果看不到「眼睛」圖示，您可能沒有檢視密碼的許可權。請向帳戶擁有者核對您的存取權。
{: note}

## 存取配置模式
{: accessing-the-configuration-mode}

一旦 Shell 開啟至 vSRX，您就可以執行 `config` 指令，來進入配置模式。您可以在此模式中使用下列指令來執行數個作業：

* `show` - 檢視配置  
* `show | compare` - 檢視暫置的變更
* `set` - 暫置變更
* `commit check` - 驗證配置的語法

如果滿意變更，則可以先執行 `commit` 指令，再執行 `save`，向作用中配置確定它們。  

若要離開「配置」模式，請執行 `exit` 指令。

## 使用 Juniper Web 管理使用者介面存取裝置
{: #accessing-the-device-using-the-juniper-web-management-ui}

依預設，已配置 Juniper Web 管理 GUI，搭配 vSRX 產生的自簽憑證。只會在埠 8443 上啟用 https。您可以在 `https://gateway-ip` 存取它。

![閘道應用裝置 HA 詳細資料](images/vSRX-webui.png)

## 建立系統使用者
{: #creating-system-users}

依預設，會將 IBM Cloud Juniper vSRX 配置為對使用者名稱 `admin` 具有 SSH 存取權。也可以新增其他使用者，具有自己一組的優先順序。例如：

```
set system login user ops class operator authentication encrypted-password <CYPHER>
```

在此範例中，`ops` 是使用者名稱，而 `operator` 是指派給使用者的類別/許可權層次。

也可以定義自訂的類別，而不是預先定義的類別。

## 定義 vSRX 主機名稱
{: #defining-the-vsrx-hostname}

您可以使用下列指令來設定或變更 vSRX 主機名稱：

```
set system host-name <hostname>
```

## 配置 DNS 及 NTP
{: #configuring-dns-and-ntp}

若要配置名稱伺服器解析及 NTP，請執行下列指令：

```
set system name-server <DNS server>
set system ntp <NTP server>
```

## 變更 root 密碼
{: #changing-the-root-password}

您可以執行下列指令來變更 root 密碼：

```
set system root-authentication plain-text-password
```

這會提示您輸入新密碼，該密碼已加密並儲存在配置中，且不可見。
