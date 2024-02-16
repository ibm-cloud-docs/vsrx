---

copyright:
  years: 2018, 2020
lastupdated: "2020-04-01"

keywords: checking, readiness

subcollection: vsrx

---

{{site.data.keyword.attribute-definition-list}}

# Checking vSRX readiness
{: #vsrx-readiness}

A readiness check verifies the ability of your {{site.data.keyword.vsrx_full}} to perform certain gateway actions. They include:

* OS reloads
* License upgrades
* Version upgrades

After you run the readiness check, errors alert you to any necessary actions that you should take before you begin one of these actions, or inform you that you're ready to proceed.

To run a readiness check, perform the following procedure:

1. From your browser, open the [IBM Cloud console](/login){: external} and log in to your account.
2. Select the Menu icon ![Menu icon](../../icons/icon_hamburger.svg) from the upper left, then click **Classic Infrastructure**.
3. Choose **Network > Gateway Appliances**.
4. Click the name of the vSRX you want to run a readiness check on.
5. Find the Readiness Check module on the vSRX details page.
6. Click **Run check**.
7. Select one of the three actions that you want to check for readiness, then select **Run check**.
8. The details page for your vSRX displays again, as do the test results in the readiness check module.

   Ensure the status for any action that you want to perform is Ready before you begin that action.
   {: important}

The following section provides details on the various readiness status conditions that your check might return.

## Readiness status
{: #readiness-status}

There are seven unique status conditions for the readiness check that you might encounter.

### Unchecked
{: #status-unchecked}

A readiness check has not yet been run for this action.

### Expired
{: #status-expired}

The readiness check has not run recently enough to reflect accurate results. Run a new check to see the status. Readiness checks expire 5 hours after they complete.

### Ready
{: #status-ready}

Your vSRX is ready to perform an action.

### Not Ready
{: #status-not-ready}

Your vSRX is not ready to perform the action in question. This might occur because of several reasons. Either a readiness check error occurred, or the readiness check did not complete fast enough, and timed out.

Error messages for the issues that are found during the readiness check display next to the module. Click the error codes to get more information on each error. Alternatively, you can find information about each error in the topic [Understanding readiness errors](/docs/vsrx?topic=vsrx-readiness-errors).

### Running
{: #status-running}

The readiness check is running on your vSRX, and did not encounter any errors.

### Incomplete
{: #status-incomplete}

The first member of the gateway's highly available (HA) setup failed the readiness check. As a result, the gateway might not complete the readiness check.

### Unsupported
{: #status-unsupported}

The action that you are attempting to check is not supported for this gateway.

### Current
{: #status-current}

The action that you are attempting to check does not need to be performed, as the gateway already has the latest version available.
