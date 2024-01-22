# Node Operator Guide (WIP)

Although it is technically possible to run a StakeWise node alongside an existing Ethereum node, we recommend using a completely isolated system, and this guide assumes this is the case.

Note that the commands here are only examples. We used Debian 12 to create this guide, but your local environment may be different. **Do not simply copy and paste these commands without understanding!**

{% hint style="info" %}
&#x20;here are technical limitations which make it difficult to run a fully custom environment for the NodeSet-StakeWise integration. See [this repository](https://github.com/nodeset-org/hyperdrive-stakewise) for a compatible environment using scripts provided by NodeSet.
{% endhint %}

***

## **Installation**

### **1. Plan your node operation**

[See this page on planning your node operation.](../node-operators/planning-your-node-architecture.md)

### 2. Install Hyperdrive and run the StakeWise setup process

Use the interactive installer for Hyperdrive to set up a StakeWise node. For more information, [see the README for Hyperdrive.](https://github.com/nodeset-org/hyperdrive-stakewise)



### 3. Update your node to your NodeSet account

a) Go to [https://nodeset.io/dashboard](https://nodeset.io/dashboard) and create and/or login to your NodeSet account

b) Use the dashboard to add your new node address

c) Confirm the registration of your node with Hyperdrive (this is free):&#x20;

`nodeset stakewise register myusername@myemail.com`



### 4. Backup your mnemonic and private key

Ensure you store these secrets safely and regularly test your access procedures. We recommend two copies in offline cold storage, each in different locations. This is only in case of emergency since you can access your secrets at any time from a healthy node.



### 6. (Optional)&#x20;



### 9. Send your payment address, validator deposit data, and pre-signed exit messages to NodeSet

deposit\_data@nodeset.io (?)

Some form on our website?\
Some API we create?



### 10. Maintain your node

Once NodeSet receives your deposit data and associated exit messages, we will upload the validator keys to the StakeWise vault contract, and ETH may be automatically deposited into these validators at any time.&#x20;

{% hint style="info" %}
Even if only some of your validators are filled with ETH, you will still receive the same share of rewards as everyone else. Because of this, NodeSet will only upload your deposit data when there are enough assets to justify adding new operators.

If there are large withdrawals, NodeSet may contact you to exit from a vault entirely to ensure those with active validators are still compensated fairly. \[HOW DOES STAKEWISE CHOOSE WHICH VALIDATORS TO EXIT?]
{% endhint %}

As always, you should \[use the same best practices for maintaining your operation].

{% hint style="warning" %}
Be careful! Even if there is no ETH deposited into your node's validators when it goes down, Ethereum never goes down, so deposits might be made to those validators even while the node is offline. If this happens, those validators will be penalized, and you may eventually be ejected from NodeSet!
{% endhint %}

If you no longer wish to participate as an operator for any of NodeSet's StakeWise vaults, please contact us at info@nodeset.io.
