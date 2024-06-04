# Authorizing Your Node

{% hint style="info" %}
Before operators can connect their nodes and earn rewards, they must first [create an account on the NodeSet dashboard](introduction.md#creating-an-account).
{% endhint %}

To connect your node to your NodeSet account, follow the steps listed here.&#x20;

1. Use the [View/Add Authorized Node Addresses](https://staging.nodeset.io/dashboard/stakewise/authorized-addresses) page to whitelist your node address. You may whitelist any Ethereum address and any number of them, but these will only become authorized and connected after verification of ownership in the next step.
2. In Hyperdrive, use the `hyperdrive stakewise nodeset register-node` command to register the node. This will prompt you to enter the email address you used to create your NodeSet account, then sign a message proving your ownership of this node address and upload it to NodeSet.&#x20;

Once you've successfully authorized your node, Hyperdrive's full capabilities are unlocked and you will see that node address in the list of authorized nodes on the dashboard.

\
