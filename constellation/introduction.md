---
description: >-
  Constellation is a protocol built on Rocket Pool which improves its capital
  efficiency and scalability while reducing asset concentration risk -- all
  without compromising on the base security model.
---

# Overview

**The Problem**

To be maximally trustless, Rocket Pool requires node operators to post a bond for each validator. This restricts growth by requiring a constant supply of NOs who can afford this bond and leads to an uneven distribution of assets across nodes.



**The Solution**

Constellation liquidizes the NO bond, opening it up to external investors via tokens called xrETH and xRPL. The ETH and RPL deposits used to mint these tokens are used by the Constellation smart contracts to create new minipools on Rocket Pool which are operated non-custodially by NodeSet operators.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Constellation + Rocket Pool Architecture (simplified)</p></figcaption></figure>

There are three main roles for participants in this system:

1\) Depositors ([xrETH](xreth.md) or [xRPL](xrpl.md) holders)\
2\) Node operators\
3\) Administrator

<figure><img src="https://miro.medium.com/v2/resize:fit:700/0*d24eUDlyiDTya8oE" alt="" height="446" width="700"><figcaption><p>Constellation Internal Architecture (simplified)</p></figcaption></figure>

## Current status <a href="#d4ac" id="d4ac"></a>

**Constellation is approaching its release! Stay tuned for audit and testnet information.**

## &#x20;<a href="#id-5b03" id="id-5b03"></a>

## FAQ <a href="#id-3bc0" id="id-3bc0"></a>

**Since xrETH has better returns, could it replace rETH?**

We view xrETH as an accelerator and extension to the core Rocket Pool protocol because without sufficient rETH demand, xrETH can’t exist. In fact, due to the improving capital efficiency of RP with low-ETH-bonded minipools, it’s mathematically impossible for xrETH to achieve greater liquidity depth/TVL than rETH.

However, there are several potential solutions we’re considering in case growth of both systems stalls due to higher demand for xrETH than rETH. For example, one of the simplest is capping the xrETH deposit pool to prevent the protocol from growing any further. This is still an active area of research, but we are committed to being good actors in our ecosystem, even if that means placing limitations on Constellation’s growth.

**Will Constellation have a governance token?**

There are no plans for a governance token. Constellation is an extension of Rocket Pool and a prelude to building out a wider NodeSet network of opportunity for NOs — it is not a wholly separate protocol with complex governance needs. Generally, we respect the “ungovernance” principle that projects like [Liquity](https://www.liquity.org/) and [Reflexer](https://reflexer.finance/) model for the same reasons that [Vitalik enunciates well here](https://vitalik.ca/general/2021/08/16/voting3.html). As mentioned above, we hope to eventually fully automate and ossify Constellation, and building up governance in the meantime is counterproductive to this goal.

**Why can’t we just add this to Rocket Pool itself?**

This original concept was studied during Rocket Pool’s development, and back then, it was called nETH. However, the lack of sybil-resistance and other tools to combat NO malfeasance prevented the idea’s viability. Put another way, the available tools were incompatible with full permissionless-ness, so Rocket Pool abandoned the idea.

Constellation, however, as a distinct project built on top of the fully permissionless base protocol, has more flexibility to relax permissioning standards and delegate NO onboarding to an independent administrator to perform the required sybil checks. Thus, the tradeoffs for depositors become more clear: if one believes the administrator and NO’s incentive alignment is sufficient, Constellation will offer higher returns via xrETH, and if one disagrees, then rETH is the appropriate token. Either way, since it’s built on top instead of included with the core protocol, if Constellation malfunctions, Rocket Pool’s sublight engines still work just fine.

**What happens to all the new RPL voting power in Constellation?**

Rocket Pool governance is structured so that NOs will simply have more individual voting power if they are a part of Constellation because they will have more RPL staked. As usual, if NOs wish to delegate their Constellation node’s voting power to another address, they may do so. We encourage NOs to delegate to the administrator so that xrETH and xRPL depositors’ interests are represented, but this is optional.

**How does the xrETH price feed work? Is there an oracle?**

Although we can rely on the base protocol to track xRPL price data, xrETH is more challenging. After [EIP-4788](https://eips.ethereum.org/EIPS/eip-4788) goes live with the Deneb Ethereum upgrade, several potential solutions are available. Until then, however, our only option is to use a crypto-economically secured oracle mechanism, which we’ll detail in a future article.

A historical state proof system is likely to be the ultimate solution, but this represents additional engineering challenges. Tooling is improving quickly, though, and we expect to transition to this model as soon as possible.

This topic is already the subject of wider research, as this is essentially the same problem that the oDAO represents for Rocket Pool. RP’s trusted DAO committee is a potential solution for us as well, though undesirable for many of the same reasons.

**What if the administrator does bad stuff?**

There is a whole category of attacks against Constellation by the administrator which we have termed “Bad Admin” attacks. This includes subcategories like “Evil Admin” attacks and “Incompetent Admin” scenarios, for example. These are all the subject of ongoing security research, but there are several ways to design Constellation to avoid any risk of administrator malfeasance. For example:

* Parameter changes and contract upgrades will have a substantial delay so that depositors or NOs can leave the system before they take effect if they disagree
* Rate-limits may be applied to the removal of NOs so that the administrator can’t take over the network without depositors leaving first

As part of the development process, we’re conducting several security analyses, and once this is further along, we’ll open this research up to the public for further review and contribution. In addition to standard security audits from top-tier firms, we will rely on community review and participation in our public beta to ensure safety.

**What does the administrator look like? Is it one person/entity?**

At the moment, we can’t say for sure what the administrator will look like for launch, but we know that its ideal form is a smart contract. This won’t be possible initially, so we anticipate a multi-sig will manually perform the admin duties. The exact make-up of this group depends on a number of factors which we’re still researching.

**How much work has been done so far? Wen launch?!**

Most of the important pre-development research and design work has already been completed, and smart contract development began a few months ago. We estimate that we’re about 50% through this process, but there is a significant amount of off-chain development needed as well. Software development is notoriously difficult to predict, and we have the same growing pains that every startup experiences with fundraising, hiring, and in this industry, the necessary complication of audits. All of this impacts the timeline, so we can’t give a very specific estimate at the moment.

All of that said, **we hope to launch Constellation early in 2024!**
