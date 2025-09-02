---
description: >-
  Learn the technical details behind creating non-custodial validators for
  NodeSet-powered StakeWise vaults
---

# How it Works

## Components

The module has three services (Docker containers):

* `sw_operator` is the [StakeWise v3 Operator](https://github.com/stakewise/v3-operator?tab=readme-ov-file#what-is-v3-operator) service. It is StakeWise's node operator service that communicates with the StakeWise oracle network to submit new validator creation requests.
* `sw_daemon` is the Hyperdrive daemon for StakeWise. It manages your validator keys, coordinates between the operator service and NodeSet.io to launch new validators when available, and interacts with the CLI during command requests.
* `sw_vc` is the Validator Client used to run your StakeWise validators. Remember that each module has its own VC to isolate it from keys belonging to other modules and ensure the correct fee recipient is used.

## Process Overview

Here is a brief overview of how the new StakeWise module works.

1. You generate some validator keys in advance. You can make as many as you want; the module will use them in order as new deposits can be made.
   * Note that these keys will be loaded into your Validator Client upon generation, even though they haven't been used yet. This will allow your node to automatically start validating with them as soon as they are activated.
2. ETH gets deposited into the StakeWise vault.
3. The StakeWise operator makes a request for new validators to deposit.
4. The Hyperdrive StakeWise daemon coordinates with NodeSet.io to verify that your node is eligible for new validators.
   * If you don't have any available keys ready for depositing, this process will stop. It's important to make sure you always have extra keys ready to handle new deposits!
   * If you have keys and are eligible for more deposits, it produces deposit data and signed exit messages for as many as it is allowed to make.
5. NodeSet.io signs off on these artifacts and adds each validator you created to its database. This allows you to see which keys it currently has, which is helpful for validator key recovery (discussed later).
6. The daemon provides the artifacts back to the StakeWise operator.
7. The operator bundles the artifacts together and submits a validator approval request to the StakeWise oracles.
8. The oracles verify the deposit information and approve the request.
9. The operator submits a transaction with all of the information.
10. As long as nobody has front-run you and deposited before you, your deposits will be processed and your validators will be added to the Beacon Chain's activation queue.
    * StakeWise's system keys on the deposit root - a value that changes any time a new deposit is made to the Beacon deposit contract. It requires that the deposit root doesn't change throughout that entire process; in other words, in order for your deposit to succeed, there can be no other deposits during the window between a new validator request and deposit transaction submission.
    * If a deposit is made that changes the deposit root before your transaction is processed, your transaction will revert and your validators will not be added.
    * Hyperdrive handles this situation by reusing such validator keys for subsequent deposit attempts automatically.
