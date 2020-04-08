---

copyright:
  years: 2018
lastupdated: "2020-04-01"

keywords: checking, readiness, errors

subcollection: vSRX

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tIP: .tIP}
{:note: .note}
{:important: .important}
{:download: .download}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Understanding readiness errors
{: #readiness-errors}

Readiness check errors you may encounter can either be common errors or version upgrade errors. The below lists provide additional information on these error codes.

## Common readiness errors
{: #common-errors}

The following common errors may occur when running readiness checks.

### Error 1000
{: #error-1000}
An OS Reload is already running on a different node in the HA cluster, the other nodes OS Reload must complete before executing a second OS Reload.

### Error 1002
{: #error-1002}
An error occurred in the connectivity check, please contact support.

### Error 1003
{: #error-1003}
The root user for host is not found.

### Error 1004
{: #error-1004}
The root user credentials for host are not found.

### Error 1005
{: #error-1005}
The host SSH console connection could not be created. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

### Error 1007
{: #error-1007}
The host SSH console connection could not be created. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

### Error 1008
{: #error-1008}
The host SSH console could not process the command. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

### Error 1009
{: #error-1009}
The host has an invalid IP address or is blocked by a firewall, SSH failed. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

### Error 1011
{: #error-1011}
The root user credentials for gateway are not found.

### Error 1012
{: #error-1012}
The gateway SSH console connection failed. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

### Error 1013
{: #error-1013}
The root user for the gateway is not found.

### Error 1014
{: #error-1014}
The gateway readiness check has timed out.

### Error 1017
{: #error-1017}
The gateway SSH console connection could not be created. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

### Error 1018
{: #error-1018}
The gateway SSH console could not process the command. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

### Error 1019
{: #error-1019}
The gateway has an invalid IP address or is blocked by a firewall, SSH failed. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

### Error 1021
{: #error-1021}
An error occurred in the connectivity check, please contact support.

## Version upgrade errors
{: #upgrade-errors}

You may encounter the following errors when running version upgrade readiness checks.

### Errors 2001 - 2004
{: #error-2001}
The host has a readiness check setup failure, please rerun or contact support.

### Error 2007
{: #error-2007}
The host has a readiness check setup failure and can not SSH to the gateway. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

### Error 2008
{: #error-2008}
The host has a readiness check setup failure and can not SSH to the private IP for the other node's host. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

### Error 2009
{: #error-2009}
The host has a readiness check setup failure, a required vSRX interface is down.

### Error 2010
{: #error-2010}
The host has a readiness check setup failure, a required vSRX interface is down.

### Error 2011
{: #error-2011}
The host has a readiness check setup failure, a required vSRX interface is down.

### Error 2012
{: #error-2012}
The host has a readiness check setup failure, the vSRX node is not clustered.

### Errors 2013 and 2014
{: #error-2013}
The host has a readiness check setup failure, the vSRX redundancy group configuration is incorrect.

### Error 2015
{: #error-2015}
The host has a readiness check setup failure, the vSRX FPC is offline.

### Error 2016
{: #error-2016}
The host has a readiness check setup failure, the vSRX PIC is offline.

### Error 2017
{: #error-2017}
The host has a readiness check setup failure, the vSRX license is invalid.

### Error 2018
{: #error-2018}
The host has a readiness check setup failure, the vSRX license could not be validated.

### Error 2019
{: #error-2019}
The host has a readiness check setup failure, please rerun or contact support.

### Error 2020
{: #error-2020}
The host has a readiness check setup failure, change the vSRX configuration to allow more SSH sessions. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

### Error 2021
{: #error-2021}
The host has a readiness check setup failure, please rerun or contact support.

### Error 2022
{: #error-2022}
The host has a readiness check setup failure, the vSRX firewall configuration blocks connectivity.

### Error 2023
{: #error-2023}
The host has a readiness check setup failure, please rerun or contact support.

### Error 2024
{: #error-2024}
The host has a readiness check setup failure, unable to ping the vSRX FXP IP address.

### Error 2025
{: #error-2025}
The host has a readiness check setup failure, unable to SSH to the vSRX FXP IP address. Refer to [Correcting readiness errors](/docs/infrastructure/vSRX?topic=vSRX-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.
