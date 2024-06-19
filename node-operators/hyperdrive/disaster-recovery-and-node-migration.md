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

First, [install Hyperdrive as usual](installation.md) on your new node.&#x20;

Next, use the `hyperdrive wallet recover` command to regenerate your node wallet based on your seed phrase backup. From here, you should review your configuration with `hyperdrive service config` and [monitor the node as usual](monitoring-your-node.md) to ensure it is operational.

## Lost Seed Phrase

All node operators should keep an offline backup of your seed phrase in case of emergency. If you lose your seed phrase but still have access to your old node, the private key for your node wallet is located inside your wallet file, which is typically located at `~/.hyperdrive/data/wallet`

{% hint style="danger" %}
If you lose your seed phrase and no longer have access your old node's filesystem, you should immediately contact NodeSet for help.

**You are at risk of being ejected from NodeSet!**
{% endhint %}

