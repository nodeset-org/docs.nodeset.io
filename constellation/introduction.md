---
description: >-
  Constellation is a protocol built on Rocket Pool which improves its capital
  efficiency and scalability while reducing asset concentration risk -- all
  without compromising on the base security model.
---

# Overview

{% hint style="danger" %}
Constellation has been deprecated due to lack of rETH demand in Rocket Pool. All NodeSet services are now currently provided via our [StakeWise integration](broken-reference).
{% endhint %}

**The Problem**

To be maximally trustless, Rocket Pool requires node operators to post a bond for each validator. This restricts growth by requiring a constant supply of NOs who can afford this bond and leads to an uneven distribution of assets across nodes.

**The Solution**

Constellation liquidizes the NO bond, opening it up to external investors via tokens called xrETH and xRPL. The ETH and RPL deposits used to mint these tokens are used by the Constellation smart contracts to create new minipools on Rocket Pool which are operated non-custodially by NodeSet operators.

<figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Constellation + Rocket Pool Architecture (simplified)</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Sketch of Constellation contract architecture</p></figcaption></figure>

There are four main user roles in this system:

1\) Depositors ([xrETH](xreth.md) or [xRPL](xrpl.md) holders)\
2\) [Node operators](node-operators.md)\
3\) [Administrator](administrator.md)\
4\) [Treasurer](treasurer.md)

## Current status <a href="#d4ac" id="d4ac"></a>

NodeSet has created a testnet deployment of Constellation on Holesky. The Directory contract is located at this address: [0x925D0700407fB0C855Ae9903B3a2727F1e88576c](https://holesky.etherscan.io/address/0x925D0700407fB0C855Ae9903B3a2727F1e88576c)

[Gravita has also launched a deployment of Constellation](https://app.gravitaprotocol.com/constellation/xreth) on Ethereum mainnet. The Directory contract is located at this address: [0x4343743dBc46F67D3340b45286D8cdC13c8575DE](https://etherscan.io/address/0x4343743dBc46F67D3340b45286D8cdC13c8575DE)
