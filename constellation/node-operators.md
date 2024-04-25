# Node Operators

## Node Operators <a href="#id-2259" id="id-2259"></a>

The rewards for xrETH and xRPL comes from the base Rocket Pool protocol, thanks to NOs who opt-in to Constellation. This process is expected to be simple and mostly automated: register with the NodeSet network, download and install an extension to Rocket Pool’s smartnode CLI, run validators, then earn rewards! To ensure depositors receive 100% of ETH staking rewards, NO compensation flows from the rETH commission.

Behind the scenes, NodeSet’s node operator software will create and exit minipools as required using depositors’ ETH with no input needed from the NO. They just need to maintain a Rocket Pool node as usual to get rewarded by Constellation.

However, to fuel the continual creation of new validators in a non-custodial manner, NOs will need to pay initialization gas costs. To understand the full flow, let’s go over the details of minipool creation for Constellation in detail.

**Minipool Creation**

1. NO deploys a node contract and sets the Constellation contract as its withdrawal address.
2. NO deploys a minipool for that node.
3. NO makes a request for Constellation to stake assets into their new minipool. This requires an (encrypted) pre-signed exit message for the validator to be sent to and subsequently approved by Constellation’s admin.
4. If the minipool is validated and approved, the necessary ETH and RPL will be staked by Constellation into that minipool.
5. This process can be repeated to make as many minipools as allowed by the protocol.

NOs always have an incentive to run as many minipools as allowed by Constellation because they are paid for each minipool they run.
