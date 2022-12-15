---

copyright:
  years: 2018, 2021
lastupdated: "2022-08-05"

keywords: checking, readiness, errors

subcollection: vSRX

---

{{site.data.keyword.attribute-definition-list}}

# Understanding readiness errors and warnings
{: #readiness-errors}

Readiness check warnings and errors can occur for any of the three readiness checks: OS reload, license upgrade, or version upgrade. The following list provides information on these error and warning codes.

## Error 1000
{: #error-1000}

An OS reload is already running on a different node in the HA cluster. The other node's OS reload must complete before executing a second OS reload.

## Error 1002
{: #error-1002}

An error occurred in the connectivity check. Contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help).

## Error 1003
{: #error-1003}

The root user for the host is not found.

## Error 1004
{: #error-1004}

The root user credentials for the host are not found.

## Error 1005
{: #error-1005}

The host SSH console connection could not be created. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1007
{: #error-1007}

The host SSH console connection could not be created. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1008
{: #error-1008}

The host SSH console could not process the command. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1009
{: #error-1009}

The host has an invalid IP address, or is blocked by a firewall. SSH failed. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1011
{: #error-1011}

The root user's credentials for the gateway were not found.

## Error 1012
{: #error-1012}

The gateway SSH console connection failed. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1013
{: #error-1013}

The root user for the gateway was not found.

## Error 1014
{: #error-1014}

The gateway readiness check has timed out.

## Error 1017
{: #error-1017}

The gateway SSH console connection could not be created. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1018
{: #error-1018}

The gateway SSH console could not process the command. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1019
{: #error-1019}

The gateway has an invalid IP address, or is blocked by a firewall. SSH failed. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1021
{: #error-1021}

An error occurred in the connectivity check. Contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help).

## Error 1022
{: #error-1022}

The gateway readiness precheck failed with an unexpected exception. Try again or contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help).

## Error 1023
{: #error-1023}

The gateway readiness precheck failed the DNS accessibility check on the Ubuntu host. Confirm there is network access to the private `10.0.0.0/8` subnet from the host.

## Error 1024
{: #error-1024}

The gateway readiness precheck failed with an unexpected exception. Try again or contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help).

## Error 1025
{: #error-1025}

The IPMI interface is disabled for the Gateway host. Check IPMI status and enable the interface if is disabled. Try again or contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help).

## Error 1026
{: #error-1026}

The Ubuntu host is unable to write to the attached storage as it is read only. Reboot the host and try again or contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help). 

## Error 1101
{: #error-1101}

An error occurred during the readiness check. Try again or contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help).

## Error 1102
{: #error-1102}

The host experienced a precheck setup failure. Try again or contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help).

## Error 1103
{: #error-1103}

The host experienced a precheck setup failure. Try again or contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help).

## Error 1104
{: #error-1104}

The host experienced a precheck setup failure. Try again or contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help).

## Error 1105
{: #error-1105}

The host experienced a precheck setup failure and cannot SSH to the gateway. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1106
{: #error-1106}

The host experienced a precheck setup failure and cannot SSH to the private IP for the other node's host. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1107
{: #error-1107}

The host experienced a precheck setup failure due to an invalid password. Correct the password and try again. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1108
{: #error-1108}

The gateway experienced a precheck setup failure due to an invalid password. Correct the password and try again. Refer to [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1109
{: #error-1109}

The gateway experienced a precheck setup failure, and is unable to check the vSRX disk capacity. Remove any unnecessary files from `/var` and try again.

## Error 1110
{: #error-1110}

The gateway experienced a precheck setup failure because the vSRX file system reached capacity. Remove any unneecessary files from `/var` and try again.

## Error 1111
{: #error-1111}

The gateway experienced a precheck setup failure due to a general failure in the JunOS RPC call. Try again or contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help).

## Error 1112
{: #error-1112}

The gateway experienced a precheck setup failure due to a cluster error. Ensure redundancy group 0 is online and has no monitor-failures.

## Error 1113
{: #error-1113}

The host experienced a precheck setup failure and is unable to determine the status of the host VM using `virsh`. Try again or contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help).

## Error 1114
{: #error-1114}

The host has a precheck setup failure because insufficient memory is installed on the bare-metal server. A minimum of 32 GB is required. Contact [IBM Support](/docs/vsrx?topic=gateway-appliance-getting-help) to install the required amount of memory.

## Error 1115
{: #error-1115}

The gateway has a precheck setup failure due to an incompatible SSH connection limit in the vSRX configuration. Remove the SSH connection limit from the vSRX configuration and retry.

## Error 1116
{: #error-1116}

The host has a precheck setup failure, Ubuntu is missing the telnet software package. Install telnet and retry.

## Error 1117
{: #error-1117}

The host's Ubuntu mirror server is not accessible. Retry the operation once the mirror is accessible.

## Error 1118
{: #error-1118}

The vSRX node is not started. Start the vSRX VM and retry the operation.

## Error 1119
{: #error-1119}

The vSRX node's VM is running but the node is not accessible via telnet. Exit from all console (telnet) sessions and retry the operation.

## Error 1120
{: #error-1120}

The vSRX node does not have a valid license. Remove any evaluation licenses and apply a valid license. Then retry the operation. Refer to [Known limitations for IBM Cloud Juniper vSRX](/docs/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx) for more information on identifying and removing the evaluation license.

## Error 1121
{: #error-1121}

License operations against vSRX v15.1 are not supported. Upgrade to a newer version of the vSRX.

## Error 1122
{: #error-1122}

An error occurred in the readiness check, try again or contact support.	

## Error 1123
{: #error-1123}

The vSRX console has an active session in edit mode. Exit the console session and retry.	

## Error 1124
{: #error-1124}

The gateway experienced a precheck setup failure due to a Juniper incompatibility change in version 18.4. Specify a vlan-id for each interface configured with vlan-tagging. Refer to [Correcting error 1124](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1124) for more information.

## Error 1125
{: #error-1125}

The gateway experienced a precheck setup failure due to a Juniper incompatibility change in the version 18.4 syslog settings. Refer to [Correcting error 1125](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1125) for more information.

## Error 1126
{: #error-1126}

The gateway control link is down. Ensure vnet0 and vnet1 are configured on the Ubuntu host and retry.

## Error 1127
{: #error-1127}

The Ubuntu host is missing an ethernet interface in bond0. Ensure bond0 includes the 2 private ethernet interfaces.

## Error 1128
{: #error-1128}

The Ubuntu host is missing an ethernet interface in bond1. Ensure bond1 includes the 2 public ethernet interfaces.

## Error 1129
{: #error-1129}

The Ubuntu host has an extra ethernet interface in bond0. Ensure bond0 only includes the 2 private ethernet interfaces.

## Error 1130
{: #error-1130}

The Ubuntu host has an extra ethernet interface in bond1. Ensure bond1 only includes the 2 public ethernet interfaces.

## Error 1131
{: #error-1131}

The vSRX configuration is using a hidden cli command not compatible with the automation. Remove and replace the `address-range` command syntax and retry.

## Error 1132
{: #error-1132}

The Ubuntu host has a kvm xml configuration that is missing the default telnet configuration used for console access. Add this configuration back and retry.

## Error 1133
{: #error-1133}

The vSRX console connection via telnet timed out executing commands. Please rerun or contact support.

## Error 1134
{: #error-1134}

The node being OS reloaded cannot access the other node in the cluster. Ensure the other node is active and retry. If both nodes are unrecoverable contact support to run Rebuild Cluster.

## Error 1135
{: #error-1135}

The vSRX license file cannot be found. Please rerun or contact support.

## Error 1136
{: #error-1136}

The vSRX license file is found, but the contents are empty. Please rerun or contact support.

## Error 1137
{: #error-1137}

The vSRX license file cannot be read. Please rerun or contact support.

## Error 1138
{: #error-1138}

The vSRX license install has failed during the vSRX license configuration. Please rerun or contact support.

## Error 1139
{: #error-1139}

The vSRX configuration includes a `tcp-mss` setting on an interface. Remove the invalid configuration and rerun.

## Error 1140
{: #error-1140}

The vSRX configuration includes an unsupported configuration setting. Correct and/or remove the unsupported configuration setting and rerun. Refer to [Correcting Unsupported vSRX Configuration Commands](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-unsupported-configuration) for more information.

## Error 1141
{: #error-1141}

The vSRX was accessible but we were unable to determine which node is the primary.

## Error 1142
{: #error-1142}

The vSRX includes duplicate IPs in the interface section of the vSRX config. Remove the duplicate IPs from the config and rerun.

## Error 1143
{: #error-1143}

The gateway upgrade process failed with an unexpected exception. Contact IBM Support.

## Error 1145
{: #error-1145}

The vSRX license does not support IDP, but IDP policies and configurations were detected on the running vSRX. Remove the policies and configurations or install a vSRX license with IDP support such as the Content Security Bundle (CSB) and retry the operation.

## Error 1146
{: #error-1146}

The Ubuntu server's network switch does not support multicast, which is required by the gateway configuration. Contact IBM Support.

## Error 1147
{: #error-1147}

The vSRX configuration includes a url-pattern with invalid characters. Remove the invalid characters and retry. Refer to [Correcting error 1147](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1147) for more information.

## Warning 1176
{: #warning-1176}

The gateway experienced a precheck setup warning. A VPN establishment configuration with `non-immediate` was detected, which could increase the time it takes for VPN establishment after the vSRX starts. Refer to [Correcting warning 1176](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1176) for more information.

## Warning 1177
{: #warning-1177}

The gateway experienced a precheck setup warning. A security policy using `dynamic-application any` was detected, which can result in packet loss. This can also cause VPN tunnel communication to fail. Refer to [Correcting warning 1177](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1177) for more information.

## Warning 1178
{: #warning-1178}

The license was updated. However, validation of the new license failed. It is recommended you manually check that the vSRX license is applied to each vSRX node.

## Warning 1179
{: #warning-1179}

The vSRX version found to be running on the Gateway is unsupported. Operations such as OS Reload and Rebuild Cluster will overwrite the current unsupported vSRX version with the version currently listed on the Gateway Details page. Refer to [Correcting warning 1179](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1179) for more information.

## Warning 1180
{: #warning-1180}

The vSRX license found on the Gateway is unsupported. [Correcting warning 1180](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1180) for more information.

## Warning 1181
{: #warning-1181}

The vSRX license and version on the Gateway are both found to be unsupported. [Correcting warning 1181](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1181) for more information.
