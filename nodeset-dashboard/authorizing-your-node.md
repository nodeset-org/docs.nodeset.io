# Authorizing Your Node

{% hint style="info" %}
Before operators can connect their nodes and earn rewards, they must first [create an account on the NodeSet dashboard](introduction.md#creating-an-account).
{% endhint %}

To connect your node to your NodeSet account, follow the steps listed here.&#x20;

1. Use the [Node Addresses](https://www.nodeset.io/dashboard/node-addresses) page to whitelist your node address by adding it as a pending node address. You may add any Ethereum address and any number of them, but these will only become registered and connected after verification of ownership in the next step.
2. In Hyperdrive, use the `hyperdrive nodeset register-node` command to register the node. This will prompt you to enter the email address you used to create your NodeSet account, then it will automatically confirm your ownership of the node's private key and authorize its use with your NodeSet account.

Once you've successfully authorized your node, Hyperdrive's full capabilities are unlocked and you will see that node address in the list of authorized nodes on the dashboard.

\
