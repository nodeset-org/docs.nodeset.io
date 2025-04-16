# Node Operator Guide

Although it is technically possible to run a StakeWise node alongside an existing Ethereum node, we recommend using a completely isolated system, and this guide assumes this is the case.

{% hint style="info" %}
There are technical limitations which make it very difficult to run a fully custom node environment for NodeSet's StakeWise integration. Therefore, you must use [the Hyperdrive client](https://github.com/nodeset-org/hyperdrive) to connect appropriately to NodeSet's web services.
{% endhint %}

***

## **Installation**

### **1. Plan your node operation**

[See this page on planning your node operation.](../../node-operators/best-practices/planning-your-node-architecture.md)

### 2. Install Hyperdrive

[See this page for more information on setting up Hyperdrive](https://docs.nodeset.io/node-operators/hyperdrive). Remember to enable support for StakeWise during the setup process!

### **3. Fund your node wallet**

{% hint style="info" %}
You must send ETH to your node wallet so that Hyperdrive can submit deposit transactions for your validators. This is an important mechanism in StakeWise to prevent griefing attacks ([see here for more information](https://docs.nodeset.io/stakewise-integration/faq#why-do-node-operators-need-to-pay-to-register-validators)).
{% endhint %}

We recommend **at least** 0.01 ETH for each validator key you generate. For example, if you generate 5 keys, you should fund your node wallet with **at least** 0.05 ETH.

For Hoodi, you can use a faucet. NodeSet has not verified these faucets. Use them at your own risk!

* [https://hoodi-faucet.pk910.de/](https://hoodi-faucet.pk910.de/)

### 4. Add your node address to your NodeSet account

a) Go to [https://nodeset.io/dashboard](https://nodeset.io/dashboard) to create or login to your NodeSet account. Users who have gone through the on-boarding process will automatically be given the permission to access the StakeWise portion of the dashboard.

b) Use the dashboard to [add your new node address](../../nodeset-dashboard/authorizing-your-node.md).

### 5. Generate validator keys

```bash
hyperdrive stakewise wallet generate-keys 
```

This command will generate new validator keys, upload them to NodeSet so we can refer them to the StakeWise vault, and add them to your validator client and sw\_operator containers.

After this finishes, the status command should show your new validator public keys:

```bash
hyperdrive stakewise status
```

Additionally, you should see those validator keys in the NodeSet dashboard at [https://nodeset.io/dashboard/stakewise/validators](https://nodeset.io/dashboard/stakewise/validators).

### 6. Backup your node wallet mnemonic and/or private key

Ensure you store your secrets safely and regularly test your access procedures. We recommend two copies in offline cold storage, each in different locations.

### 7. Maintain your node

Once NodeSet registers your node, ETH may be automatically deposited into your validators at any time.

As always, you should [use the same best practices for maintaining your operation](../../node-operators/best-practices/).

{% hint style="warning" %}
Be careful! Even if there are no validators activated when your node goes down, Ethereum never goes down, so deposits might be made to those validators even while the node is offline. If this happens, those validators will be penalized, and you may eventually be ejected from NodeSet!
{% endhint %}

If you no longer wish to participate as an operator for any of NodeSet's StakeWise vaults, please contact us at _info@nodeset.io_. We are working on a way to exit your operation automatically through the dashboard, but this is not ready yet.

## Validator Lifecycle

The following is StakeWise-specific. For a refresher on the Ethereum validator lifecycle, see [this page](https://www.attestant.io/posts/understanding-the-validator-lifecycle/).

###

## Disaster Recovery

{% hint style="info" %}
Operators do NOT need to exit StakeWise validators to migrate or recover their nodes! As long as you still have your wallet mnemonic, you can recover your StakeWise validator keys.
{% endhint %}

In addition to [the usual steps you take to recover your wallet on new hardware](../../node-operators/hyperdrive/disaster-recovery-and-node-migration.md#wallet-recovery), you also need to recover your StakeWise keys specifically. In the future, this will be done automatically, but currently you will need to run the following command manually to recover your StakeWise configuration:

`hyperdrive stakewise wallet generate-keys --count [123]`

In the above command, \[123] should be the number of keys you have already already uploaded to NodeSet, which you can view at [https://nodeset.io/dashboard/stakewise/validators](https://nodeset.io/dashboard/stakewise/validators).

## Claiming Rewards

{% hint style="info" %}
Node Operator rewards for StakeWise validators are not live yet, but rewards are already accruing! We will update this page when operators can claim rewards for the StakeWise validators they run.
{% endhint %}
