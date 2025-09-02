---
description: Quick start guide for NodeSet operators serving StakeWise vaults
---

# Node Operator Guide

{% hint style="info" %}
There are technical limitations which make it very difficult to run a fully custom node environment for NodeSet's StakeWise integration. Therefore, you must use [the Hyperdrive client](https://github.com/nodeset-org/hyperdrive) to connect appropriately to NodeSet's web services.
{% endhint %}

***

## **Installation**

### **1. Plan your node operation**

[See this page on planning your node operation.](../../node-operators/best-practices/planning-your-node-architecture.md)

### 2. Install Hyperdrive

[See this page for more information on setting up Hyperdrive](https://docs.nodeset.io/node-operators/hyperdrive). Remember to enable support for StakeWise during the setup process!

#### Enabling the StakeWise Module

StakeWise support is currently **open to all registered node operators**. There is no permissions gate to use it.

Open the config UI with `hyperdrive service config`, navigate to the `Modules` section, and open the `StakeWise` module. Check it to enable it, then save and exit. You will be prompted to restart your services in order to launch the StakeWise module.

### **3. Fund your node wallet**

{% hint style="info" %}
You must send ETH to your node wallet so that Hyperdrive can submit deposit transactions for your validators. This is an important mechanism in StakeWise to prevent griefing attacks ([see here for more information](https://docs.nodeset.io/stakewise-integration/faq#why-do-node-operators-need-to-pay-to-register-validators)).
{% endhint %}

We recommend funding your node wallet with 0.01 ETH to pay the gas costs of generating validators. Each validator costs approximately .00034 ETH at 1 gwei gas costs. If you run out of ETH in your wallet, you won't be able to create more validators, even if there are assets available.

For testing on the Hoodi network, you can obtain funds using a faucet. NodeSet has not verified these faucets. Use them at your own risk!

* [https://hoodi-faucet.pk910.de/](https://hoodi-faucet.pk910.de/)

### 4. Add your node address to your NodeSet account

a) Go to [https://nodeset.io/dashboard](https://nodeset.io/dashboard) to create or login to your NodeSet account. Users who have gone through the on-boarding process will automatically be given the permission to access the StakeWise portion of the dashboard.

b) Use the dashboard to [add your new node address](../../nodeset-dashboard/authorizing-your-node.md).

### 5. Generate validator keys

```bash
hyperdrive stakewise wallet generate-keys 
```

You can optionally provide the `--count` flag, along with the number of keys to generate, instead of answering the question within the interactive prompt.

You should see output like this:

```
Note: key generation is an expensive process, this may take a long time! Progress will be printed as each key is generated.

Generated 0x903bee1b9f05c133548f4afae99b7c51cfd1646389a629554a49bf69cb7ce0e4216ee50e3b882a665ca595949fff65aa (1/2) in 4.586464858s
Generated 0xa5172893d3252995c8a7178a88b7798edbc96b4733629eb96e04bd52b716645bd59cd2b1fb470ada8ac0b3d84cd84746 (2/2) in 4.697215708s
Completed in 9.283731898s.

You now have 2 validator keys ready for deposits:
	0x903bee1b9f05c133548f4afae99b7c51cfd1646389a629554a49bf69cb7ce0e4216ee50e3b882a665ca595949fff65aa
	0xa5172893d3252995c8a7178a88b7798edbc96b4733629eb96e04bd52b716645bd59cd2b1fb470ada8ac0b3d84cd84746

Restarting Validator Client to load the new keys... done!
Your new keys are now loaded.
Your node will deposit with them automatically once the vault has been funded.
It will start attesting for those validators automatically once they have been activated.
```

This will let you generate one or more keys, add then to your Validator Client, and mark them as available for new deposits. Note that the Hyperdrive daemon will verify any new keys haven't been used for deposits previously before providing them to StakeWise.

Additionally, you should see those validator keys in the NodeSet dashboard at [https://nodeset.io/dashboard/stakewise/validators](https://nodeset.io/dashboard/stakewise/validators).

### 6. Backup your node wallet mnemonic and/or private key

Ensure you store your secrets safely and regularly test your access procedures. We recommend two copies in offline cold storage, each in different locations.

### 7. Maintain your node

Once NodeSet registers your node, ETH may be automatically deposited into your validators at any time.

As always, you should [use the same best practices for maintaining your operation](../../node-operators/best-practices/).

{% hint style="warning" %}
Be careful! Your node must be online 100% of the time! If your node goes down, any active validators will be penalized, and you may be ejected from NodeSet!&#x20;
{% endhint %}

If you no longer wish to participate as an operator for any of NodeSet's StakeWise vaults, you may exit your validators at any time. **Make sure to also contact us at** [_**info@nodeset.io**_](mailto:info@nodeset.io) **so we can help you ensure your node was correctly exited.**

## Claiming Rewards

{% hint style="info" %}
Node Operator rewards for StakeWise validators are not live yet, but rewards are already accruing! We will update this page when operators can claim rewards for servicing StakeWise validators.
{% endhint %}
