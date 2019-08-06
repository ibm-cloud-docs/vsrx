---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: working, routing, static, default, creating, ospf, bgp

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

# 使用路由
{: #working-with-routing}

{{site.data.keyword.vsrx_full}} 基于 `JunOS`，为您提供了对完全 Juniper 路由堆栈的访问权。

##静态路由
{: #static-routing}

要配置静态路由，请运行以下命令：

###设置缺省路由
{: #setting-a-default-route}

```
set routing-options static route 0/0 next-hop <Gateway IP>
```

### 创建静态路由
{: #creating-a-static-route}
```
set routing-options static route <PREFIX/MASK> next-hop <Gateway IP>
```  

###基本 OSPF 路由
{: #basic-ospf-routing}

要设置基本 OSPF 路由，并仅使用区域 0，请使用 md5 认证来运行以下命令：

```
set protocols ospf area 0 interface ge-0/0/1.0 authentication md5 0 key <KEY>
```

### 基本 BGP 路由
{: #basic-bgp-routing}

要设置基本 BGP 路由，请首先定义本地 AS：

```
set routing-options autonomous-system 65001
```

然后，配置 BGP 邻居及其会话属性：

```
set protocols bgp group CUSTOMER local-address 1.1.1.1
set protocols bgp group CUSTOMER family inet unicast
set protocols bgp group CUSTOMER family inet6 unicast
set protocols bgp group CUSTOMER peer-as 65002
set protocols bgp group CUSTOMER neighbor 2.2.2.2
```

在此示例中，BGP 配置为用于以下目的：

* 使用源 IP 地址 `1.1.1.1` 来建立会话
* 同时协商 ipv4 和 ipv6 单点广播系列
* 与属于 `AS 65002` 的邻居建立对等连接
* 与邻居 IP `2.2.2.2` 建立对等连接

其他配置可以在 [Juniper Web 站点 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.juniper.net/documentation/en_US/junos11.4/information-products/topic-collections/config-guide-routing/config-guide-routing.pdf){: new_window} 上找到。
