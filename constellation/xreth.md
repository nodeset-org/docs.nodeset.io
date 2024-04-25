---
description: >-
  xrETH is a liquid Ether staking token which receives the same rewards as solo
  staking
---

# xrETH

Functionally, xrETH is very similar to [rETH](https://docs.rocketpool.net/guides/staking/overview#the-reth-token), except it offers the extra advantage of returning the full ETH staking APR. This gives xrETH a similar yield profile to solo staking while remaining liquid.

Also like rETH, xrETH uses the [cToken model made famous by Compound](https://docs.compound.finance/v2/ctokens/) where the protocol's  exchange rate for xrETH will rise over time with the value of earned rewards. This model is more gas efficient than a rebasing token, and it also may offer tax advantages to users in certain jurisdictions.

### Fee Calculations

xrETH is designed to receive the same yield as standard Ethereum staking (including MEV). To achieve this, the ETH exchanged for xrETH is used inside Rocket Pool to create new minipools alongside rETH.

Node operators on Rocket Pool receive the following rewards per ETH bonded:

\`(rETH commission \* ETH staking yield \* 3) + ETH staking yield\`

Constellation reserves an operational fee equal to:

\`rETH commission \* ETH staking yield \* 3\`

For example, if the rETH commission is 14% and the ETH staking yield is 4%, typical RP operators would receive 0.061 ETH/yr per ETH bonded, and xrETH holders would receive 0.04 ETH per/year per ETH deposited.

_Note that it is always more profitable to run a Rocket Pool node with your assets instead of minting xrETH or xRPL. If you are technically capable, please support the network and community by running a Rocket Pool node (and_ [_join NodeSet_](https://nodeset.io/join) _to earn even more)!_
