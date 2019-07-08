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

您可以從[閘道應用裝置詳細資料畫面](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)執行各種動作。

## 建立 VLAN 與閘道應用裝置的關聯
{: #associate-a-vlan-to-a-gateway-appliance}

VLAN 需要先與「閘道應用裝置」相關聯，然後才能遞送。VLAN 關聯是將合格的 VLAN 鏈結至「網路閘道」，讓它可以遞送至「閘道應用裝置」。此關聯不會自動將 VLAN 遞送至「閘道應用裝置」；VLAN 會繼續使用前端及後端客戶路由器，直到遞送完成為止。

VLAN 一次只能與一個「閘道」相關聯，且不得有防火牆。請執行下列程序，來建立 VLAN 與「網路閘道」的關聯。

1. 在「客戶入口網站」中[存取「閘道應用裝置詳細資料」畫面](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)。
2. 選取 VLAN 標籤。
3. 按一下**關聯 VLAN**，並從下拉清單中選取 VLAN。
4. 按一下**儲存**，並確認您的選項。VLAN 關聯動作不會透過防火牆遞送 VLAN。

將 VLAN 與「閘道應用裝置」相關聯之後，它會出現在「閘道應用裝置詳細資料」畫面的「關聯的 VLAN」區段中。在此區段中，VLAN 可以遞送至「閘道」，或與「閘道」取消關聯。您隨時可以重複上述步驟，以建立其他合格 VLAN 與「閘道應用裝置」的關聯。

## 遞送關聯的 VLAN
{: #route-an-associated-vlan}

關聯的 VLAN 會鏈結至「閘道應用裝置」，但在 VLAN 遞送之前，進出 VLAN 的資料流量不會到達「閘道」。在遞送相關聯的 VLAN 之後，所有前端及後端資料流量都會透過「閘道應用裝置」進行遞送，而不是客戶路由器進行遞送。

請執行下列程序來遞送關聯的 VLAN：

1. 在「客戶入口網站」中[存取「閘道應用裝置詳細資料」畫面](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)。
2. 選取 VLAN 標籤。
3. 透過切換勾選框來選取所需的 VLAN。
4. 按一下**遞送方式**，並確認您的選項。

在遞送 VLAN 之後，所有前端及後端資料流量都會從客戶路由器移至「網路閘道」。與資料流量及「閘道應用裝置」本身相關的其他控制項，可藉由存取「閘道」的管理工具來取得。藉由[略過「閘道應用裝置」](#bypass-gateway-appliance-routing-for-a-vlan)，即可隨時停止透過「網路閘道」進行的遞送。

## 略過 VLAN 的閘道應用裝置遞送
{: #bypass-gateway-appliance-routing-for-a-vlan}

在遞送 VLAN 之後，所有前端及後端資料流量都會透過「網路閘道」。隨時都可以略過「閘道應用裝置」，讓資料流量回到前端和後端客戶路由器（FCR 和 BCR）。

略過 VLAN 可讓 VLAN 保持與「網路閘道」的關聯。如果 VLAN 不應再與「閘道應用裝置」相關聯，請參閱[取消 VLAN 與閘道應用裝置的關聯](#disassociate-a-vlan-from-a-gateway-appliance)。

請執行下列程序，以略過 VLAN 的「閘道」遞送：

1. 在「客戶入口網站」中[存取「閘道應用裝置詳細資料」畫面](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)。
2. 選取 VLAN 標籤。
3. 透過切換勾選框來選取所需的 VLAN。
4. 按一下**遞送路線**，並確認您的選項。

在略過「網路閘道」之後，所有前端及後端資料流量都會透過與 VLAN 相關聯的 FCR 及 BCR 遞送。VLAN 將繼續與「閘道應用裝置」相關聯，且隨時可遞送回到「閘道應用裝置」。

## 取消 VLAN 與閘道應用裝置的關聯
{: #disassociate-a-vlan-from-a-gateway-appliance}

VLAN 可透過[關聯](#associate-a-vlan-to-a-gateway-appliance)，一次鏈結至一個「閘道應用裝置」。關聯可容許隨時將 VLAN 遞送至「閘道應用裝置」。如果 VLAN 應該與另一個「閘道應用裝置」相關聯，或者 VLAN 不應再與其「閘道」相關聯，則需要取消關聯。取消關聯會移除從 VLAN 到「閘道應用裝置」的「鏈結」，並視需要容許它與另一個「閘道」相關聯。

請執行下列程序，來取消 VLAN 與「閘道應用裝置」的關聯：

1. 在「客戶入口網站」中[存取「閘道應用裝置詳細資料」畫面](/docs/infrastructure/vsrx?topic=vsrx-viewing-your-gateway-appliance-details)。
2. 選取 VLAN 標籤。
3. 透過切換勾選框來選取所需的 VLAN。
4. 按一下**取消關聯**，並確認您的選項。

在取消 VLAN 與「閘道應用裝置」的關聯之後，VLAN 可以與另一個「閘道」相關聯。VLAN 也可以隨時再次與「閘道應用裝置」相關聯。在取消 VLAN 與「閘道應用裝置」的關聯之後，VLAN 的資料流量即無法透過「閘道」遞送。VLAN 必須先與「閘道應用裝置」相關聯，然後才能遞送。

## 透過相同的網路介面遞送多個 VLAN
{: #route-multiple-vlans-over-the-same-network-interface}

IBM® Cloud Juniper vSRX 可以透過相同的網路介面搭配多個 VLAN 操作。它也可以同時處理未標記及已標記的資料流量。此動作是在獨立式裝置上透過將介面封裝設為 `flexible-vlan-tagging` 來完成，或是在「高可用性」裝置透過使用 reth2 和 reth3 作為已標記介面來完成。此作法是預設配置的一部分，且不需要進行修改。在獨立式裝置上，「裝置 0」是未標記的子介面；其他非零裝置則已標記。

使用下列一組指令來配置其他已標記的介面：

獨立式案例：
```
set interfaces ge-0/0/0 unit 50 vlan-id 50
set interfaces ge-0/0/0 unit 50 family inet address <IP/MASK>
```

HA 案例：
```
set interfaces reth2 unit 50 vlan-id 50
set interfaces reth2 unit 50 family inet address <IP/MASK>
```

即使未標記單位 0，`JunOS` 也需要使用它來參照配置為 `native-vlan` 的 VLAN ID。在範例中，由於 `native-vlan-id` 為 `10`，裝置 0 也應具有 `10` 的 `vlan-id`。如此一來，將通知 `JunOS`，裝置 0 應該為未標記。
{: note}

## vSRX 的 VLAN 配置範例
{: #sample-vlan-configuration-for-vsrx}

下面是 vSRX 的配置範例，其定義了兩個專用介面及一個客戶區域。使用此配置範例，「專用 VLAN1」與「專用 VLAN2」可以彼此通訊。獨立式 vSRX 介面會定義為 ge-0/0/0（專用）及 ge-0/0/1（公用），而且若為「高可用性」實例，它們則會定義為 reth2（HA 專用）及 reth3（HA 公用）。

<img src="images/Sample-Topology-VLAN-to-VLAN.png" alt="圖片" style="width: 500px;"/>

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
