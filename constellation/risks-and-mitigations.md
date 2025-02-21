---
description: Understand the mechanisms designed to keep assets in Constellation safe
---

# Risks and Mitigations

### **Timelocks and Admin Risk**&#x20;

While some administration tasks in Constellation are relatively safe, such as changing the maximum number of validators each node operator is allowed, there are other parameter adjustments that will immediately affect users returns or represent critical security concerns. For these settings, Constellation uses [standard timelock contracts](https://docs.openzeppelin.com/contracts/4.x/api/governance#TimelockController) to give users time to exit the system before potentially dangerous maintenance occurs.&#x20;

There are three levels of timelocks in Constellation:

{% hint style="info" %}
The timelocks are set to small values during Constellation's initial deployment to ensure administrators can react quickly. These values will be increased after a successful launch.
{% endhint %}

<table><thead><tr><th width="112">Name</th><th width="162">Current Length</th><th>Affected Parameters</th></tr></thead><tbody><tr><td>Short</td><td>1 block</td><td>ETH/RPL system ratios, liquidity reserve requirements, NO temporary bond value, operator removal</td></tr><tr><td>Medium</td><td>1 block</td><td>Treasury fees, NO fees, mint fee</td></tr><tr><td>Long</td><td>7 days</td><td>Contract upgrades</td></tr></tbody></table>

### Downtime Risk

Because NodeSet uses a distributed infrastructure model, node operators are allowed nearly full independence of their operation. This means that they may experience downtime which would allow performance to trend towards the Ethereum network average. However, NodeSet monitors network performance to ensure that downtime is reasonable. If operators experience too much downtime, their validators will be exited and they will no longer be allowed to participate.

### **Slashing Risk**

[If Ethereum validators engage in behavior that appears malicious to the network, they will be slashed.](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/rewards-and-penalties/) Because of this deterrence, slashing incidents are accidental and extraordinarily rare. However, it is [statistically much more likely for large, enterprise operators](https://blog.lido.fi/category/postmortem/) to be slashed due to their reliance upon high-availability setups which cause double-signing infractions.

xrETH is not inherently protected against slashing. However, xrETH is staked across hundreds of independent operators individually vetted by NodeSet, and accordingly, asset exposure risk for the failure of any individual operator is minimal. To date, no NodeSet operator has been slashed, and performance for the NodeSet network remains comparable with professional operators.

If you prefer to exchange some yield for additional slashing protection, you may consider minting osETH from[ a StakeWise vault operated by NodeSet's operators](broken-reference) instead.
