# Node Operator Guide (WIP)

Although it is technically possible to run a StakeWise node alongside an existing Ethereum node, we recommend using a completely isolated system, and this guide assumes this is the case.

Note that the commands here are only examples. We used Debian 12 to create this guide, but your local environment may be different. **Do not simply copy and paste these commands without understanding!**

{% hint style="info" %}
&#x20;here are technical limitations which make it difficult to run a fully custom environment for the NodeSet-StakeWise integration. See [this repository](https://github.com/nodeset-org/hyperdrive-stakewise) for a compatible environment using scripts provided by NodeSet.
{% endhint %}

***

## **Installation**

### **1. Plan your node operation**

[See this section of the Node Operator Best Practices page.](../node-operators/best-practices.md#plan-your-node-architecture)



### 3. Install the NodeSet-StakeWise client

Use the interactive installer to set up a StakeWise node. For more information, [see the README for Hyperdrive.](https://github.com/nodeset-org/hyperdrive-stakewise)



### 4. Backup your mnemonic and private key

Ensure you store these secrets safely and regularly test your access procedures. We recommend two copies in offline cold storage, each in different locations. This is only in case of emergency, since you can access your secrets at any time from a healthy node.



### 6. (Optional) Set your graffiti to identify yourself as a NodeSet operator

Nimbus: [https://nimbus.guide/graffiti.html](https://nimbus.guide/graffiti.html)

```
nimbus_beacon_node --graffiti="<YOUR_WORDS>"
```



### 8. Generate pre-signed exit messages

{% hint style="info" %}
This step requires validators to already be active on the network long enough to receive an index from the network. Make sure you've completed the prior step before continuing.
{% endhint %}

Out of an abundance of caution, operators must share pre-signed exit messages with NodeSet so that your validators may be exited if you are unable to exit gracefully.&#x20;

Use [this custom fork of the staking-deposit-cli](https://github.com/nodeset-org/staking-deposit-cli) to generate these messages (or your own preferred solution like ethdo).



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
