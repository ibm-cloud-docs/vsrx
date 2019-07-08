---

copyright:
  years: 2018
lastupdated: "2018-10-22"

keywords: manage, managing, vlan, gateway, route, bypass, disassociate, associate, configuration, disassociating, associating, standalone, ha

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

# 管理 IBM VLAN
{: #managing-ibm-vlans}

您可以在[“网关设备详细信息”屏幕](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)中执行各种操作。

## 将 VLAN 与网关设备相关联
{: #associate-a-vlan-to-a-gateway-appliance}

VLAN 需要与网关设备关联，然后才能对其进行路由。VLAN 关联是将有资格的 VLAN 链接到网关，以便可以将其路由到网关设备。此关联不会自动将 VLAN 路由到网关设备；在路由该 VLAN 之前，该 VLAN 会继续使用前端和后端客户路由器。

一次只能将 VLAN 与一个网关相关联，并且 VLAN 不能有防火墙。执行以下过程来将 VLAN 与网关相关联。

1. 在客户门户网站中[访问“网关设备详细信息”屏幕](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)。
2. 选择 VLAN 选项卡。
3. 单击**关联 VLAN**，然后从下拉列表中选择 VLAN。
4. 单击**保存**，并确认您的选择。VLAN 关联操作不会通过防火墙路由 VLAN。

将 VLAN 关联到网关设备后，该 VLAN 就会显示在“网关设备详细信息”屏幕的“关联的 VLAN”部分中。在此部分中，可以将 VLAN 路由到网关，也可以解除它与网关的关联。通过重复上述步骤，可以随时将其他有资格的 VLAN 与网关设备相关联。

## 路由关联的 VLAN
{: #route-an-associated-vlan}

关联的 VLAN 已链接到网关设备，但在路由该 VLAN 之前，进出该 VLAN 的流量不会命中相应的网关。路由关联的 VLAN 后，所有前端流量和后端流量都会通过网关设备路由，而不再通过客户路由器路由。

执行以下过程来路由关联的 VLAN：

1. 在客户门户网站中[访问“网关设备详细信息”屏幕](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)。
2. 选择 VLAN 选项卡。
3. 通过切换复选框来选择所需的 VLAN。
4. 单击**通过以下项路由：**，并确认您的选择。

路由 VLAN 后，所有前端和后端流量都会从客户路由器移至网关。通过访问网关的管理工具，可取得与流量和网关设备本身相关的其他控制权。可随时通过[绕过网关设备](#bypass-gateway-appliance-routing-for-a-vlan)来中断通过网关进行的路由。

## 绕过 VLAN 的网关设备路由
{: #bypass-gateway-appliance-routing-for-a-vlan}

路由 VLAN 后，所有前端流量和后端流量都通过网关传递。可随时绕过网关设备，使流量恢复为通过前端和后端客户路由器（FCR 和 BCR）传递。

绕过 VLAN 时允许该 VLAN 保持与网关的关联。如果 VLAN 不应该再与网关设备相关联，请参阅[解除 VLAN 与网关设备的关联](#disassociate-a-vlan-from-a-gateway-appliance)。

执行以下过程来绕过 VLAN 的网关路由：

1. 在客户门户网站中[访问“网关设备详细信息”屏幕](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)。
2. 选择 VLAN 选项卡。
3. 通过切换复选框来选择所需的 VLAN。
4. 单击**绕过以下项路由：**，并确认您的选择。

在绕过网关后，所有前端和后端流量都将通过与 VLAN 关联的 FCR 和 BCR 进行路由。VLAN 将保持与网关设备相关联，并且可以随时恢复路由到网关设备。

## 解除 VLAN 与网关设备的关联
{: #disassociate-a-vlan-from-a-gateway-appliance}

通过[关联](#associate-a-vlan-to-a-gateway-appliance)，一次可以将 VLAN 链接到一个网关设备。关联允许随时将 VLAN 路由到网关设备。如果 VLAN 应该与其他网关设备相关联，或者如果 VLAN 不应该再与其网关相关联，那么需要解除关联。解除关联会除去 VLAN 与网关设备的“链接”，从而允许根据需要将其与其他网关相关联。

执行以下过程来解除 VLAN 与网关设备的关联：

1. 在客户门户网站中[访问“网关设备详细信息”屏幕](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)。
2. 选择 VLAN 选项卡。
3. 通过切换复选框来选择所需的 VLAN。
4. 单击**解除关联**，并确认您的选择。

解除 VLAN 与网关设备的关联后，该 VLAN 即可与其他网关相关联。该 VLAN 还可以随时恢复与网关设备相关联。解除 VLAN 与网关设备的关联后，该 VLAN 的流量即无法通过该网关路由。VLAN 必须与网关设备关联，然后才能对其进行路由。

## 通过同一网络接口路由多个 VLAN
{: #route-multiple-vlans-over-the-same-network-interface}

IBM® Cloud Juniper vSRX 可以通过同一网络接口来操作多个 VLAN。它还可以同时处理未标记和已标记的流量。通过将接口封装设置为 `flexible-vlan-tagging`（在独立设备上），或将 reth2 和 reth3 用作已标记接口（在高可用性设备上），可完成此操作。这将作为缺省配置的一部分完成，并且不需要进行修改。在独立设备上，单元 0 是未标记的子接口；其他非零单元均为已标记子接口。

使用以下一组命令来配置其他已标记接口：

独立用例：
```
set interfaces ge-0/0/0 unit 50 vlan-id 50
set interfaces ge-0/0/0 unit 50 family inet address <IP/MASK>
```

HA 用例：
```
set interfaces reth2 unit 50 vlan-id 50
set interfaces reth2 unit 50 family inet address <IP/MASK>
```

尽管单元 0 未标记，`JunOS` 也需要使用它来引用配置为 `native-vlan` 的 VLAN 标识。在此示例中，由于 `native-vlan-id` 为 `10`，因此单元 0 的 `vlan-id` 也应该为 `10`。这样，`JunOS` 就会收到通知，声明单元 0 应该是未标记的。
{: note}

## vSRX 的样本 VLAN 配置
{: #sample-vlan-configuration-for-vsrx}

下面是 vSRX 的样本配置，其中定义了两个专用接口和一个客户专区。对于此样本配置，Private VLAN1 和 Private VLAN2 可以相互通信。独立 vSRX 接口定义为 ge-0/0/0（专用）和 ge-0/0/1（公共），对于高可用性实例，则定义为 reth2（HA 专用）和 reth3（HA 公共）。

<img src="images/Sample-Topology-VLAN-to-VLAN.png" alt="图样" style="width: 500px;"/>

```
# show interfaces

ge-0/0/0 {
   description PRIVATE_VLANs;
   flexible-vlan-tagging;
   native-vlan-id 1121;
   unit 0 {
       vlan-id 1121;
       family inet {
           address 10.184.108.158/26;
       }
   }
   unit 10 {
       vlan-id 1811;
       family inet {
           address 10.184.237.201/29;
       }
   }
   unit 20 {
       vlan-id 1812;
       family inet {
           address 10.185.48.9/29;
       }
   }
}


# show security zones security-zone CUSTOMER-PRIVATE
interfaces {
   ge-0/0/0.10 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
   ge-0/0/0.20 {
       host-inbound-traffic {
           system-services {
               all;
           }
       }
   }
}
# show security policies from-zone CUSTOMER-PRIVATE to-zone CUSTOMER-PRIVATE
policy Allow_C_C {
   match {
       source-address any;
       destination-address any;
       application any;
   }
   then {
       permit;
   }
}
```
