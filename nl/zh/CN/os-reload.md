---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}

# 重装和迁移操作系统
{: #reloading-an-migrating-the-os}

操作系统重装过程用于重建网关服务器。此过程执行以下操作：

* 重装服务器主机的操作系统
* 在操作系统中安装 KVM
* 在 KVM 中创建 vSRX VM
* 使用 IBM® Cloud 的缺省配置重新配置 vSRX

该过程通常需要 1 小时 40 分钟才能完成。在此期间，独立网关将停止运行。对于 Juniper 高可用性 (HA) 网关，在其中一个服务器上重装操作系统时，vSRX 会故障转移到集群中的另一个服务器，并继续处理数据流量。重装完成后，服务器将重新加入集群。

**注意：**如果已在运行 Juniper vSRX HA 集群，请不要同时在 HA 网关的两个服务器上执行操作系统重装。这样做会销毁 vSRX 集群并导致网关停止运行。如果 vSRX 集群被销毁，那么必须使用**重建集群**选项（在下文中详细描述）来重新供应 vSRX 并重新创建 HA 集群。

## 执行操作系统重装
要重装网关服务器的操作系统，请执行以下过程：

1. 在客户门户网站中[访问“网关设备”屏幕](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances)，然后通过选择所需的网关名称浏览至“网关详细信息”页面。

2. 单击“硬件”面板中的服务器名称。
![硬件服务器](images/os_hardware.png)

3. 在设备的页面上，单击“操作”下拉菜单中的**操作系统重装**以访问“服务器配置”页面。
![设备详细信息](images/os_device_page.png)

4. 在“服务器配置”页面上，可以配置并启动重装。如果要重装其他操作系统，请单击**操作系统**旁边的 **编辑**，选择 **Juniper**，然后选取其中一个 Juniper vSRX 15.x Standard 选项。修改设置完成后，选择**重装以上配置**以继续。

5. 这将显示“操作系统重装详细信息”屏幕。复查已选择的设置，如果需要更改，请单击**编辑设置**。否则，单击**下一步**以继续。


6. 在“操作系统重装确认”屏幕上，同意“主服务协议”的条款，然后通过单击**确认操作系统重装**来启动操作系统重装过程。如果不想继续重装，请单击**取消**。

## 使用操作系统重装从 Vyatta/VRA 服务器迁移到 Juniper vSRX
如果重装的是独立 Vyatta 服务器，那么在操作系统重装完成后，将供应独立的 Juniper vSRX。将使用相同的网关 IP 地址，并且将重置主机服务器上 root 用户的密码（以及 vSRX 中 admin 和 root 用户的密码）。

如果重装的是高可用性 Vyatta 服务器，那么必须在两个硬件服务器上都执行操作系统重装。这将安装 Ubuntu 16.04。接下来，使用“重建集群”选项（在以下部分中详细描述）来供应 vSRX 并创建 HA 集群。与独立 vSRX 一样，将使用相同的网关 IP 地址，并且将重置主机服务器上 root 用户的密码（以及 vSRX 中 admin 和 root 用户的密码）。

**注意：**不要只在 Vyatta HA 集群的一台服务器上执行操作系统重装。不支持在单个网关 HA 集群上具有两个不同的操作系统。

## 重建 HA vSRX 集群
要重建某个 HA vSRX 集群，请执行以下过程：

1. 在客户门户网站中[访问“网关设备”屏幕](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances)，然后通过选择所需的 HA 网关名称浏览至“网关详细信息”页面。

2. 单击 vSRX 面板中的**重建集群**。
![重建集群](images/rebuild_cluster.png)

3. 请仔细阅读警告消息。重建集群的操作具有破坏性。如果要继续，请先保存 vSRX 配置，然后单击**重建**以启动该过程。
![确认重建集群](images/rebuild_cluster_confirm.png)
