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

# 执行 IBM Cloud Juniper vSRX 基本配置
{: #performing-ibm-cloud-juniper-vsrx-basics}

IBM® Cloud Juniper vSRX 网关可以通过 SSH 使用远程控制台会话进行配置，也可以通过登录到 Juniper Web 管理 GUI 进行配置。

在 vSRX 的 shell 和接口外部配置 vSRX 可能会生成意外结果，因此建议不要这样做。
{: note}

## 使用 SSH 访问设备
{: #accessing-the-device-using-ssh}

可以使用 SSH 通过公共 IP 地址来访问 vSRX，或者如果您使用的是 SoftLayer VPN，那么可以通过专用 IP 地址来访问 vSRX：

1. 转至“网关设备详细信息”屏幕，并获取公共网关 IP 或专用网关 IP。

  <img src="images/gw-sa-details.png" alt="图样" style="width: 700px;"/>

2. 单击“眼睛”图标以显示 admin 用户的密码。

3. 运行 `ssh admin@<gateway-ip>` 命令，然后输入 admin 用户的密码。

如果看不到“眼睛”图标，说明您可能无权查看密码。请与帐户所有者核实您的访问许可权。
{: note}

## 访问配置方式
{: accessing-the-configuration-mode}

在 shell 打开到 vSRX 之后，通过运行 `config` 命令可以进入配置方式。在此方式下可以使用以下命令执行若干操作：

* `show` - 查看配置  
* `show | compare` - 查看编译打包的更改
* `set` - 对更改编译打包
* `commit check` - 验证配置的语法

如果您对更改感到满意，那么可以通过运行 `commit` 命令，再运行 `save` 命令将更改落实到活动配置。  

要退出配置方式，请运行 `exit` 命令。

## 使用 Juniper Web 管理 UI 访问设备
{: #accessing-the-device-using-the-juniper-web-management-ui}

缺省情况下，Juniper Web 管理 GUI 已配置为使用 vSRX 生成的自签名证书。仅端口 8443 上启用了 HTTPS。您可以在 `https://gateway-ip:8443` 上访问 HTTPS。

![网关设备 HA 详细信息](images/vSRX-webui.png)

## 创建系统用户
{: #creating-system-users}

缺省情况下，IBM Cloud Juniper vSRX 针对用户名 `admin` 配置为使用 SSH 访问。可以添加其他用户并使用其自己的一组优先级。例如：


```
set system login user ops class operator authentication encrypted-password <CYPHER>
```

在此示例中，`ops` 是用户名，`operator` 是分配给用户的类/许可权级别。

还可以定义定制类，以取代预定义类。

## 定义 vSRX 主机名
{: #defining-the-vsrx-hostname}

可以使用以下命令来设置或更改 vSRX 主机名：

```
set system host-name <hostname>
```

## 配置 DNS 和 NTP
{: #configuring-dns-and-ntp}

要配置名称服务器解析和 NTP，请运行以下命令：

```
set system name-server <DNS server>
set system ntp <NTP server>
```

## 更改 root 用户密码
{: #changing-the-root-password}

可以通过运行以下命令来更改 root 用户密码：

```
set system root-authentication plain-text-password
```

这将提示您输入新密码，该密码会加密并存储在配置中，并且不会显示。
