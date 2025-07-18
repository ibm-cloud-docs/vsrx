---

copyright:
  years: 2017, 2025
lastupdated: "2025-07-17"

keywords: checking, readiness, errors

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Understanding readiness errors and warnings
{: #readiness-errors}

Readiness check warnings and errors can occur for any of the three readiness checks: OS reload, license upgrade, or version upgrade. The following list provides information on these error and warning codes.

## Error 1000
{: #error-1000}

An OS reload is already running on a different node in the HA cluster. The other node's OS reload must be completed before you run a second OS reload.

## Error 1002
{: #error-1002}

An error occurred in the connectivity check. Contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1003
{: #error-1003}

The root user for the host is not found.

## Error 1004
{: #error-1004}

The root user credentials for the host are not found.

## Error 1005
{: #error-1005}

The host SSH console connection was not created. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1007
{: #error-1007}

The host SSH console connection was not created. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1008
{: #error-1008}

The host SSH console cannot process the command. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1009
{: #error-1009}

The host has an invalid IP address, or is blocked by a firewall. SSH failed. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1011
{: #error-1011}

The root user's credentials for the gateway were not found.

## Error 1012
{: #error-1012}

The gateway SSH console connection failed. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1013
{: #error-1013}

The root user for the gateway was not found.

## Error 1014
{: #error-1014}

The gateway readiness check timed out.

## Error 1017
{: #error-1017}

The gateway SSH console connection was not created. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1018
{: #error-1018}

The gateway SSH console could not process the command. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1019
{: #error-1019}

The gateway has an invalid IP address, or is blocked by a firewall. SSH failed. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1021
{: #error-1021}

An error occurred in the connectivity check. Contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1022
{: #error-1022}

The gateway readiness precheck failed with an unexpected exception. Try again or contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1023
{: #error-1023}

The gateway readiness precheck failed the DNS accessibility check on the Ubuntu host. Confirm that a network access to the private `10.0.0.0/8` subnet from the host exists.

## Error 1024
{: #error-1024}

The gateway readiness precheck failed with an unexpected exception. Try again or contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1025
{: #error-1025}

The IPMI interface is disabled for the Gateway host. Check IPMI status and enable the interface if it is disabled. Try again or contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1026
{: #error-1026}

The Ubuntu host is unable to write to the attached storage as it is read only. Reboot the host and try again or contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1101
{: #error-1101}

An error occurred during the readiness check. Try again or contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1102
{: #error-1102}

The host experienced a precheck setup failure. Try again or contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1103
{: #error-1103}

The host experienced a precheck setup failure. Try again or contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1104
{: #error-1104}

The host experienced a precheck setup failure. Try again or contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1105
{: #error-1105}

The host experienced a precheck setup failure and cannot SSH to the gateway. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1106
{: #error-1106}

The host experienced a precheck setup failure and cannot SSH to the private IP for the other node's host. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1107
{: #error-1107}

The host experienced a precheck setup failure due to an invalid password. Correct the password and try again. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1108
{: #error-1108}

The gateway experienced a precheck setup failure due to an invalid password. Correct the password and try again. See [Correcting connectivity errors](/docs/vsrx?topic=vsrx-correcting-readiness-errors) for information on how to resolve SSH connectivity check errors.

## Error 1109
{: #error-1109}

The gateway experienced a precheck setup failure, and is unable to check the vSRX disk capacity. Remove any unnecessary files from `/var` and try again.

## Error 1110
{: #error-1110}

The gateway experienced a precheck setup failure because the vSRX file-system-reached capacity. Remove any unnecessary files from `/var` and try again.

## Error 1111
{: #error-1111}

The gateway experienced a precheck setup failure due to a general failure in the JunOS RPC call. Try again or contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1112
{: #error-1112}

The gateway experienced a precheck setup failure due to a cluster error. Ensure redundancy group 0 is online and has no monitor-failures.

## Error 1113
{: #error-1113}

The host experienced a precheck setup failure and is unable to determine the status of the host VM by using `virsh`. Try again or contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help).

## Error 1114
{: #error-1114}

The host has a precheck setup failure because insufficient memory is installed on the bare-metal server. A minimum of 32 GB is required. Contact [IBM Support](/docs/vsrx?topic=vsrx-getting-help) to install the required amount of memory.

## Error 1115
{: #error-1115}

The gateway has a precheck setup failure due to an incompatible SSH connection limit in the vSRX configuration. Remove the SSH connection limit from the vSRX configuration and retry.

## Error 1116
{: #error-1116}

The host has a precheck setup failure. Ubuntu is missing the telnet software package. Install telnet and retry.

## Error 1117
{: #error-1117}

The host's Ubuntu mirror server is not accessible. Retry the operation when the mirror is accessible.

## Error 1118
{: #error-1118}

The vSRX node is not started. Start the vSRX VM and retry the operation.

## Error 1119
{: #error-1119}

The vSRX node's VM is running but the node is not accessible from telnet. Exit from all console (telnet) sessions and retry the operation. Alternatively, see [Correcting error 1119](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1119) for more information.

## Error 1120
{: #error-1120}

The vSRX node does not have a valid license. Remove any evaluation licenses and apply for a valid license. Then, retry the operation. See [Known limitations for IBM Cloud Juniper vSRX](/docs/vsrx?topic=vsrx-known-limitations-for-ibm-cloud-juniper-vsrx) for more information on identifying and removing the evaluation license.

## Error 1121
{: #error-1121}

License operations against vSRX v15.1 are not supported. Upgrade to a newer version of the vSRX.

## Error 1122
{: #error-1122}

An error occurred in the readiness check, try again or contact IBM support.

## Error 1123
{: #error-1123}

The vSRX console has an active session in edit mode. Exit the console session and retry.

## Error 1124
{: #error-1124}

The gateway experienced a precheck setup failure due to a Juniper incompatibility change in version 18.4. Specify a vlan-id for each interface configured with vlan-tagging. See [Correcting error 1124](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1124) for more information.

## Error 1125
{: #error-1125}

The gateway experienced a precheck setup failure due to a Juniper incompatibility change in the version 18.4 syslog settings. See [Correcting error 1125](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1125) for more information.

## Error 1126
{: #error-1126}

The gateway control link is down. Ensure vnet0 and vnet1 are configured on the Ubuntu host and retry.

## Error 1127
{: #error-1127}

The Ubuntu host is missing an Ethernet interface in bond0. Ensure bond0 includes the 2 private Ethernet interfaces.

## Error 1128
{: #error-1128}

The Ubuntu host is missing an Ethernet interface in bond1. Ensure bond1 includes the 2 public Ethernet interfaces.

## Error 1129
{: #error-1129}

The Ubuntu host has an extra Ethernet interface in bond0. Ensure bond0 includes only the 2 private Ethernet interfaces.

## Error 1130
{: #error-1130}

The Ubuntu host has an extra Ethernet interface in bond1. Ensure bond1 includes only the 2 public Ethernet interfaces.

## Error 1131
{: #error-1131}

The vSRX configuration is using a hidden cli command not compatible with the automation. Remove and replace the `address-range` command syntax and retry.

## Error 1132
{: #error-1132}

The Ubuntu host has a kvm xml configuration that is missing the default telnet configuration that is used for console access. Add this configuration back and retry.

## Error 1133
{: #error-1133}

The vSRX console connection by using telnet timed out when running the commands. Rerun or contact IBM Support.

## Error 1134
{: #error-1134}

The node, which is OS reloaded, cannot access the other node in the cluster. Ensure that the other node is active and retry. If both nodes are unrecoverable contact IBM support to run Rebuild Cluster.

## Error 1135
{: #error-1135}

The vSRX license file cannot be found. Rerun or contact IBM Support.

## Error 1136
{: #error-1136}

The vSRX license file is found, but the contents are empty. Rerun or contact IBM support.

## Error 1137
{: #error-1137}

The vSRX license file cannot be read. Rerun or contact IBM support.

## Error 1138
{: #error-1138}

The vSRX license installation failed during the vSRX license configuration. Rerun or contact IBM support.

## Error 1139
{: #error-1139}

The vSRX configuration includes a `tcp-mss` setting on an interface. Remove the invalid configuration and rerun.

## Error 1140
{: #error-1140}

The vSRX configuration includes an unsupported configuration setting. Correct or remove the unsupported configuration setting and rerun. See [Correcting Unsupported vSRX Configuration Commands](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-unsupported-configuration) for more information.

## Error 1141
{: #error-1141}

The vSRX was accessible but we were unable to determine which node is the primary.

## Error 1142
{: #error-1142}

The vSRX includes duplicate IPs in the interface section of the vSRX config. Remove the duplicate IPs from the config and rerun.

## Error 1143
{: #error-1143}

The gateway upgrade process failed with an unexpected exception. Contact IBM Support.

## Error 1144
{: #error-1144}

The vSRX add-on license files are not equal to the expected license count. Contact IBM Support.

## Error 1145
{: #error-1145}

The vSRX license does not support IDP, but IDP policies and configurations were detected on the running vSRX. Remove the policies and configurations or install a vSRX license with IDP support such as the Content Security Bundle (CSB) and retry the operation. For details on configuration removal, see [Correcting error 1145](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1145) for more information.

## Error 1146
{: #error-1146}

The Ubuntu server's network switch does not support multicast, which is required by the gateway configuration. Contact IBM Support.

## Error 1147
{: #error-1147}

The vSRX configuration includes a url-pattern with invalid characters. Remove the invalid characters and retry. See [Correcting error 1147](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1147) for more information.

## Error 1154
{: #error-1154}

Both vSRX cluster nodes are down. Start the vSRX nodes and retry.

## Error 1155
{: #error-1155}

The vSRX configuration cannot specify both a `service` and an `any-service` within the same `security-zone interface` stanza. Correct this configuration and retry.

## Error 1157
{: #error-1157}

vSRX SSL certificates that are included in stanzas, such as `set services ssl initiation`, `set services ssl termination`, and `set services ssl proxy` cannot be migrated to the newly upgraded vSRX node. Remove these certificates from the vSRX configuration, retry, and re-import the certs after upgrade.

## Error 1158
{: #error-1158}

The vSRX security NAT configuration includes an invalid network address range. Specify a valid network IP range by using CIDR notation and retry.

## Error 1159
{: #error-1159}

The vSRX configuration includes a reference to an SSL certificate in the `system services rest https` config. Certs cannot be migrated during an upgrade. Deactivate the reference that uses `deactivate system services rest https`, retry, and reactivate and re-import the certificate after the upgrade completes.

## Error 1160
{: #error-1160}

The vSRX configuration includes a `security idp sensor-configuration packet-log total-memory` reference. This causes issues during an upgrade. Remove the reference and retry.

## Error 1163
{: #error-1163}

If the vSRX configuration includes a **Weak cipher**, the Upgrade pre-check fails with the error 1163. To fix this error, remove or deactivate the weak cipher configuration and retry.

## Error 1165
{: #error-1165}

The vSRX configuration contains a Juniper security policy with keywords dynamic-application any and junos-defaults. Remove the policy or replace junos-defaults with any.

## Error 1167
{: #error-1167}

The vSRX configuration contains a Juniper `security ike` but does not specify a corresponding `external-interface`. Modify the configuration and retry.

## Error 1168
{: #error-1168}

The Ubuntu server is running in rescue mode. Exit rescue mode and retry.

## Error 1169
{: #error-1169}

The vSRX configuration contains a security policy that checks the match of unsupported `dynamic-application junos:ICMP-TRACEROUTE`. Remove the policy line that contains `junos:ICMP-TRACEROUTE`.

## Warning 1176
{: #warning-1176}

The gateway experienced a precheck setup warning. A VPN establishment configuration with `non-immediate` was detected, which might increase the time that it takes for VPN establishment after the vSRX starts. See [Correcting warning 1176](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1176) for more information.

## Warning 1177
{: #warning-1177}

The gateway experienced a precheck setup warning. A security policy that uses `dynamic-application any` is detected, which can result in packet loss. This issue can also cause VPN tunnel communication to fail. See [Correcting warning 1177](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1177) for more information.

## Warning 1178
{: #warning-1178}

The license was updated. However, validation of the new license failed. It is recommended you manually check that the vSRX license is applied to each vSRX node.

## Warning 1179
{: #warning-1179}

The vSRX version found to be running on the Gateway is unsupported. Operations such as OS Reload and Rebuild Cluster overwrites the current unsupported vSRX version with the version that is currently listed on the Gateway Details page. See [Correcting warning 1179](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1179) for more information.

## Warning 1180
{: #warning-1180}

The vSRX license that is found on the Gateway is unsupported. [Correcting warning 1180](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1180) for more information.

## Warning 1181
{: #warning-1181}

The vSRX license and version on the Gateway are both found to be unsupported. [Correcting warning 1181](/docs/vsrx?topic=vsrx-correcting-readiness-errors#correcting-1181) for more information.

## Warning 1182
{: #warning-1182}

The vSRX add-on license files are not found. Contact IBM Support.

## Warning 1183
{: #warning-1183}

The vSRX add-on license count is not found in the import settings. Contact IBM Support.

## Warning 1184
{: #warning-1184}

A connection timeout error occurred when checking the installed licenses. Contact IBM Support.

## Warning 1185
{: #warning-1185}

The gateway does not have a valid license because the license for the version might have expired. Upgrade to the version, `21.3R2-S1` or newer. Contact IBM Support.
