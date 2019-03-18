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

# 使用防火牆
{: #working-with-firewalls}

IBM® Cloud Juniper vSRX 使用安全區域的概念，其中每一個 vSRX 介面都會對映至一個「區域」，以處理有狀態的防火牆。無狀態防火牆是由防火牆過濾器控制。

原則是用來容許及封鎖這些已定義區域之間的資料流量，且這裡定義的規則是有狀態的。

在 IBM Cloud 中，vSRX 是設計成具有四個不同的安全區域：

| 區域                     | 獨立式介面 | HA 介面 |
| :---                     |        :----:        |         ---: |
| SL-Private（未標記）    | ge-0/0/0.0           | reth0.0      |
| SL-Public（未標記）    | ge-0/0/1.0           | reth1.0      |
| Customer-Private（已標記）| ge-0/0/0.1           | reth2.1      |
| Customer-Public（已標記）| ge-0/0/1.1           | reth3.1      |

## 區域原則
若要配置有狀態防火牆，請執行下列程序：

1. 建立安全區域並指派個別介面：

	獨立式情境：
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces ge-0/0/1.1
	```
	高可用性情境：
	```
	set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.1
	set security zones security-zone CUSTOMER-PUBLIC interfaces reth2.1
	```
2. 定義兩個不同區域之間的原則及規則。

	下列範例說明如何將 `Customer-Private` 區域中的資料流量 ping 至 `Customer-Public`：

	```
	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP match source-address any destination-address any application junos-icmp

	set security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PUBLIC policy ALLOW_ICMP then permit
	```

以下是可在原則中定義的部分屬性：

* 來源端位址
* 目的地位址
* 應用程式
* 動作 (permit/deny/reject/count/log)

因為這是有狀態作業，所以不需要容許傳回封包（在此情況下，指的是 echo 回覆）。

使用下列指令，容許導向至 vSRX 的資料流量：

獨立式案例：
```
set security zones security-zone CUSTOMER-PRIVATE interfaces ge-0/0/0.0 host-inbound-traffic system-services all
```
HA 案例：
```
set security zones security-zone CUSTOMER-PRIVATE interfaces reth2.0 host-inbound-traffic system-services all
```

若要容許通訊協定（例如 OSPF 或 BGP），請使用下列指令：

獨立式案例：
```
set security zones security-zone trust interfaces ge-0/0/0.0 host-inbound-traffic protocols all
```
HA 案例：
```
set security zones security-zone trust interfaces reth2.0 host-inbound-traffic protocols all
```

## 防火牆過濾器
依預設，IBM Cloud Juniper vSRX 容許 ping、SSH 及 HTTPS 至本身，並藉由將 `PROTECT-IN` 過濾器套用至 `lo` 介面來捨棄所有其他資料流量。

若要配置新的無狀態防火牆，請執行下列程序：

1. 建立防火牆過濾器及項目（下列過濾器僅容許 ICMP，並捨棄所有其他資料流量）
	```
	set firewall filter ALLOW-PING term ICMP from protocol icmp
	set firewall filter ALLOW-PING term ICMP then accept
	```

2. 將過濾器規則套用至介面（下列指令會將過濾器套用至所有專用網路資料流量）
	```
	set interfaces ge-0/0/0 unit 0 family inet filter input ALLOW-PING
	```
