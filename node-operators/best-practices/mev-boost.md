# MEV Boost

{% hint style="info" %}
For a primer on MEV in general, please see the [official Ethereum documentation](https://ethereum.org/en/developers/docs/mev/).
{% endhint %}

To maximize earnings, node operators generally should use external APIs for block building rather than building blocks locally. Hyperdrive includes Flashbots' [MEV Boost](https://github.com/flashbots/mev-boost) to enable this feature automatically for operators.

Although NodeSet highly recommends the usage of at least one relay (and ideally, multiple), the choice of which MEV relay(s) to utilize (or whether to utilize them at all) is entirely up to the operator, as NodeSet has no way to enforce this.&#x20;

Hyperdrive includes some relays built-in, but users may also add custom relays using the [configuration TUI](../hyperdrive/configuration.md). For a full list of existing MEV relays, their URLs, and their properties, see [the ETHStaker documentation](https://github.com/eth-educators/ethstaker-guides/blob/main/MEV-relay-list.md).

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Hyperdrive's MEV-Boost Settings Menu</p></figcaption></figure>
