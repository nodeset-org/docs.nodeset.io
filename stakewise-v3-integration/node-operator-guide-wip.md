# Node Operator Guide (WIP)

Although it is technically possible to run a StakeWise node alongside an existing Ethereum node, we recommend using a completely isolated system, and this guide assumes this is the case.

Note that the commands here are only examples. We used Debian 12 to create this guide, but your local environment may be different. **Do not simply copy and paste these commands without understanding!**

There are technical limitations which make it difficult to run a fully custom environment for the StakeWise vaults which NodeSet operators service. See [this repository](https://github.com/nodeset-org/hyperdrive-stakewise) for a compatible environment using scripts provided by NodeSet.

***

### **1. Setup eth1 and eth2 clients**

There are many guides available, such as [Somer Esat's excellent solo staker guide](https://github.com/SomerEsat/ethereum-staking-guides). For StakeWise nodes, you only need to set and sync your clients during this step, not generate keys and make deposits -- the StakeWise operator client will do this for you.&#x20;

Given the high resource requirements of eth1 clients, we recommend you set up a separate machine with this for all of your nodes to share.

For Holesky testing, we recommend using a checkpoint sync to speed up the process: [https://eth-clients.github.io/checkpoint-sync-endpoints/#holesky](https://eth-clients.github.io/checkpoint-sync-endpoints/#holesky)&#x20;

### 2. Download and extract the latest release of v3-operator

Example using the v0.3.3 release:

<pre><code>mkdir ~/bin/stakewise
cd ~/bin/stakewise
<strong>wget https://github.com/stakewise/v3-operator/releases/latest/download/operator-v0.3.3-linux-amd64.tar.gz
</strong>tar -xf operator-v0.3.3-linux-amd64.tar.gz
mv operator-v0.3.3-linux-amd64/operator operator
rm -r operator-v0.3.3-linux-amd64*
</code></pre>



### 3. Initialize your StakeWise configuration with the NodeSet vault values:

```
./operator init
```

#### Goerli Testnet (deprecated)

Network: `goerli`&#x20;

Vault: `0x4c54003b39e25d8a6a0157b0b4c14db2a7456199`

**Holesky Testnet**

Network: `holesky`

Vault: `0x01b353Abc66A65c4c0Ac9c2ecF82e693Ce0303Bc`

#### Ethereum Mainnet

Network: `mainnet`

Vault: `0xTODO`



This step will generate a mnemonic for you. Make sure you store this seed phrase securely! See \[here] for recommendations on how to store your seed phrase.



### 4. Create new validator keys

```
./operator create-keys
```

See the SWv3 operator binary documentation for more details.



### 5. Set your eth2 client fee recipient

You are **REQUIRED** to use the StakeWise smoothing pool as the fee recipient for your validators. This is a setting passed to your eth2 client. If you use the NodeSet StakeWise docker compose, this is already set up for you.

Nimbus: [https://nimbus.guide/suggested-fee-recipient.html](https://nimbus.guide/suggested-fee-recipient.html)

Holesky: `0xc98F25BcAA6B812a07460f18da77AF8385be7b56`

Mainnet: `0x48319f97E5Da1233c21c48b80097c0FB7a20Ff86`



See the list of StakeWise compatible relays: [https://docs-v3.stakewise.io/for-operators/smoothing-pool-relays](https://docs-v3.stakewise.io/for-operators/smoothing-pool-relays)



### 6. Set your grafitti to identify yourself as a NodeSet operator

Nimbus: [https://nimbus.guide/graffiti.html](https://nimbus.guide/graffiti.html)

```
nimbus_beacon_node --graffiti="<YOUR_WORDS>"
```



### 7. Import your validator keys into your eth2 client

asdfasdfasdf



Once these keys have been active long enough to receive a validator index from the network, you can proceed to the next step.



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
