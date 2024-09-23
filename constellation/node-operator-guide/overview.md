# Overview

The Constellation network has three key components:

* The ETH vault, which stores deposited ETH and mints xrETH in return.
* The RPL vault, which stores deposited RPL and mints xRPL in return.
* Node operators, which take the ETH and RPL from the vaults and put them to work on the Beacon Chain by creating and running Rocket Pool minipools (validators).

This guide serves as an introduction for users that would like to run a Constellation node via the Hyperdrive application. Note that it is a work-in-progress and will be updated as Hyperdrive evolves.

The guide has been updated for **Hyperdrive v1.1.0 Beta 1**.

### Responsibilities

As a Constellation node operator, your primary responsibility is to **earn revenue for the xrETH and xRPL holders**. This revenue comes from running validators on the Beacon Chain as part of the Rocket Pool network, much like regular Rocket Pool node operation. Unlike Rocket Pool node operation, however, you do not need to provide any up-front collateral for your minipools; they are funded entirely by the xrETH and xRPL holders.

Because the token holders fund the minipools, they receive the bulk of the rewards for validation duties. The remainder of the rewards are split between you, the node operator, and the Constellation treasury to fund protocol development. For full details on how Constellation rewards work and the distribution percentages, see the [Node Operators](../node-operators.md) section.

Like regular Rocket Pool node operation, the process is quite similar:

1. Provision your node for validation duties, ensuring the ability to run (or access to your own external) Execution Client and Beacon Node pair. Hyperdrive can handle the configuration and operation of these services for convenience, along with some optional ones like MEV-Boost and performace analysis tools.
2. Register your node with the Constellation network.
3. Create minipools by staking ETH and RPL onto the Rocket Pool network, and ultimately onto the Beacon Chain.
4. Keep them running and earning rewards for as long as you are able.

Unlike regular Rocket Pool node operation, running a Constellation node is not a permissionless endeavor. You must be a whitelisted member of the NodeSet cohort to run a Constellation node and gain access to its ETH and RPL vaults. Accordingly, it's important to ensure that your node is operating efficiently at all times and performing all of its assigned validation duties. Failure to do so and accumulation of excess penalties may result in the forced exiting of your node's minipools and ejection from the cohort. See the [penalty and ejection policy](https://docs.nodeset.io/node-operators/node-operator-policies#penalty-and-ejection-policy) for more information.

### Hyperdrive

The Constellation network has multiple different components, including [smart contracts](https://github.com/nodeset-org/constellation) and an authoritative web service hosted on [https://nodeset.io](https://nodeset.io). NodeSet's [Hyperdrive application](https://docs.nodeset.io/node-operators/hyperdrive) comes with [a Constellation module](https://github.com/nodeset-org/hyperdrive-constellation) that has full support for interacting with all of these components. While it's technically feasible to become a node operator without the use of Hyperdrive, we recommend users install and run it for convenience and consistency when opting to be a Constellation node operator.

The remainder of this guide assumes that users follow this recommendation and explain how to be a Constellation node operator from a Hyperdrive-centric perspective.

Hyperdrive's Constellation module comes with two Docker containers:

* `hyperdrive_cs_daemon`, the module's core service. This provides the underlying API server that the Hyperdrive CLI interacts with, interacts with both the Constellation and Rocket Pool smart contracts, and interacts with nodeset.io when authoritative requests are involved. It also runs the recurring tasks loop, which automatically handles important time-sensitive tasks.
* `hyperdrive_cs_vc`, the Validator Client for your Constellation node. As with all Hyperdrive modules, this Validator Client will run your Constellation validators but will not touch any other validator keys for any other module (such as StakeWise).

Note that you **are allowed to run multiple modules** if you so choose (e.g., you can run StakeWise and Constellation side-by-side on the same machine). As each module has its own Validator Client and its own unique BLS key derivation path, there is **no risk of key overlap or getting slashed** by running both modules together.

### The Process

Becoming a Constellation node operator generally follows this process:

1. Become a whitelisted member of the NodeSet cohort.
2. Prepare a node with Hyperdrive installed and configured, and sync your clients (or have access to externally-managed clients)
3. Enable the Constellation module and register your node with Constellation.
   1. Note that there can only be **one** Constellation node for each user account. If you have multiple nodes whitelisted with your user account, only one of them can participate in Constellation.
4. Create a Constellation minipool and stake it once the Rocket Pool scrub check has passed (Hyperdrive will do the latter for you automatically).
   1. Note that you will need to submit a temporary security bond of 1 ETH until the second deposit (the `stake` transaction) occurs, to protect the network against the [withdrawal credentials exploit](https://github.com/rocket-pool/rocketpool-research/blob/master/Reports/withdrawal-creds-exploit.md). The `stake` transaction will return this bond to you.
   2. You will also need to pay for the gas costs of creating and staking the minipool.
5. Upload a **signed exit message** for your minipool's validator to the nodeset.io service (Hyperdrive will do this for you automatically).&#x20;
6. Repeat steps 4 and 5 as many times as the Constellation contracts allow you to do.
7. Maintain the node until you would like to voluntarily exit your validators, or until they are exited on your behalf by the NodeSet service.&#x20;

### Signed Exit Messages

Aside from not providing the bond for your minipools, another significant difference between Rocket Pool and Constellation node operation is that in Constellation, you must send **signed exit messages** to the nodeset.io service for your validators. These are messages that contain all of the details needed to voluntarily exit your validator, all signed by your validator's private key. The NodeSet service will store them securely but will not upload them to the Beacon Chain unless one of two conditions occur:

1. There is an obvious problem with your node that cannot be resolved via conventional communication, and your validator needs to be exited to protect the validator's bond.
2. Depositors want to exit their xrETH or xRPL positions and require more liquidity than is readily available. In this case the signed exits may be submitted to free up more liquidity after the typical Beacon Chain exit and withdrawal delays.

Of course, you still have the power to voluntarily exit your own validators whenever you like if you so desire. The signed exit message system simply acts as a temporary method to allow "forced exits" until [EIP-7002](https://eips.ethereum.org/EIPS/eip-7002) makes this a canonical feature of the Ethereum protocol.
