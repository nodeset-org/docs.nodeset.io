# Security Information

{% hint style="info" %}
If you wish to report any security-related issues, please email us directly at **info@nodeset.io**
{% endhint %}

### Audits

Constellation is being audited by leading independent security professionals. When these reports are available, they will be released publicly here.

### Bug Bounties

Note that, in order to be eligible for a bug bounty, you must provide a proof of concept and, if necessary, work with our developers to successfully demonstrate the issue.

Rewards for successfully replicated issues in the Constellation smart contracts are awarded according to severity as classified by the [Immunefi Vulnerability Severity Classification System](https://immunefi.com/immunefi-vulnerability-severity-classification-system-v2-3/) for smart contracts:

<table><thead><tr><th width="121">Severity</th><th width="142">Amount (USD)</th></tr></thead><tbody><tr><td>Critical</td><td>$100,000</td></tr><tr><td>High</td><td>$25,000</td></tr><tr><td>Medium</td><td>$5,000</td></tr></tbody></table>

### Scope

The following smart contracts in the `contracts/Constellation` directory of [the Constellation repository](https://github.com/nodeset-org/constellation/) are in-scope:

* Directory.sol
* MerkleClaimStreamer.sol
* SuperNodeAccount.sol
* OperatorDistributor.sol
* WETHVault.sol
* RPLVault.sol
* Whitelist.sol
* PoAConstellationOracle.sol
* PriceFetcher.sol

ONLY the most recent version of contracts deployed on mainnet are in scope. Currently, this is v1.0.0.

### Independent Mediator

[Riley Holterhus](https://www.rileyholterhus.com/) serves as an independent mediator in case there is a disagreement between the white hat and NodeSet about the severity of bug reports for Constellation.
