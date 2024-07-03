# Claiming Rewards

## Claim Procedure

To claim your StakeWise rewards from the rewards contract, use one of the following two methods:

* If your withdrawal address is a hot wallet, then you can simply connect that wallet to the [splitter contract for the vault](../introduction.md) on [app.splits.org](https://app.splits.org).&#x20;
* If your node wallet is the withdrawal address, you can claim StakeWise rewards with Hyperdrive using the `hyperdrive stakewise wallet claim-rewards` command.

## Withdrawal Address

The default StakeWise rewards claim address for all networks is the first node you registered with NodeSet, but you can easily set an alternate withdrawal address per network in your NodeSet profile ([https://nodeset.io/dashboard/profile](https://nodeset.io/dashboard/profile)). When changed, this new withdrawal address will only be reflected after the next rewards contract update occurs, and any existing unclaimed rewards will be claimable via the new address.

{% hint style="info" %}
If you have a different node wallet for mainnet vs testnet, please ensure the withdrawal address is set correctly! Although there are unique deployments of the rewards contract, Ethereum addresses are tied to the same seed phrase on all EVM chains, so there is no difference between a holesky node and a mainnet node in the NodeSet dashboard.
{% endhint %}

## Technical Context

NodeSet currently uses [splits.org](https://splits.org) to distribute StakeWise vault rewards to operators, and this is done by manually updating this contract with a list of addresses and percentage allocations for operators. Because it is a manual process, NodeSet updates it infrequently, but we are developing a custom rewards contract to improve the experience for operators in the future.
