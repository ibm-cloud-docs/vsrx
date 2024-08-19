---

copyright:
  years: 2017, 2024
lastupdated: "2024-08-19"

keywords: vsrx, access

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Accessing your IBM Cloud Juniper vSRX
{: #vsrx-accessing}

The public interfaces of the Ubuntu hypervisor and the vSRX do not allow SSH access. Additionally, the vSRX web management console is disabled by default. You can use several different approaches to access these devices.
{: shortdesc}

## Private Interfaces
{: #vsrx-private-interfaces}

The vSRX Gateway Overview page provides details on the private interfaces of the Ubuntu hypervisor (found in the Hardware pane, under Private IP) and the vSRX (found in the vSRX pane, under Private IP). By default, SSH, Ping (ICMP), and the vSRX web management interface (8443) are enabled on these interfaces. To access these interfaces you must have network connectivity to the private network. 

The following sections detail ways you can gain access.

## Accessing private interfaces with a VPN
{: #vsrx-vpn-private-interfaces}

IBM Cloud Classic supports Virtual Private Networking (VPN) access to the private network. This can be used to access the private interfaces of the host and the vSRX. For more information, refer to [Getting started with IBM Cloud Virtual Private Networking](/docs/iaas-vpn?topic=iaas-vpn-getting-started). Throughput on this shared VPN solution is limited to 1Mbps and is not recommended for large file transfers. This is the most widely used and simplest method for accessing the IBM Cloud Classic private network.

If the shared customer VPN solution does not meet your requirements, you can also build Remote Access VPNs using [Juniper Secure Connect](https://cloud.ibm.com/media/docs/downloads/vSRX/IBM-Cloud-Secure-Connect.pdf) on the vSRX itself. There are also similar solutions through other gateway appliances in your IBM Cloud account, as one of the primary functions of a firewall is to deploy VPN solutions for secure access. Additionally, can build and manage a classic Baremetal or VSI installed with OpenVPN, WireGuard, or other VPN software. This provides an encrypted public access point into the IBM Cloud Classic private network. These options require [private secondary subnets](/docs/subnets?topic=subnets-about-subnets-and-ips#static-subnets) as the address pools. 

The process for building a VPN using a standard server is not currently documented.
{: note}

## Accessing the private interfaces with a bastion (jump) host
{: #vsrx-bastion-host}

IBM Cloud Classic accounts are generally VRF enabled. If your account is not enabled, ensure VLAN spanning is enabled. If not, refer to [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint&interface=ui) to do so. VLAN spanning and VRF are two specific configurations for account level routing that allow private VLAN intercommunication.

Once you enable VLAN spanning or VRF, IBM Cloud resources (such as virtual servers) can connect to one another through their private network connectivity over different private subnets, private VLANs, across pods, and across different datacenters. A VSI or baremetal server with a public facing interface can provide a bridge to the private network, as well as access to the private interfaces of the gateway. You can use these servers as a direct jumphost for connecting to the server on the public interface. You can then access your FortiGate through SSH or HTTPS , or configure a SOCKS proxy in SSH to the server. This allows you to configure the SOCKS proxy connection in your browser so that your browser can connect to the Web GUI of your vSRX through the proxy connection.

## Using the Ubuntu hosts local console
{: #vsrx-ubuntu-console}

The vSRX runs as a Virtual Machine (VM) on the bare-metal Ubuntu host. You can access the VM using the local console of the Ubuntu host. This requires access to the Ubuntu host, which, by default, has SSH enabled only on the private network. 

To access the VM using the local console of the Ubuntu host:

1) Find the VM Name or ID: 

   `virsh list --all`.
   
1) Use the ID to dump the configuration in XML format and search for the console port: 

   `virsh dumpxml <id> | grep service`

   For example:

   ```
   :~# virsh dumpxml 2 | grep service
      <source mode='bind' host='127.0.0.1' service='8624' tls='no'/>
      <source mode='bind' host='127.0.0.1' service='8624' tls='no'/>  
   ```
   {: pre}
   
   You can also use `ss -tulip | grep qemu` to find the serial port number.
  
1) Use telnet and the port number (from the example) to access the VM:

   `telnet localhost 8624`
  
## Enable j-web on public and private interfaces
{: #vsrx-enable-public}

While it is recommended to keep your default settings so as to disable the public interfaces, it is possible to re-enable them if needed. The vSRX web management interface can be enabled on public and private interfaces by activating web-management. 

Web-management is deactivated by default starting in Junos version 23.2R2-S2:
{: tip}

```sh
configure
activate system services web-management
commit
```
{: codeblock}

To lock J-web after activating it, set the web-management HTTPS interface as the private interface only. You can also customize the PROTECT-IN filter on loopback to only allow access from specific source IP addresses. To revert to the default of the completely deactivated J-web, you can run: 

`deactivate system services web-management`

When executing destructive actions, such as "Rebuild Cluster" (vSRX Only) and "Force Rebuild" (Ubuntu and vSRX), the defaults will be re-enabled as the systems are reset to defaults.
{: note}
