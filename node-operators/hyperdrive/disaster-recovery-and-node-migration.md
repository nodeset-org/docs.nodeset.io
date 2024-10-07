---
description: What to do if something goes wrong
---

# Disaster Recovery and Node Migration

{% hint style="info" %}
In all cases, NodeSet recommends operators keep backup hardware ready. If you have a testnet node running, you can use it for mainnet while you diagnose the issue with your other node.
{% endhint %}

## Diagnosing Issues

### If your node is accessible via SSH but is no longer attesting correctly

First, check to [ensure Hyperdrive and your operating system are up to date](updating.md).

Next, you should [check the node logs](monitoring-your-node.md) for errors or other signs of unexpected behavior.

### If you cannot access your node via SSH

First, check the physical hardware for issues, especially your network connection. If it's still running, manually log into the system and attempt to diagnose the issue that way.&#x20;

## Migrating to a New Node

Whether you're upgrading your node hardware or recovering from a problem, migrating to a new node is easy with Hyperdrive.

### If your old node is accessible

The easiest way to migrate to new node hardware is to re-use your old storage drive with new hardware. If there's nothing wrong with your filesystem, you can simply move the old drive over to the new system with no major consequences.

If your filesystem is lost -- due to drive failure, for example -- you should physically destroy the drive before disposal to ensure sophisticated actors cannot recover any private keys from the device. Then, you can begin the wallet recovery process with new hardware using your seed phrase backup.

### Wallet Recovery

Wallet recovery is the process for restoring a node from an offline seed phrase backup. Note that wallet recovery does not recover your configuration, however.

{% hint style="info" %}
To minimize downtime, you should initiate a wallet recovery on new hardware **as soon as you realize the old filesystem is not recoverable.**
{% endhint %}

First, [install Hyperdrive as usual](installation.md) on your new node. When Hyperdrive asks you to create a wallet, reply `n`. This will save you the step of creating and validating a new mnemonic which won't be used. 

Next, use the `hyperdrive wallet recover` command to regenerate your node wallet based on your seed phrase backup. From here, you should review your configuration with `hyperdrive service config` and [monitor the node as usual](monitoring-your-node.md) to ensure it is operational.

### Recovering the StakeWise Module

After you've recovered your wallet, you can enable the StakeWise module in the Hyperdrive Configuration terminal `hyperdrive service config` -> Modules menu.

After exiting the configuration terminal, Hyperdrive asks you to verify you don't have any running validators, and a final verification that if you did have validators running, you've waited 15 minutes, because Hyperdrive can't determine if you attested in the last 15 minutes. Because you're about to regenerate the same keys, this will apply to you, and **you MUST ensure that the node you're recovering hasn't attested in the last 15 minutes or you may be slashed!**

```
NOTE: There is currently no way to remove a validator's deposit data from the NodeSet service once you've uploaded it. The key will be eligible for activation at any time, so this node must remain online at all times to handle activation and validation duties.
If you turn the node off, you may be removed from NodeSet for negligence of duty!

Do you want to continue uploading your deposit data? [y/n]
y

Uploading deposit data to the NodeSet server...
All of your validator keys are already registered (10 in total).
7 are pending activation.
3 have been activated already.
```

After you've enabled the StakeWise module, you need to regenerate your validator keys. The reason for this is that the new Hyperdrive installation currently has no way of knowing how many keys were generated before. Regenerate the same number of keys with `hyperdrive stakewise wallet generate -c X` where `X` is the number of keys to generate. The alias version of this command is `hyperdrive sw w g -c X`.

Hyperdrive will ask if you want to continue uploading your deposit data. Even though it's already been uploaded, it's safe to do this, as Hyperdrive will detect they've already been uploaded, and report back the status.

### Recovering the Constellation Module

After you've recovered your wallet, you can enable the Constellation module in the Hyperdrive Configuration terminal `hyperdrive service config` -> Modules menu.

After exiting the configuration terminal, Hyperdrive asks you to verify you don't have any running validators, and a final verification that if you did have validators running, you've waited 15 minutes, because Hyperdrive can't determine if you attested in the last 15 minutes. Because you're about to regenerate the same keys, this will apply to you, and **you MUST ensure that the node you're recovering hasn't attested in the last 15 minutes or you may be slashed!**

```
The following keys will be rebuilt:
        Minipool: 0xeDa3C8D065B97609Be536bF54fEC757D11D79CD5
        Validator: 0x992b0131967c3bd4e840075e2189c7a6836c5b858ee964e4fdd05a1d3230d9668259fdb3651b5ef63bad06e17b37b330
        Index: 1814204

Are you ready to rebuild these keys? [y/n]
y

Rebuilding 0x992b0131967c3bd4e840075e2189c7a6836c5b858ee964e4fdd05a1d3230d9668259fdb3651b5ef63bad06e17b37b330... done! (2.228147452s)
1 keys have been rebuilt.

Your Constellation Validator Client must be restarted in order to load the validator keys and resume attesting wth them.
Would you like to restart the Constellation Validator Client now? [y/n]
y

Successfully restarted the Constellation Validator Client. Your rebuilt validator keys are now loaded.
```

After you've enabled the Constellation module, you need to rebuild your validator keys. The Constellation module searches for activated keys from the Constellation wallet derivation path, by default from index 0 to index 500. You can rebuild your validator keys with `hyperdrive constellation wallet rebuild`. The alias version of this command is `hyperdrive cs w b`.

## Lost Seed Phrase

All node operators should keep an offline backup of your seed phrase in case of emergency. If you lose your seed phrase but still have access to your old node, the private key for your node wallet is located inside your wallet file, which is typically located at `~/.hyperdrive/data/wallet`

{% hint style="danger" %}
If you lose your seed phrase and no longer have access your old node's filesystem, you should immediately contact NodeSet for help.

**You are at risk of being ejected from NodeSet!**
{% endhint %}

