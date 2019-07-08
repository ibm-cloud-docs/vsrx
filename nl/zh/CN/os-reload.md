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

# 重装操作系统
{: #reloading-the-os}

操作系统重装过程用于重建网关服务器。此过程执行以下操作：

* 重装服务器主机的操作系统
* 在操作系统中安装 KVM
* 在 KVM 中创建 vSRX VM
* 使用 IBM® Cloud 的缺省配置重新配置 vSRX

该过程通常需要 1 小时 40 分钟才能完成。在此期间，独立网关将停止运行。对于 Juniper 高可用性 (HA) 网关，在其中一个服务器上重装操作系统时，vSRX 会故障转移到集群中的另一个服务器，并继续处理数据流量。重装完成后，服务器将重新加入集群。

要在 HA vSRX 上成功重装或重建集群，须符合以下条件：

* 供应的 vSRX 网关的 root 用户密码必须与 vSRX 门户网站中定义的 root 用户密码相匹配。门户网站中的密码是在网关供应之初定义的，因此可能与当前的网关密码不匹配。如果在初始供应后更改了密码，请使用 SSH 连接到 vSRX 网关，并更改 root 用户密码以进行匹配。更改密码后，可以继续执行操作系统重装或重建集群操作。

  <img src="images/gw-vsrx-password.png" alt="图样" style="width: 700px;"/>

* **不要**在高可用性网关的两个服务器上同时执行操作系统重装。

在 HA 网关的两个服务器上同时执行操作系统重装将破坏 vSRX 集群，并导致网关停止运行。如果 vSRX 集群被销毁，那么必须使用**重建集群**选项（在下文中详细描述）来重新供应 vSRX 并重新创建 HA 集群。
{: important}

## 执行操作系统重装
{: #performing-an-os-reload}

要重装网关服务器的操作系统，请执行以下过程：

1. 在客户门户网站中[访问“网关设备”屏幕](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances)，然后通过选择所需的网关名称浏览至“网关详细信息”页面。

  <img src="images/gw-sa-details.png" alt="图样" style="width: 700px;"/>

2. 单击“硬件”面板中的服务器名称。

  ![硬件服务器](images/os_hardware.png)

3. 在设备的页面上，单击“操作”下拉菜单中的**操作系统重装**以访问“服务器配置”页面。

  ![设备详细信息](images/os_device_page.png)

4. 在“服务器配置”页面上，可以配置并启动重装。如果要重装其他操作系统，请单击**操作系统**旁边的 **编辑**，选择 **Juniper**，然后选取其中一个 Juniper vSRX 15.x Standard 选项。修改设置完成后，选择**重装以上配置**以继续。

5. 这将显示“操作系统重装详细信息”屏幕。复查已选择的设置，如果需要更改，请单击**编辑设置**。否则，单击**下一步**以继续。

6. 在“操作系统重装确认”屏幕上，同意“主服务协议”的条款，然后通过单击**确认操作系统重装**来启动操作系统重装过程。如果不想继续重装，请单击**取消**。

## 重建 HA vSRX 集群
{: #rebuilding-an-ha-vsrx-cluster}

要重建某个 HA vSRX 集群，请执行以下过程：

1. 在客户门户网站中[访问“网关设备”屏幕](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances)，然后通过选择所需的 HA 网关名称浏览至“网关详细信息”页面。

2. 单击**操作**下拉列表，并选择**重建集群**。

3. 请仔细阅读警告消息。重建集群的操作具有破坏性。如果要继续，请先保存 vSRX 配置，然后单击**重建**以启动该过程。

  ![确认重建集群](images/rebuild_cluster_confirm.png)
