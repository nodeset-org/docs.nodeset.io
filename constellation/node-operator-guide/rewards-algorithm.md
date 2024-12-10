---
description: >-
  Detailed description of how node operator rewards are calculated for
  Constellation
---

# Rewards Algorithm

There are two different times that rewards are issued to Node Operators in Constellation: when a minipool is processed and when a Merkle claim is submitted. The rewards from each of these are distributed differently, so we'll treat each as a separate algorithm, outlined below.

First we check the beacon node for all relevant validators and update their `activationEpoch` and `exitEpoch`, translating them into the starting blocks of those epochs, and store that data with the validators in the database as `activationBlock` and `exitBlock`.

In order to initiate each reward processing, we then scan for events between the last block we've scanned and the current block, looking for \`MinipoolProcessed\` and \`MerkleClaimSubmitted\` events. We then assign rewards based on algorithm according to the event type:

### MerkleClaimSubmitted

When a `MerkleClaimSubmitted` event is found, the first thing we do is find the block of the _previous_ `MerkleClaimSubmitted` event (using the block the contract was deployed if there is no previous `MerkleClaimSubmitted` event). We'll call this value `fundingStartBlock`. We then assign the block of the new `MerkleClaimSubmitted` event to a value called `fundingEndBlock` and the `amount` in the new `MerkleClaimSubmitted` event to `fundingAmount`.&#x20;

The idea here is that the rewards from the current `MerkleClaimSubmitted` event represent the work done in the period of time since the last `MerkleClaimSubmitted` event, and so the rewards of the current event should be distributed among all validators active between the previous event and the current one.

To calculate the amount that each validator should receive, we get a list of all validators that have an `activationBlock` before the `fundingEndBlock` and are either still active or have an `exitBlock` later than the `fundingStartBlock`, which in effect gets a list of all validators that were active for some period overlapping the time between the previous event and the current one.

Then for every validator we calculate how many "shares" of the reward they've earned:

`shares = min(exitBlock, fundingEndBlock) - max(activationBlock, fundingStartBlock)`

Which in effect counts the number of blocks the validator has been active that overlap with the period of time between the last `MerkleClaimSubmitted` event and the current one.&#x20;

We then total up all validators' `shares` amounts into `totalShares`, allowing us to calculate the percentage of the total pool of shares that each validator has operated, and we award each validator that percentage of the total `fundingAmount`:&#x20;

`awards = fundingAmount * (shares / totalShares)`

#### Example

Let's say we have 4 validators:

* Validator A has a `startBlock` of `390000` and an `exitBlock` of `411000`&#x20;
* Validator B has a `startBlock` of `395000` and an `exitBlock` of `416000`&#x20;
* Validator C has a `startBlock` of `400000` and is still active
* Validator D has a `startBlock` of `412000` and is still active

We have a new `MerkleClaimSubmitted` event at block `413000` with an amount of `50000` and the previous `MerkleClaimSubmitted` event at block `410000` (the amount of the previous event is irrelevant).

<img src="../../.gitbook/assets/file.excalidraw (1).svg" alt="" class="gitbook-drawing">

Each validator would have the following shares:

* Validator A: `min(411000, 413000) - max(390000, 410000)` = `411000 - 410000` = `1000`&#x20;
* Validator B: `min(416000, 413000) - max(395000, 410000)` = `413000 - 410000` = `3000`
* Validator C: `min(infinite, 413000) - max(400000, 410000)` = `413000 - 410000` = `3000`
* Validator D: `min(infinite, 413000) - max(412000, 410000)` = `413000 - 412000` = `1000`

The total number of shares would be `1000 + 3000 + 3000 + 1000 = 8000`

So each validator's percentage of the reward would be:

* Validator A: `1000 / 8000 = 0.125`
* Validator B: `3000 / 8000 = 0.375`
* Validator C: `3000 / 8000 = 0.375`
* Validator D: `1000 / 8000 = 0.125`

And with the event amount being `50000`, the final rewards would be:

* Validator A: `50000 * 0.125 = 6250`
* Validator B: `50000 * 0.375 = 18750`
* Validator C: `50000 * 0.375 = 18750`
* Validator D: `50000 * 0.125 = 6250`

### MinipoolProcessed

Whenever a `MinipoolProcessed` event is found, we first get the `ethRewards` \* from the event and, using the same logic [as the contract](https://github.com/nodeset-org/constellation/blob/main/contracts/Constellation/OperatorDistributor.sol#L520), we get the `noFee` from the `minipoolData` [of the validator](https://github.com/nodeset-org/constellation/blob/main/contracts/Constellation/SuperNodeAccount.sol#L102), then run:

`mulDiv(ethRewards, noFee, CALC_BASE)` (where `CALC_BASE = 10 ** 18`)

Using an off-chain implementation of [OpenZeppelin's mulDiv operation](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/math/Math.sol#L144). We then assign that amount as rewards to the validator.

The reason we need to re-perform the same calculation as `onEthBeaconRewardsReceived` is that `onEthBeaconRewardsReceived` was added in an update, so the oldest processing events don't have a corresponding `onEthBeaconRewardsReceived` event.&#x20;

\* Currently the `MinipoolProcessed` event erroneously reports `ethRewards` as `0` if the minipool was finalized, so when the `finalized` value is true in the event we instead recalculate the correct `ethRewards` value off-chain using logic identical [to the contract](https://github.com/nodeset-org/constellation/blob/main/contracts/Constellation/OperatorDistributor.sol#L290).

### Unprocessed Rewards

In the dashboard you may see "unprocessed rewards" for your validators. These are calculated by looking at the balance of the validator's minipool address and calculating the hypothetical reward amount using the same calculation used for calculating rewards from `MinipoolProcessed` events. Essentially, it is the amount of rewards expected if you were to initiate a minipool processing event at the current moment (not including the transaction costs of doing so).

The balances of each validator are updated every 10,000 blocks, so the balance in the dashboard may not immediately reflect the latest balance, but the _actual_ amount rewarded to you when a minipool is processed uses the values from the actual `MinipoolProcessed` events, so the actual reward amounts will always be accurate and the unprocessed amounts will at worst reflect a slightly outdated, and thus lower, amount than reality.



