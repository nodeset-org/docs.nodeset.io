---
description: >-
  xRPL is an RPL liquid staking token which grows in value against RPL based on
  the rate of the Rocket Pool protocol's native RPL emissions
---

# xRPL

#### RPL Staking Rewards

xRPL automatically receives rewards based on the underlying RPL emissions from Rocket Pool. To learn more about how Rocket Pool works and the role of RPL, [please see the Rocket Pool documentation](https://docs.rocketpool.net/).&#x20;

Note that the issuer of xRPL may take a portion of these emissions, so make sure to check with the owner of the Constellation instance you are using to understand their fee structure.

#### Value Accrual Design (not rebasing)

Like xrETH, xRPL uses the [cToken model made famous by Compound](https://docs.compound.finance/v2/ctokens/), where the protocol's exchange rate for xRPL adjusts over time with the value of earned rewards. This model is more gas efficient than a rebasing token, and it may offer tax advantages to users in certain jurisdictions.
