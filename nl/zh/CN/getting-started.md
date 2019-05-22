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

# IBM Cloud Juniper vSRX 网关入门
{: #getting-started}

要开始使用 IBM® Cloud Juniper vSRX 网关，请首先确定您的帐户是否已链接到 IBM Cloud。

## 开始之前

要了解您是否具有链接的帐户，请在浏览器中浏览至[客户门户网站 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){: new_window} 并登录。如果您的帐户未链接，那么将在右上角看到**了解有关 Bluemix 的更多信息！**按钮。

## 订购步骤

可以使用以下其中一种方法来订购网关设备：

有关 IBM Cloud Juniper vSRX 网关已知限制的列表，请参阅[已知限制](/docs/infrastructure/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx)主题。
{:note}

### 使用链接的帐户进行订购
如果您的帐户已链接，请执行以下过程：

1.	打开 [IBM Cloud 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.bluemix.net/){: new_window}，并登录到您的帐户。
2.	在左侧导航中，选择**基础架构 > 网络 > 网关设备**。
3.	在**网关设备**列表中，单击**创建网关**。
4. 在**订购**页面中，选择**主机名**和**域**。
5. 根据需要，选择**高可用性对**选项。

	<img src="images/linked_order.png" alt="图样" style="width: 700px;"/>

5. 接下来，选择**位置**和关联的 **pod**，然后选择**服务器**和所需数量的 **RAM**。

	如果计划使用双处理器多核心服务器，那么必须选择 **Intel Xeon 5120** 作为服务器类型。
{:note:}

	<img src="images/linked_server.png" alt="图样" style="width: 600px;"/>

6. 如果要使用 SSH 密钥来认证对新网关的访问权，请选择该 SSH 密钥。
7. 在**映像**下，对于单处理器服务器，选择 **Juniper vSRX 15.x（最高 1 Gbps）Standard**，对于双处理器服务器，选择 **Juniper vSRX 15.x（最高 10 Gbps）Standard**。
8. 选择任何可选的附加组件，添加任何其他**存储磁盘**，然后选择所需的**上行链路端口速度**。
8. 在**订单摘要**中复查所做的选择，然后阅读并同意“第三方软件条款”。
9. 最后，单击**供应**。

### 使用未链接的帐户进行订购
如果您的帐户未链接，请执行以下过程：

1.	打开[客户门户网站 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){: new_window}，并登录到您的帐户。
2.	在客户门户网站导航中，选择**网络 > 网关设备**。
3.	在**网关设备**列表中，单击**订购网关**。
4.	在**订购**页面中，从下拉菜单中选择所需的数据中心，然后选择要供应 Juniper vSRX 的所需服务器硬件类型。

	如果计划使用双处理器多核心服务器，那么必须选择 **Intel Xeon 5120** 作为服务器类型。
{:note}

5.	在**订购**页面上，根据需要选择**高可用性对**选项，然后选择**内存大小**。
6. 	接下来，单击**操作系统**下的 **Juniper** 选项卡，对于单处理器服务器，选择 **Juniper vSRX 15.x（最高 1 Gbps）Standard**，对于双处理器服务器，选择 **Juniper vSRX 15.x（最高 10 Gbps）Standard**。
7. 	最后，选择所需的网络上行链路速度。
8.	复查您的选择，然后单击**添加到订单**。这将自动验证您的订单。
9.	在**结帐**页面上，如果已在所选数据中心内拥有 VLAN，请选择要保护的后端 VLAN。请确保：
	* 提供服务器的主机名和域名
	* 根据需要，选择用于访问认证的 SSH 密钥
	* 选中 IBM Cloud 服务条款和“第三方软件条款”的所有框
10. 单击**提交订单**。

## 后续步骤
订单被核准后，vSRX 的供应会自动启动。供应过程完成后，网关会显示在**网关设备**列表中。

单击网关名称可打开**网关详细信息**页面。您将找到该设备的 IP 地址、登录用户名和密码。

<img src="images/after_order.png" alt="图样" style="width: 700px;"/>
