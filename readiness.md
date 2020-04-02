---

copyright:
  years: 2018
lastupdated: "2020-04-01"

keywords: checking, readiness

subcollection: vsrx

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank_"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:download: .download}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Checking vSRX readiness
{: #vsrx-readiness}

A readiness check verifies the ability of your {{site.data.keyword.vsrx_full}} to perform certain gateway actions. They include:

* OS reloads
* License upgrades
* Version upgrades

Once you run the readiness check, errors will alert you to any necessary actions you should take before beginning one of these actions, or inform you that you're ready to proceed.

To run a readiness check, perform the following procedure:

1. From your browser, open [https://cloud.ibm.com ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com){:new_window} and log into your account.
2. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the top left, then click **Classic Infrastructure**.
3. Choose **Network > Gateway Appliances**.
4. Click the name of the vSRX you want to run a readiness check on.
5. Find the Readiness Check module on the vSRX details page.

  ![Readiness check module](images/readiness_module.png "Readiness check module")

6. Click the **Run check** button.
7. Select one of the three actions you would like to check for readiness, then select **Run check**.
8. The details page for your vSRX displays again, as do the test results in the readiness check module.

 Ensure the status for any action you wish to perform is Ready before beginning that action.
 {: important}

The following section provides details on the various readiness status conditions your check may return.

## Readiness status
{: #readiness-status}

There are seven unique status conditions for the readiness check that you may encounter.

### Unchecked
{: #status-unchecked}

A readiness check has not yet been run for this action.

### Expired
{: #status-expired}

The readiness check has not run recently enough to reflect accurate results. Run a new check to see the current status.

### Ready
{: #status-ready}

Your vSRX is ready to perform the given action.

### Not Ready
{: #status-not-ready}

Your vSRX is not ready to perform the action in question. This could occur because of several reasons. Either a readiness check error occurred, or the readiness check did not complete fast enough, and timed out.

Error messages for the issues found during the readiness check display next to the module. Click on the error codes to get more information on each error. Alternatively, you can find information about each error in the topic [Understanding readiness errors](/docs/vsrx?topic=vsrx-readiness-errors).

### Running
{: #status-running}

The readiness check is currently running on your vSRX, and has not currently encountered any errors.

### Incomplete
{: #status-incomplete}

The first member of the gateway's highly available (HA) setup failed the readiness check. As a result, the gateway could not complete the readiness check.

### Unsupported
{: #status-unsupported}

The action you are attempting to check is not supported for this gateway.

### Current
{: #status-current}

The action you are attempting to check does not need to be performed, as the gateway already has the latest version available.
