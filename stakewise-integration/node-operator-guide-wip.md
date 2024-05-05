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

#### 2.1 Install Hyperdrive service using the CLI:

```bash
hyperdrive service install
```

You may need to restart your shell as per instructions. Also see the dedicated page for setup instructions for [Hyperdrive](https://docs.nodeset.io/node-operators/hyperdrive).

#### 2.2. Follow the interactive setup to configure your node:

```bash
hyperdrive service config
```

If you wish to use checkpoint sync, you can pick [one of the URLs from this list](https://eth-clients.github.io/checkpoint-sync-endpoints/).

Remember to enable module support for Stakewise during the setup process! Your node should start syncing automatically when you're done with the installation, but we recommend you keep an eye on things using `hyperdrive service logs`.

If you are running the Rocket Pool Smartnode Stack on the same machine, and want to use it's consensus and execution client, you will have to do the following:

a) Expose the Smarnode Stack RPC and API endpoints externally. In the Settings Manager (`rocketpool service configure`) in both the ETH1 and ETH2 categories, choose *"Open to External hosts"* from the respective dropdowns. *Open to localhost* is not sufficient, due to how Docker networking works.

b) During setup/configuration choose "External mode". Determine the external IP of your host (e.g. using `ifconfig | grep 'eth0:' -A 1`), and use that when specifying the external ETH1 and ETH2 endpoints.

#### 2.3 Initialize the Stakewise package's connection to the Hyperdrive node wallet

```bash
hyperdrive stakewise wallet init
```

(((Don't you have to run `hyperdrive wallet init` first? I don't remember...)))

#### 2.4 Add your node address to your NodeSet account

Fetch your node address:

```bash
hyperdrive wallet status
```

a) Go to [https://nodeset.io/dashboard](https://nodeset.io/dashboard) (beta testers should use [https://staging.nodeset.io/dashboard](https://staging.nodeset.io/dashboard)) to create or login to your NodeSet account. Users who have gone through the onboarding process will automatically be given the StakeWise permission.

b) Use the dashboard to add your new node address.

Note regarding addresses: You can use any address you like to log in. You will need to provide the e-mail you signed up to NodeSet with. That's how you are actually authenticated. Then add your node address at https://staging.nodeset.io/dashboard/stakewise/authorized-addresses.

#### 2.5 Get some Holesky ETH

You can use the [Rocket Pool faucet](https://docs.rocketpool.net/guides/testnet/overview#getting-test-eth-on-holesky) to do so.

#### 2.6 Generate some validator keys

```bash
hyperdrive stakewise wallet generate-keys
```

This will generate new validator keys derived from your node wallet. You can run this command again.

{% hint style="info" %}
Your node wallet must have enough ETH in it to register validators, so don't forget to fund it with enough ETH to pay for gas! We recommend at least 0.1 ETH, since it costs about 0.01 at 30 gwei to register one validator.
{% endhint %}

Each operator is currently allotted 10 validators, but this may be increased if there are not enough operators to service all of the deposits.

#### 2.7 Upload the validator keys to NodeSet

```bash
hyperdrive stakewise nodeset upload-deposit-data
```

This uploads the combined deposit data for all of your validator keys to NodeSet's Stakewise vault, so they can be assigned new deposits.

#### 2.8 Validate your setup

The status command should now show your active validator pubkeys:

```bash
hyperdrive stakewise status
```

You should also see those validators in the NodeSet dashboard at https://staging.nodeset.io/dashboard/stakewise/validators.

### 3. Backup your node wallet mnemonic and/or private key

Ensure you store your secrets safely and regularly test your access procedures. We recommend two copies in offline cold storage, each in different locations.

### 4. Maintain your node

Once NodeSet registers your node, we will sync its deposit data with the vault, and ETH may be automatically deposited into these validators at any time.

As always, you should [use the same best practices for maintaining your operation](../node-operators/best-practices/).

{% hint style="warning" %}
Be careful! Even if there are no validators activated when your node goes down, Ethereum never goes down, so deposits might be made to those validators even while the node is offline. If this happens, those validators will be penalized, and you may eventually be ejected from NodeSet!
{% endhint %}

If you no longer wish to participate as an operator for any of NodeSet's StakeWise vaults, please contact us at info@nodeset.io. We are working on a way to exit your operation automatically through the dashboard, but this is not ready yet.

### Note regarding rewards&#x20;

Because adding users to the splitter contracts and the vault is costly and NodeSet currently pays this fee, we will initially do it manually and irregularly, so there may be a delay before you begin accruing rewards. Please be patient while we work to improve and automate this flow over time. In the future, users will instead take on these costs as a one-time node registration fees in the future. As a reminder, you are already responsible for new validator registration -- [see here for more info](faq.md#why-do-node-operators-need-to-pay-to-register-nodes).
