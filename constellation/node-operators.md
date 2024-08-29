# Node Operators

## Node Operators <a href="#id-2259" id="id-2259"></a>

The rewards for xrETH and xRPL comes from the base Rocket Pool protocol, thanks to NOs who opt-in to Constellation. This process is simple and mostly automated: register with NodeSet, download and install Hyperdrive, run validators, and earn rewards! To ensure depositors receive 100% of ETH staking rewards, NO compensation flows from the rETH commission.

Behind the scenes, Hyperdrive can create as required using depositors’ ETH with no input needed from the NO. They just need to maintain a node as usual to be rewarded by Constellation.

However, to fuel the continual creation of new validators in a non-custodial manner, NOs will need to pay initialization gas costs. To understand the full flow, let’s go over the details of minipool creation for Constellation in detail.

**Minipool Creation**

1. First, a NO requests authorization to add themselves to the whitelist, then submits that authorization and is whitelisted by the contracts
2. Next the NO calls a function on one of the Constellation contracts that deploys a new minipool contract that is associated with Constellation's "Supernode". To call this function, they must have authorization. This authorization is only given if there is a pre-signed exit message on file for all existing validators. This function also requires NOs to lock up 1 ETH to disincentivize deposit contract front-running attacks.
3. After the scrub period, the NO makes a second transaction to "stake" that minipool (automated by default by Hyperdrive), which returns the 1 ETH locked to the NO.
4. That's it! This process can be repeated to make as many minipools as allowed by the protocol.

NOs always have an incentive to run as many minipools as allowed by Constellation because they are paid for each minipool they run.

### Rewards

{% hint style="info" %}
&#x20;See [the xrETH documentation](xreth.md#no-staking-fees) for the liquid staker perspective
{% endhint %}

Node operators who supply infrastructure for Constellation receive rewards from the protocol which is equal to 50% of the difference between Rocket Pool's enhanced node earnings and the typical Ethereum staking rewards:

`0.5 * rETH commission * ETH staking yield * 3` per ETH per year

For example, with an ETH staking reward rate of 4% and an rETH commission of 14%, Constellation operators earn 0.0672 ETH per LEB8 minipool per year.
