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

# IBM Cloud Juniper vSRX 网关入门
{: #getting-started}

要开始使用 IBM® Cloud Juniper vSRX 网关，请首先确定您的帐户是否已链接到 IBM Cloud。

要了解您是否具有链接的帐户，请在浏览器中浏览至[客户门户网站 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){: new_window} 并登录。如果您的帐户已链接，那么不会在右上角看到**了解有关 Bluemix 的更多信息！**按钮。

## 订购步骤
{: #steps-for-ordering}

可以使用以下其中一种方法来订购网关设备：

有关 IBM Cloud Juniper vSRX 网关已知限制的列表，请参阅[已知限制](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx)主题。
{: note}

### 使用链接的帐户进行订购
{: #ordering-with-a-linked-account}

如果您的帐户已链接，请执行以下过程：

1. 在浏览器中，打开 [Cloud 目录 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/gen1/infrastructure/provision/gateway){: new_window}，并登录到您的帐户。

  您还可以通过登录到 [IBM Cloud UI 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com)，并选择**经典基础架构 > 网络 > 网关设备**来访问此页面。
或者，在 [IBM Cloud 目录 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/catalog) 中，选择**网络**类别，然后选择**网关设备**磁贴。

2. 在**网关供应商**下，选择 **Juniper vSRX（最高 1 Gbps）**或 **Juniper vSRX（最高 10 Gbps）**。

3. 在**网关设备**部分中，输入**主机名**和**域名**信息。这些字段已经填充有缺省信息，因此请确保这些值正确。

	<img src="images/linked_order.png" alt="图样" style="width: 700px;"/>

4. 根据需要选择**高可用性**选项，选择所需的数据中心**位置**，然后从下拉菜单中选择所需的特定 **pod**。

  此菜单中只会显示已具有关联 VLAN 的 pod。如果希望在未列出的 pod 中供应网关设备，请首先在该 pod 中创建 VLAN。
  {: note}

	<img src="images/linked_server.png" alt="图样" style="width: 600px;"/>

4. 在**配置**部分中，通过选择 RAM 和 SSH 密钥（如果要使用 SSH 密钥来认证对新网关的访问权）来选择处理器。

  根据您在步骤 2 中选择的许可证版本，系统会选择相应的处理器。不过，您可以选择其他 RAM 配置。
  {: note}

5. 在**存储磁盘**部分中，选择满足存储需求的选项。

  RAID0 和 RAID1 选项可用于提升数据丢失防御能力，还增强了热备用（主组件发生故障时，可以立即投入运行的备份组件）的功能。
  {: note}

  每个 vSRX 最多可以有四个磁盘。使用 RAID 配置的“磁盘大小”是可用磁盘大小，因为 RAID 配置是镜像的。
  {: note}

  如果计划运行生成详细日志的网络诊断，请保留大于缺省设置的磁盘空间。
  {: tip}

6. 在**网络接口**部分中，选择**上行端口速度**。缺省选择是单接口，但还有冗余和仅专用选项。请选择最适合您需求的选项。

  “网络接口”的**附加组件**部分允许您根据需要选择 IPv6 地址，并显示任何其他包含的缺省选项。

8. 复查选择，选中表明您已阅读第三方服务协议的对应复选框，然后单击**创建**。这将自动验证订单。

订单被核准后，IBM Cloud Juniper vSRX 网关的供应会自动启动。供应过程完成后，新的 vSRX 会显示在“网关设备”列表页面中。单击网关名称可打开“网关详细信息”页面。在其中将找到设备的 IP 地址、登录用户名和密码。  

请记住，通过 IBM Cloud“目录”订购和配置网关后，还必须使用相同的设置配置设备本身。
{: tip}

### 使用未链接的帐户进行订购
{: #ordering-with-a-unlinked-account}

如果您的帐户未链接，请执行以下过程：

1.	打开[客户门户网站 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){: new_window}，并登录到您的帐户。
2.	在客户门户网站导航中，选择**网络 > 网关设备**。
3.	在**网关设备**列表中，单击**订购网关**。
4.	在**订购**页面中，从下拉菜单中选择所需的数据中心，然后选择要供应 Juniper vSRX 的所需服务器硬件类型。

	如果计划使用双处理器多核心服务器，那么必须选择 **Intel Xeon 5120** 作为服务器类型。
  {: note}

5.	在**订购**页面上，根据需要选择**高可用性对**选项，然后选择**内存大小**。
6. 	接下来，单击**操作系统**下的 **Juniper** 选项卡，对于单处理器服务器，选择 **Juniper vSRX（最高 1 Gbps）Standard**，对于双处理器服务器，选择 **Juniper vSRX（最高 10 Gbps）Standard**。
7. 	最后，选择所需的网络上行链路速度。
8.	复查您的选择，然后单击**添加到订单**。这将自动验证您的订单。
9.	在**结帐**页面上，如果已在所选数据中心内拥有 VLAN，请选择要保护的后端 VLAN。请确保：
	* 提供服务器的主机名和域名。
	* 根据需要，选择用于访问认证的 SSH 密钥。
	* 选中 IBM Cloud 服务条款和“第三方软件条款”的所有框。
10. 单击**提交订单**。

## 后续步骤
{: #what-s-next-}

订单被核准后，vSRX 的供应会自动启动。供应过程完成后，网关会显示在**网关设备**列表中。

单击网关名称可打开**网关详细信息**页面。您将找到该设备的 IP 地址、登录用户名和密码。

<img src="images/after_order.png" alt="图样" style="width: 700px;"/>
