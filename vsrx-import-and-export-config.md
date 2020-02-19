---

copyright:
  years: 2019
lastupdated: "2019-11-14"

keywords: understanding, default, configuration, standalone, ha

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

# Importing and and exporting a vSRX Configuration
{: #importing-exporting-vsrx-configuration}

The {{site.data.keyword.vsrx_full}} upgrade process preserves the original configuration of the vSRX throughout the entire process, as long as the required reloads are done one at a time. However, it is still strongly recommended to export and backup your vSRX configuration settings before starting the upgrade.
{: shortdesc}

After the upgrade process completes for Stand Alone servers, you should import the original configuration you have saved if you want to restore it. For High Availability configurations, you should restore the configuration manually from your exported file only if the upgrade fails.

## Considerations
{: #considerations}

* The upgrade process for Standalone and High Availability (HA) are different. Details can be found [here](/docs/vsrx?topic=vsrx-upgrading-the-vsrx).
* The J-web interface allows you to display, edit, and upload the current configuration quickly and easily without using the Junos OS CLI. Reference the [Juniper J-Web User Guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.juniper.net/documentation/en_US/junos/topics/concept/J-web-overview.html){:new_window} for more details.
* An upgrade from the vSRX 15.x 10G to the vSRX 18.x 10G offering results in changes to the vSRX interface mappings in the configuration file. As a result, when importing your original vSRX settings, make sure that the new “interfaces” section is not modified. There are two ways of doing this. Either import sub-sections other than the “interfaces” section, or import the entire configuration and manually restore the 18.x SR-IOV interfaces.

The new vSRX default interface configuration for both the Linux Bridge and SR-IOV must be preserved after the import of their configurations. For example, for SR-IOV the GE interfaces have specific mappings to the host that must be preserved to enable SR-IOV. These interfaces are found in the CLI using the command `show configuration interfaces`. Reference [vSRX default configuration](/docs/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration) for more information on SR-IOV mappings.
{: important}

If you prefer using the Junos OS CLI, the following contents provide different methods to export and import your configuration settings, depending on whether you want to export or import the entire configuration or just part of it. To manage the configuration settings, enter CLI mode, then run the command `configure` to enter configuration mode. Then to commit your changes, run the command `commit`.

## Exporting the entire vSRX configuration
{: #export-the-whole-vsrx-configuration}

To export the entire vSRX configuration:

1. First, run the command `save /var/tmp/XXX.txt` to save the entire configuration into `/var/tmp`. You can name the text file whatever you wish. The output should be similar to the following:

  ```
  Wrote 273 lines of configuration to '/var/tmp/SA15DefaultConfig.txt'  

  [edit]
  ```

2. Copy and save the text file into your local workspace for later use.

## Exporting part of the vSRX configuration
{: #export-part-of-the-vsrx-configuration}

To export only part of the vSRX configuration:

1. Ensure that you are at the top of the configuration tree by running `top` under the configuration mode.

2. Then run the command `show <section>` to get the current configuration, enclosed in braces.

  For example, you can run `show interfaces` to show all the interfaces configuration. Or, if you prefer to display the output in set mode, run the command `show <section> | display set`.

  The output should be similar to the following:
  ```
  # show interfaces | display set
  set interfaces ge-0/0/0 description PRIVATE_VLANs
  set interfaces ge-0/0/0 flexible-vlan-tagging
  set interfaces ge-0/0/0 native-vlan-id 925
  set interfaces ge-0/0/0 mtu 9000
  ...

  [edit]
  ```

  Set mode displays the configuration as a series of configuration mode commands required to re-create the configuration. This is useful if you are not familiar with how to use configuration mode commands or if you want to cut, paste, and edit the displayed configuration.
  {: tip}

3. Copy and save the output into your local workspace for later use.

## Importing the entire vSRX configuration
{: #import-the-whole-vsrx-configuration}

The new vSRX default interface configuration for both the Linux Bridge and SR-IOV must be preserved after the import of their configurations. For example, for SR-IOV the GE interfaces have specific mappings to the host that must be preserved to enable SR-IOV. These interfaces are found in the CLI using the command `show configuration interfaces`. Reference [vSRX default configuration](/docs/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration) for more information on SR-IOV mappings.
{: important}

To import the entire vSRX configuration:

1. After upgrading the vSRX, copy the config file you saved earlier back to the `/var/tmp` folder.
2. Run `load override /var/tmp/XXX.txt` under the configuration mode to replace the entire current configuration with the content that you saved under the `/var/tmp` folder.

## Importing part of the vSRX configuration
{: #import-part-of-the-vsrx-configuration}

The new vSRX default interface configuration for both the Linux Bridge and SR-IOV must be preserved after the import of their configurations. For example, for SR-IOV the GE interfaces have specific mappings to the host that must be preserved to enable SR-IOV. These interfaces are found in the CLI using the command `show configuration interfaces`. Reference [vSRX default configuration](/docs/vsrx?topic=vsrx-understanding-the-vsrx-default-configuration) for more information on SR-IOV mappings.
{: important}

To import only part of the vSRX configuration:

1. From the configuration mode, run `edit <section>` to go to the configuration tree level that you want.
2. Copy the configuration settings you have saved and run the command `load merge terminal relative` to merge the configuration with the current one.
3. Paste the content, hit Enter to go to a new line, then type Control + D to end the input.

  The output should be similar to the following:

  ```
  # load merge terminal relative
  [Type ^D at a new line to end input]
  family inet {
              filter {
                  input PROTECT-IN;
              }
          }
  load complete

  [edit interfaces lo0 unit 0]
  ```

Alternatively, you can also:

* Replace the configuration instead of merging it, by deleting the configuration first with the command `delete` under this configuration tree level and then performing a `load merge terminal relative` to copy and paste your previous configuration. 
* Edit the configuration in set mode, by running `load set terminal` instead of `load merge terminal relative`. Then copy and paste the content you saved in set mode.

  Ensure that you always run `load set terminal` at the top.
  {: note}
