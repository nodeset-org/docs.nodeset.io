# Configuration

To access the configuration menu, use the following command:

```bash
hyperdrive service config
```

### Configuration Wizard

The configuration wizard is automatically opened on first-time configuration, and it may be again accessed later with the button at the bottom of the TUI.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

#### Client Mode

Hyperdrive supports two modes for Ethereum client management: Local and External. With Local mode, Hyperdrive will directly manage your Ethereum client pair locally within the same environment that Hyperdrive is currently installed. Select External mode if you already have an existing Ethereum node which Hyperdrive will use. For more information on this, see [planning-your-node-architecture.md](../best-practices/planning-your-node-architecture.md "mention").

Note that this is not the same as using a Fallback node.

#### Checkpoint Sync

If you're on testnet, we recommend choosing a checkpoint sync [one of the URLs from this list](https://eth-clients.github.io/checkpoint-sync-endpoints/).  For safety, you cannot use a checkpoint sync with mainnet.

#### Fallback Clients

Hyperdrive allows you to use a fallback node in case your primary client pair encounters a problem. If set, Hyperdrive will automatically detect when the primary node is not working and seamlessly switch to the fallback.&#x20;

The best fallback node is another node machine which you trust and maintain yourself. However, in case you don't have your own fallback node, we are working with the [Rescue Node](https://rescuenode.com/) team to adapt their community-run infrastructure to support NodeSet operators. Stay tuned!

#### Package Support

Hyperdrive is a modular system with support for running several services side-by-side. We are currently hard at work building the StakeWise and Constellation packages, with others on the way! To enable support for any of the official packages, simply select them in the configuration wizard.

#### Monitoring / Metrics

With [Grafana](https://grafana.com/) and [Prometheus](https://prometheus.io/) built into Hyperdrive, users can monitor their nodes externally. NodeSet is developing a default dashboard to help operators monitor their node, but users must supply their own for now. For more information, see the documentation for [Grafana](https://grafana.com/docs/grafana/latest/), [Prometheus](https://prometheus.io/docs/introduction/overview/), and the [Rocket Pool monitoring guide](https://docs.rocketpool.net/guides/node/maintenance/overview).

#### Hyperdrive and TX Fees

Hyperdrive allows users to control manual and automatic transaction settings. In the configuration TUI, you can set the maximum gas, priority fees, and other details to ensure your node operates profitably.

#### Configuration Wizard - Savings Settings

In the last step of the configuration wizard, you can Review All Changes, or simply Save and Exit.  After saving and exiting the wizard, you can start Hyperdrive services.  

`Would you like to start the Hyperdrive services automatically now? [y/n]`

Most users should reply `y` to this.

`It looks like this is your first time starting a Validator Client.
Just to be sure, does your node have any existing, active validators attesting on the Beacon Chain? [y/n]`

Based on new configuration, Hyperdrive sees that you haven't started the Validator Client before. To be sure, Hyperdrive asks you to confirm there are no active validators. If this is truly a new install on a fresh system, it's safe to say `y` here.

```
Since your node didn't have any Validator Clients before, Hyperdrive can't determine if you attested in the last 15 minutes.
If you did, it may resubmit an attestation you have already submitted.
This will slash your validator!
To prevent slashing, you must wait 15 minutes from the time you stopped the clients before starting them again.

Press y when you understand the above warning, have waited, and are ready to start Hyperdrive: [y/n]
```

There is a final warning, because Hyperdrive can't determine if you may have been attesting in the last 15 minutes. Again, in a fresh install, it's safe to say `y`.

At this point, the Hyperdrive docker containers will start. The particular containers started will depend upon configuration.

#### Creating the Hyperdrive node wallet

After the containers start, Hyperdrive will check your wallet status. In a fresh installation, it detects that you don't have a wallet and offers to create one. For a new install, respond with `y`. If this installation is part of disaster recovery or migration, choose `n`, as you'll use the recover wallet command instead.

Hyperdrive then walks you through creation of the wallet, presenting the mnemonic, and testing to ensure you saved it.