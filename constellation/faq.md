# FAQ

## Will Constellation have a governance token?

There are no plans for a governance token. Constellation is an extension of Rocket Pool — it is not a wholly separate protocol with complex governance needs. Generally, we respect the “ungovernance” principle that projects like [Liquity](https://www.liquity.org/) and [Reflexer](https://reflexer.finance/) model for the same reasons that [Vitalik enunciates well here](https://vitalik.ca/general/2021/08/16/voting3.html). As mentioned above, we hope to eventually fully automate and ossify Constellation, and building up governance in the meantime is counterproductive to this goal.

## Why wasn't this added to Rocket Pool itself?

This original concept was studied during Rocket Pool’s development, and back then, it was called nETH. However, the lack of sybil-resistance and other tools to combat NO malfeasance prevented the idea’s viability. Put another way, sybil-resistance is incompatible with the fundamental design requirement that Rocket Pool remain fully permissionless, so Rocket Pool abandoned the idea.

Constellation, however, as a distinct project built on top of the fully permissionless base protocol, has more flexibility to relax permissioning standards and delegate NO onboarding to an independent administrator to perform the required sybil checks. Thus, the tradeoffs for depositors become more clear: if one believes the administrator and NO’s incentive alignment is sufficient, Constellation will offer higher returns via xrETH, and if one disagrees, then rETH is the appropriate token. Either way, since it’s built on top instead of included with the core protocol, if Constellation malfunctions, Rocket Pool’s normal functionality is unaffected.

## What happens to all the new RPL voting power in Constellation?

Rocket Pool governance is structured so that each node has voting power relative to its RPL stake. Constellation's architecture utilizes one "supernode" contract, but this contract does not have governance wrapper functions implemented so as not to unduly interfere with the base layer's typical governance functions. Put simply, none of the RPL staked in a Constellation instance will be able to participate in on- or off-chain RP DAO processes. Note that because some of these processes (e.g. proposal challenges) are defense mechanisms for Rocket Pool, it may become necessary to add limited RP governance functionality to Constellation in the future.

## How does the xrETH price feed work? Is there an oracle?

Although Rocket Pool provides the tooling necessary to track xRPL price data, xrETH is more challenging. NodeSet has developed an open-source Proof-of-Authority oracle for the beacon chain rewards accrued to Constellation. Merkle rewards (execution layer rewards for ETH and RPL staking rewards) are collected all at once and then smoothly reverse-streamed to ensure consistent token valuation updates.

After [EIP-4788](https://eips.ethereum.org/EIPS/eip-4788) went live with the Deneb Ethereum upgrade, more decentralized solutions are available for a beacon chain rewards oracle, but Constellation was already far enough along with development that these solutions must be the focus of future protocol upgrades.

## What if the administrator does bad stuff?

There is a whole category of attacks against Constellation by the administrator which we have termed “Bad Admin” attacks. This includes subcategories like “Evil Admin” attacks and “Incompetent Admin” scenarios, for example. These are all the subject of ongoing security research, but there are several ways NodeSet has designed Constellation to avoid any risk of administrator malfeasance. For example:

* Parameter changes and contract upgrades will have a substantial delay so that depositors or NOs can leave the system before they take effect if they disagree
* Rate-limits may be applied to the removal of NOs so that the administrator can’t take over the network without depositors leaving first

However, there are some centralization risks inherent in the initial design of Constellation. There is no way to prevent the admin or other trusted roles from doing Bad Things. Instead, users are encouraged to be cautious and monitor the system to ensure they exit before changes they disagree with go into effect.
