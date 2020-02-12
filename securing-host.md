---

copyright:
  years: 2018
lastupdated: "2019-11-15"

keywords: secure, securing, host, os, ubuntu, ufw, iptables, firewal, vsrx, juniper

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:note: .note}
{:important: .important}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Securing the Host Operating System
{: #securing-host-operating-system}
{: help}
{: support}

The {{site.data.keyword.vsrx_full}} runs as a Virtual Machine on a bare-metal server installed with Ubuntu and KVM. To secure the host OS, you should ensure that no other critical services are hosted on the same OS.
{: shortdesc}

## SSH Access
{: #securing-host-ssh}

The {{site.data.keyword.vsrx_full}} can be deployed with public and private network access or private network access only. By default, password based SSH access to the public IP of the host OS will be disabled on new provisions and OS reloads. Access to the host can be achieved through the private IP address. Alternatively, key based authentication can be used to access the public IP. To do so, specify the public SSH key when placing a new Gateway order . 

Some existing deployments of the {{site.data.keyword.vsrx_full}} may allow password based SSH access to the public IP of the host OS. For these deployments, you can manually disable password based SSH access to the public IP of the OS by following these steps:

1. Modify /etc/ssh/sshd_config 

  * Ensure the following values are set. 
  
  ```
  ChallengeResponseAuthentication no
  PasswordAuthentication no
  ```
  
  * Add the following filter rules to the end of the file.
  
  ```
  Match Address 10.0.0.0/8 
      Password Authentication yes
  ```
  
2. Restart the SSH service using the command `/usr/sbin/service ssh restart`. 

The procedure above ensures addresses in the private infrastructure network `10.0.0.0/8` subnet are allowed SSH access. This access is needed for actions such as:

  * OS reloads
  * Cluster rebuilding
  * Version upgrades
  {: note}

## Firewalls
{: #securing-host-firewall}

Implementing an Ubuntu firewall (UFW, Iptables, and so on) without required rules can cause the {{site.data.keyword.vsrx}} HA cluster to be disabled. The vSRX solution depends on heartbeat communication between the primary and secondary nodes. If the firewall rules do not allow communication between the nodes, then cluster communication will be lost.
{: important}

For {{site.data.keyword.vsrx}} version 18.4 and later, the following rules are used to allow cluster communication for UFW:

- To allow protocol 47 (used for heartbeat communication) in `/etc/ufw/before.rules`:

  ```
  -A ufw-before-input -p 47 -j ACCEPT
  ```

- To allow private network communication:

  ```
  ufw allow in from 10.0.0.0/8 to 10.0.0.0/8
  ```

- To enable UFW:

  ```
  ufw enable
  ```

For {{site.data.keyword.vsrx}} versions prior to 18.4, the rules must also allow for multicast communication.

In some cases, troubleshooting operations may require disabling the firewall for access to public repositories. In these cases, you should work with IBM Support to understand how to proceed.
{: note}

Most Gateway actions require SSH access to the private `10.0.0.0/8` subnet for the host OS and the {{site.data.keyword.vsrx}}. Blocking this access with a firewall can cause the following actions to fail:

- OS reloads
- Cluster rebuilding
- Version upgrades

As a result, if SSH access is disabled for the `10.0.0.0/8` subnet, you must re-enable it prior to executing any of these actions.
