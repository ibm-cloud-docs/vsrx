---

copyright:
  years: 2018
lastupdated: "2018-10-22"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Neue Datenflüsse erstellen
Nachdem Sie nun die neue Zone (`CUSTOMER-PUBLIC`) erstellt haben, müssen Sie Richtlinien konfigurieren, um den Netzdatenfluss zu steuern. Die erste unten konfigurierte Richtlinie lässt innerhalb der Zone `CUSTOMER-PUBLIC` jeglichen Datenverkehr zu. Die zweite Richtlinie lässt jeglichen Datenverkehr von `CUSTOMER-PUBLIC` an das öffentliche Internet zu, während die dritte Richtlinie nur SSH- und PING-Datenverkehr aus dem öffentlichen Internet an `CUSTOMER-PUBLIC` zulässt und den Rest löscht (da die Standardaktion 'Löschen' (`drop`) lautet).

**Anmerkung:** Blättern Sie nach rechts, um den gesamten Befehl anzuzeigen.  

```
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL description "Jeglichen Datenverkehr innerhalb der Zone CUSTOMER_PUBLIC zulassen"
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL match source-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL match destination-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL match application any
set security policies from-zone CUSTOMER-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_INTERNAL then permit

set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND description "Jeglichen ausgehenden Datenverkehr von CUSTOMER-PUBLIC an das Internet zulassen"
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND match source-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND match destination-address any
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND match application any
set security policies from-zone CUSTOMER-PUBLIC to-zone SL-PUBLIC policy ALLOW_OUTBOUND then permit

set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH description "Ping und SSH vom Internet an öffentliches Teilnetz zulassen"
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match source-address any
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match destination-address VSI_PUB_NET
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match application junos-ssh
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH match application junos-ping
set security policies from-zone SL-PUBLIC to-zone CUSTOMER-PUBLIC policy ALLOW_PING_SSH then permit
```  
