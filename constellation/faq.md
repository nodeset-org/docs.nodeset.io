# FAQ

**Will Constellation have a governance token?**

There are no plans for a governance token. Constellation is an extension of Rocket Pool and a prelude to building out a wider NodeSet network of opportunity for NOs — it is not a wholly separate protocol with complex governance needs. Generally, we respect the “ungovernance” principle that projects like [Liquity](https://www.liquity.org/) and [Reflexer](https://reflexer.finance/) model for the same reasons that [Vitalik enunciates well here](https://vitalik.ca/general/2021/08/16/voting3.html). As mentioned above, we hope to eventually fully automate and ossify Constellation, and building up governance in the meantime is counterproductive to this goal.

**Why wasn't this added to Rocket Pool itself?**

This original concept was studied during Rocket Pool’s development, and back then, it was called nETH. However, the lack of sybil-resistance and other tools to combat NO malfeasance prevented the idea’s viability. Put another way, the available tools were incompatible with full permissionless-ness, so Rocket Pool abandoned the idea.

Constellation, however, as a distinct project built on top of the fully permissionless base protocol, has more flexibility to relax permissioning standards and delegate NO onboarding to an independent administrator to perform the required sybil checks. Thus, the tradeoffs for depositors become more clear: if one believes the administrator and NO’s incentive alignment is sufficient, Constellation will offer higher returns via xrETH, and if one disagrees, then rETH is the appropriate token. Either way, since it’s built on top instead of included with the core protocol, if Constellation malfunctions, Rocket Pool’s sublight engines still work just fine.

**What happens to all the new RPL voting power in Constellation?**

Rocket Pool governance is structured so that NOs will simply have more individual voting power if they are a part of Constellation because they will have more RPL staked. As usual, if NOs wish to delegate their Constellation node’s voting power to another address, they may do so. We encourage NOs to delegate to the administrator so that xrETH and xRPL depositors’ interests are represented, but this is optional.

**How does the xrETH price feed work? Is there an oracle?**

Although Rocket Pool provides the tooling necessary to track xRPL price data, xrETH is more challenging. Currently, Constellation uses an oracle operated by Rated and secured crypto-economically. After [EIP-4788](https://eips.ethereum.org/EIPS/eip-4788) went live with the Deneb Ethereum upgrade, several new solutions are available, but Constellation was already nearly finished and these solutions must be the focus of future protocol upgrades.

**What if the administrator does bad stuff?**

There is a whole category of attacks against Constellation by the administrator which we have termed “Bad Admin” attacks. This includes subcategories like “Evil Admin” attacks and “Incompetent Admin” scenarios, for example. These are all the subject of ongoing security research, but there are several ways NodeSet has designed Constellation to avoid any risk of administrator malfeasance. For example:

* Parameter changes and contract upgrades will have a substantial delay so that depositors or NOs can leave the system before they take effect if they disagree
* Rate-limits may be applied to the removal of NOs so that the administrator can’t take over the network without depositors leaving first

In addition, Constellation will be audited by several top-tier firms, and there is a bug-bounty program scheduled to go live with the testnet release, as community review and participation will always be the best assurance of safety.

**What does the administrator look like? Is it one person/entity?**

At the moment, we can’t say for sure what the administrator will look like exactly for launch, but we anticipate a multi-sig will manually perform the admin duties. The exact make-up of this group depends on a number of factors which NodeSet is still researching
