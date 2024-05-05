# Node Operator Guide

Although it is technically possible to run a StakeWise node alongside an existing Ethereum node, we recommend using a completely isolated system, and this guide assumes this is the case.

Note that the commands here are only examples. We used Debian 12 to create this guide, but your local environment may be different. **Do not simply copy and paste these commands without understanding!**

{% hint style="info" %}
There are technical limitations which make it very difficult to run a fully custom node environment for NodeSet's StakeWise integration. Therefore, you must use [the Hyperdrive client](https://github.com/nodeset-org/hyperdrive) to connect appropriately to NodeSet's web services.
{% endhint %}

***

## **Installation**

### **1. Plan your node operation**

[See this page on planning your node operation.](../node-operators/best-practices/planning-your-node-architecture.md)

### 2. Install Hyperdrive and run the StakeWise setup process

Use the interactive installer for Hyperdrive to set up a StakeWise node. For more information, [see the README for Hyperdrive.](https://github.com/nodeset-org/hyperdrive)

{% hint style="info" %}
Your node wallet must have enough ETH in it to register validators, so don't forget to fund it with enough ETH to pay for gas! We recommend at least 0.1 ETH, since it costs about 0.01 at 30 gwei to register one validator.
{% endhint %}

#### 2.1 Install Hyperdrive service using the CLI:

`hyperdrive service install` You may need to restart your shell as per instructions.

#### 2.2. Follow the interactive setup to configure your node:

`hyperdrive service config`

If you wish to use checkpoint sync, you can pick [one of the URLs from this list](https://eth-clients.github.io/checkpoint-sync-endpoints/).

Remember to enable module support for Stakewise during the setup process! Your node should start syncing automatically when you're done with the installation, but we recommend you keep an eye on things using `hyperdrive service logs`.

#### 2.3 Initialize the Stakewise package's connection to the Hyperdrive node wallet

`hyperdrive stakewise wallet init`

#### 2.4. Generate validator keys

`hyperdrive stakewise wallet generate-keys`&#x20;

This command will generate new validator keys, upload them to NodeSet so we can refer them to the StakeWise vault, and&#x20;

Now, the status command should show active validator pubkeys: `hyperdrive stakewise status`

### 3. Add your node address to your NodeSet account

a) Go to [https://nodeset.io/dashboard](https://nodeset.io/dashboard) (beta testers should use [https://staging.nodeset.io/dashboard](https://staging.nodeset.io/dashboard)) to create or login to your NodeSet account. Users who have gone through the onboarding process will automatically be given the StakeWise permission.

b) Use the dashboard to add your new node address.

### 4. Backup your node wallet mnemonic and/or private key

Ensure you store your secrets safely and regularly test your access procedures. We recommend two copies in offline cold storage, each in different locations.

### 5. Maintain your node

Once NodeSet registers your node, we will sync its deposit data with the vault, and ETH may be automatically deposited into these validators at any time.

As always, you should [use the same best practices for maintaining your operation](../node-operators/best-practices/).

{% hint style="warning" %}
Be careful! Even if there are no validators activated when your node goes down, Ethereum never goes down, so deposits might be made to those validators even while the node is offline. If this happens, those validators will be penalized, and you may eventually be ejected from NodeSet!
{% endhint %}

If you no longer wish to participate as an operator for any of NodeSet's StakeWise vaults, please contact us at info@nodeset.io. We are working on a way to exit your operation automatically through the dashboard, but this is not ready yet.

### Note regarding rewards&#x20;

Because adding users to the splitter contracts and the vault is costly and NodeSet currently pays this fee, we will initially do it manually and irregularly, so there may be a delay before you begin accruing rewards. Please be patient while we work to improve and automate this flow over time. In the future, users will instead take on these costs as a one-time node registration fees in the future. As a reminder, you are already responsible for new validator registration -- [see here for more info](faq.md#why-do-node-operators-need-to-pay-to-register-nodes).
