# Registering your Node with Constellation

Before beginning, you will need to install the latest beta version of Hyperdrive. Please follow [the Public Beta guide](../../node-operators/hyperdrive/public-betas.md) to install and configure the latest beta release (currently **v1.1.0 Beta 1** ) before proceeding, or the following instructions will not work.

### Enabling Constellation

With Hyperdrive v1.1.0-b1 or higher installed, start by enabling the Constellation module:

1. Run `hyperdrive service config` to configure the service.
2. Navigate to the `Modules` menu.
3. Select the `Constellation` button.
4. Check the `Enable` box.
5. Modify any settings you'd like to change (for example, ports or any additional flags you want to provide to the VC).
6. Press `Esc` twice to return to the main menu.
7. Press `Tab` and select the `Review Changes and Save` button, then save and exit the config TUI.
8. Restart the Hyperdrive service (you will be prompted to do this after exiting the TUI).

You will now see two new Docker containers created: `hyperdrive_cs_vc` and `hyperdrive_cs_daemon`. See the [Overview segment](overview.md#hyperdrive) for more information on these containers.

All of the Constellation module's CLI commands fall under the `hyperdrive constellation ...` prefix. For simplicity, Hyperdrive accepts `hyperdrive cs ...` as an alias for this module. We will use this alias in the documentation moving forward.

### A Note on the Node Wallet

As part of Hyperdrive's initial set up process, you will be asked to create a new wallet (or recover an existing wallet) for your node. Note that Hyperdrive's architecture creates **one wallet** for the whole node. In other words, if you have both the StakeWise and Constellation modules enabled, you use the same node wallet for both of them. You **do not** need to make a new, unique wallet for Constellation that is separate from StakeWise (though you can do so if you wish). This generally makes things like disaster recovery and topping-off with ETH easier since there's only one address to track and only one mnemonic to preserve.

If you need your node's address, you can retrieve it with the following command:

```
hyperdrive wallet status
```

### Funding the Node

Now that Constellation is enabled, it's a good idea to top the wallet off with enough ETH to pay for typical gas costs. With current gas costs of less than 10 gwei, a good comfortable buffer would be approximately 1.1 ETH (1 ETH for the temporary minipool lockup, discussed later, and 0.1 ETH for miscellaneous gas costs).

Fund your wallet with whatever mechanism you are comfortable with. You can use the `hyperdrive wallet status` command again and/or use a chain explorer to view your node's ETH balance for confirmation.

### Registering with Constellation

Now that your node is funded and ready, you can register with the Constellation network. Doing so is simple; just run the following command:

```
hyperdrive cs node register
```

You will first be prompted with the following notice:

```
NOTE:
Your NodeSet account can only have one node registered with Constellation at a time.
Registration requires a special off-chain signature from the Constellation administrator.
If you proceed, Hyperdrive will retrieve this signature for you automatically which will lock this node as your account's Constellation node (even if you aren't ready to submit the registration transaction yet).

Are you ready to assign this node as your account's Constellation node?
```

This refers to [the restriction mentioned in the Prerequisites section](prerequisites.md#important-note-about-node-selection) regarding one Constellation node per user account. Under the hood, registration is a two-step process:

1. Hyperdrive retrieves a special Ethereum signature from the nodeset.io service for registering your node with the Constellation contracts. This is off-chain and does not cost any gas. The very process of retrieving this signature will lock your node in as your user account's Constellation node, so it's important to ensure you want this node to be your Constellation node before proceeding.
2. Hyperdrive then submits that signature to the Constellation smart contracts via an on-chain transaction to register (whitelist) your node with the system. As this is an on-chain transaction, you will need to pay for gas.

When you accept the note, Hyperdrive will retrieve the signature, lock your node in as your user account's Constellation node, and submit the registration transaction to the smart contracts. Once included in a block, your node will be registered with Constellation.

You can verify your registration status at any time with the following command:

```
hyperdrive cs node status
```

After registering, you're ready to start making minipools.
