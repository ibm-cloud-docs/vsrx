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

# 回收网关
{: #reclaiming-a-gateway}

执行以下过程来回收网关：

1. 在客户门户网站中[访问“网关设备”屏幕](/docs/infrastructure/vsrx?topic=vsrx-viewing-all-your-gateway-appliances)，然后通过选择所需的网关名称浏览至“网关详细信息”页面。

2. 单击“硬件”面板中的服务器名称。

	![硬件服务器](images/os_hardware.png)

	回收网关之前，请确保所有受保护的 VLAN 都已与该网关[解除关联](/docs/infrastructure/vsrx?topic=vsrx-managing-ibm-vlans)。

3. 在设备的页面上，单击“操作”下拉菜单中的**取消设备**以访问“服务器配置”页面。  

4. 在“取消设备”确认屏幕上，通过单击**继续**以启动回收过程。如果不想继续回收，请单击**关闭**。

对于 HA 对，需要在两个设备上执行这些操作。
