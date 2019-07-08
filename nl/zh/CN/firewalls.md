---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords:

subcollection: vsrx, firewalls, working, policy, policies, rules, zones, standalone, ha

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

# 使用防火墙
{: #working-with-firewalls}

IBM® Cloud Juniper vSRX 使用了安全专区的概念，其中每个 vSRX 接口会映射到一个“专区”以处理有状态防火墙。无状态防火墙通过防火墙过滤器进行控制。

策略用于允许和阻止这些所定义专区之间的流量，并且此处定义的规则是有状态的。

在 IBM Cloud 中，vSRX 设计为具有四个不同的安全专区：

|专区|独立接口|HA 接口|
| :---                     |        :----:        |         ---: |
|SL-Private（未标记）|ge-0/0/0.0 或 ae0.0|reth0.0|
|SL-Public（未标记）|ge-0/0/1.0 或 ae1.0|reth1.0|
|Customer-Private（已标记）|ge-0/0/0.1 或 ae0.1|reth2.1|
|Customer-Public（已标记）|ge-0/0/1.1 或 ae1.1|reth3.1|

## 专区策略
{: #zone-policies}

要配置有状态防火墙，请执行以下过程：

1. 创建安全专区，并分配相应的接口：

	独立场景：
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces ge-0/0/1.1
	```
	高可用性场景：
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces reth2.1
	```
2. 定义两个不同专区之间的策略和规则。

	以下示例说明了从专区 `Customer-Private` 流至 `Customer-Public` 的 ping 流量：

	```
	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP match source-address any destination-address any application junos-icmp

	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP then permit
	```

下面是可以在策略中定义的一些属性：

* 源地址
* 目标地址
* 应用程序
* 操作 (permit/deny/reject/count/log)

由于这是有状态操作，因此不需要允许返回包（在本例中，回传会应答）。

使用以下命令以允许定向到 vSRX 的流量：

独立用例：
```
set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.0 host-inbound-traffic system-services all
```
HA 用例：
```
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.0 host-inbound-traffic system-services all
```

要允许协议（例如，OSPF 或 BGP），请使用以下命令：

独立用例：
```
set security zones security-zone trust interfaces ge-0/0/0.0 host-inbound-traffic protocols all
```
HA 用例：
```
set security zones security-zone trust interfaces reth2.0 host-inbound-traffic protocols all
```

## 防火墙过滤器
{: #firewall-filters}

缺省情况下，IBM Cloud Juniper vSRX 支持流至其自身的 ping、SSH 和 HTTPS 流量，并通过将 `PROTECT-IN` 过滤器应用于 `lo` 接口来丢弃其他所有流量。

要配置新的无状态防火墙，请执行以下过程：

1. 创建防火墙过滤器和过滤项（以下过滤器仅允许 ICMP 并丢弃其他所有流量）
	```
	set firewall filter ALLOW-PING term ICMP from protocol icmp
	set firewall filter ALLOW-PING term ICMP then accept
	```

2. 将过滤规则应用于接口（以下命令将过滤器应用于所有专用网络流量）
	```
	set interfaces ge-0/0/0 unit 0 family inet filter input ALLOW-PING
	```
