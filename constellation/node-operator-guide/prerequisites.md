# Prerequisites

Prior to becoming a Constellation node operator, it's prudent to ensure both you and your node are prepared for the responsibilities involved. As with any Beacon Chain validation protocol, this involves both understanding the system and maintaining your validators to the best of your ability.

To become a Constellation node operator, you will need the following:

* A [nodeset.io account](https://nodeset.io/dashboard). Note that you will need to be a whitelisted member of the NodeSet cohort in order to participate.
* A machine capable of acting as an Ethereum node. Generally this requires a stable Internet connection with at least 1.2 TB of data per month (though preferably uncapped), stable electricity, an NVMe SSD with sufficient disk space (at least 512 GB for the Holesky test network, or at least 2 TB for the Ethereum mainnet), at least 16 GB of RAM, and a relatively modern and performant CPU.
  * If you already run Hyperdrive with the StakeWise module, or if you run the Rocket Pool Smart Node, then you already have this.
* Basic experience with the Linux OS, and the ability to use a terminal (or a remote access tool like SSH).
* At least 1 ETH (as a temporary bond for security purposes, explained later), and enough additional ETH to cover the gas costs of Constellation node operation.
  * It costs approximately 2.3 million gas to both deploy and stake a new Constellation minipool. At the time of writing, the gas price is currently 8 gwei; this means each minipool deployment will cost about 0.02 ETH in gas fees. You will likely want to have more than this in your node wallet as a buffer to account for varying gas costs.

### Node Preparation

The process for preparing a node in terms of security posture and Operating System provisioning is currently beyond the scope of this limited documentation; it assumes you already have a node running, or able to run. For details on preparing a node from scratch, we recommend [the comprehensive documentation provided by Rocket Pool](https://docs.rocketpool.net/guides/node/local/overview).

When your node is prepared, [ensure you have Hyperdrive installed](../../node-operators/hyperdrive/installation.md) prior to following the rest of this guide.

### Important Note about Node Selection

For each nodeset.io user account, there can be **only one** Constellation node. If you have multiple nodes whitelisted on your user account, please bear this in mind; you will have to choose one to be your Constellation node, and only that node can create Constellation minipools. You **cannot** split your Constellation duties across multiple nodes. If you want to change your Constellation node to a different node in the future, you will have to contact the NodeSet system administrators and work with them to ensure your old node can no longer be used prior to switching.

Ensure that the node you intent to use for Constellation duties is prepared with the steps above, and proceed to the registration guide next.
