# Creating and Running Minipools

Constellation extends Rocket Pool with a contract known as the [SuperNodeAccount](https://github.com/nodeset-org/constellation/blob/main/contracts/Constellation/SuperNodeAccount.sol) (the "supernode"). The supernode serves as a registered Rocket Pool node operator, just like every other Rocket Pool node operator in the network; the only thing that makes it special is that it is a smart contract itself, rather than an EOA. When you register your node with Constellation, your node becomes a "subnode" of the supernode - Constellation knows you're a registered node operator, but Rocket Pool does not. All it sees is the supernode as one large monolithic node operator that comprises all of Constellation.

As a note, the supernode is opted into Rocket Pool's [Smoothing Pool](https://docs.rocketpool.net/guides/node/fee-distrib-sp#the-smoothing-pool). This means all subnode operators are automatically opted into it as well. In other words, the Smoothing Pool is a requirement to run in Constellation.

When you create a Constellation minipool, you do so by interacting with the supernode contract. The supernode will perform its own internal bookkeeping, then forward the request on to the Rocket Pool contracts. As far as Rocket Pool is concerned there is nothing special about this minipool: it is just like all of the other minipools on the Rocket Pool network. What makes it a Constellation minipool is purely the fact that it was created under the supernode and it is managed by the Constellation protocol.

All new Constellation minipools have an [8-ETH node operator bond (LEB8s)](https://docs.rocketpool.net/guides/node/create-validator#choosing-a-bond-size).&#x20;

### Prerequisites

Creating a Constellation minipool comes with a few rules:

1. There must be enough RPL and ETH liquidity in both of Constellation's vaults to fund the node operator portion of the bond for a new minipool.
2. Constellation has a contract setting known as the "max validator limit", which is the number of active (non-exited, non-finalized) minipools each node operator is allowed to run at once. You cannot make a new minipool if your node is already at this limit.
3. The Rocket Pool protocol has a setting to disable new minipool creation, which can be toggled in case of a security emergency by the Rocket Pool Security Council. This must be enabled for new minipools to be created, Constellation minipools included.
4. The supernode must have enough RPL staked to allow new minipools to be created. RPL stake rebalancing happens automatically as part of typical protocol operation, but the supernode may be temporarily undercollateralized until rebalancing occurs.
5. Nodeset.io must have signed exit messages uploaded for all of your previous validators.
   1. The first minipool you create is "free" in this sense; the second will require a signed exit from the first before you can create it, and so on.
6. You must have enough ETH in your node wallet to cover the temporary 1 ETH lockup and pay for gas costs.

If all of these conditions are passed, you can proceed to creating a new minipool.

_Note that if the Rocket Pool deposit pool doesn't have enough ETH to fund the depositor portion of the bond for a new minipool, it can be created but it will enter the minipool queue and wait for deposits to be assigned to it._

### Creating a Minipool

To create a new minipool, run the following command:

```
hyperdrive cs minipool create
```

Follow the prompts to verify all of the details, and then accept the confirmation dialog. As part of the creation process, 1 ETH from your node wallet will be temporarily locked in Constellation as insurance to prevent abuse of the [withdrawal credentials exploit](https://github.com/rocket-pool/rocketpool-research/blob/master/Reports/withdrawal-creds-exploit.md).

If you are familiar with [vanity addresses](https://docs.rocketpool.net/guides/node/create-validator#optional-finding-a-custom-vanity-address-for-your-minipool), you can use the following command to find a salt that will create your minipool with a custom address:

```
hyperdrive cs minipool find-vanity-address
```

The underlying salting process is slightly different from the process Rocket Pool uses, so it's important that you do this with Hyperdrive. Salts found by other tools such as the Smart Node won't work properly in Constellation and will result in an address other than the one you were searching for.

### Checking Minipool Status

Once the new minipool is created, you can view its status with this command:

```
hyperdrive cs minipool status
```

This prints information about the minipool on the Execution Layer and its corresponding validator on the Beacon Chain.

As with Rocket Pool, your minipool will first enter the `prelaunch` phase once it's been fully funded. It will then need to wait for 12 hours for the Oracle DAO scrub check (to ensure the withdrawal credential exploit hasn't been abused).

You can view how long the minipool has left before the scrub check is passed by looking at the Constellation daemon task loop logs:

```
hyperdrive service dl cs-tasks
```

After the scrub check is passed, your minipool can be "staked". This is the second deposit required by Rocket Pool which submits the remaining 31 ETH in the minipool to the Beacon Chain deposit contract, thus fully funding the validator. Hyperdrive's tasks loop will perform this automatically for you. If you prefer to do it manually instead, you can run this command:

```
hyperdrive cs minipool stake
```

Either way, once this transaction has been included in a block, the minipool creation process is complete.

### Uploading Signed Exits

To make a second minipool (and beyond), Constellation requires that you first submit a signed exit message for the first minipool's validator to the NodeSet service.

Deposits to the Beacon deposit contract have a relatively long latency before they are observed by the Beacon Chain itself. It can take up to 24 hours after creating a new minipool before the Beacon Chain sees the initial deposit and assigns your validator a unique index.  Signed exit messages use these indices, rather than the validator pubkey, so signed exits for your validator cannot be created and uploaded to the NodeSet service until your initial deposit has been seen by the Beacon Chain and your validator has been assigned an index.

As part of its duties, the Hyperdrive task loop will routinely query your Beacon Node for the status of your new minipool's validator. Once it has been assigned an index, Hyperdrive will automatically create and submit a signed exit message to the NodeSet service. If you prefer to do this manually, you can do so with the following command:

```
hyperdrive cs minipool upload-signed-exits
```

Upon verification of a valid signed exit message, the NodeSet service will enable you to create another minipool.

### Monitoring your Validator Performance

There are several tools at your disposal to view the performance of your node and its validators.

First, you can access the Validator Client logs with the following command:

```
hyperdrive service logs cs_vc
```

Second, you can use [a chain explorer](https://beaconcha.in/) to view the performance of each validator.

### Recovering your Validator Keys

In the event of a disaster, such as accidental deletion of your validator keys or loss of your node hardware, Hyperdrive is able to regenerate your validator keys using your node wallet. As long as you have the mnemonic for you wallet backed up, you will be able to do a full recovery and get back online.

If you need to recover the node wallet, run the following command:

```
hyperdrive wallet recover
```

Once that's done, or if you already have your node wallet and just want to regenerate your validator keys, use this command:

```
hyperdrive cs wallet rebuild
```

This will query the Constellation contracts for the list of all of your active validators and regenerate the keys for each one automatically.

### Exiting your Validators

Should you decide that you no longer want to run a Constellation node, you can submit a voluntary exit for one or more of your validators with the following command:

```
hyperdrive cs minipool exit
```

This will alert the Beacon Chain that you want to gracefully exit and withdraw your staked ETH back to the Execution Layer. As with all validators, you will be put into the Beacon Chain exit queue and will need to keep your validator online and active until your turn in the queue. You can use a chain explorer to easily view this status.
