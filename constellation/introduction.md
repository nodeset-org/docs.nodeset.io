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

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Constellation + Rocket Pool Architecture (simplified)</p></figcaption></figure>

There are three main roles for participants in this system:

1\) Depositors ([xrETH](xreth.md) or [xRPL](xrpl.md) holders)\
2\) Node operators\
3\) Administrator

<figure><img src="https://miro.medium.com/v2/resize:fit:700/0*d24eUDlyiDTya8oE" alt="" height="446" width="700"><figcaption><p>Constellation Internal Architecture (simplified)</p></figcaption></figure>

## Current status <a href="#d4ac" id="d4ac"></a>

**Constellation is approaching its release! Stay tuned for audit and testnet information.**
