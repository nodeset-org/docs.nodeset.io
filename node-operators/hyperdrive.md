---
description: Hyperdrive is an all-in-one node management system for NodeSet node operators.
---

# Hyperdrive

[https://github.com/nodeset-org/hyperdrive](https://github.com/nodeset-org/hyperdrive)

NodeSet operators use the Hyperdrive client for managing their nodes. It supports all Ethereum consensus and execution clients and features a flexible, modular design to allow multiple services to run side-by-side or across multiple nodes.

NodeSet is working on additional features such as a client SDK, package management, and hardware resource management so that Hyperdrive as the best node management platform

### Installation

NodeSet provides packaged versions of each release so operators can manage their installations via their system package manager. To use Hyperdrive, simply add the NodeSet package repository to your package source list and then install it via the system package manager.

**E.g. Debian:**

`sudo add-apt-repository 'deb https://packagecloud.io/nodeset/hyperdrive'`

`sudo apt-get update`

`sudo apt-get install hyperdrive`

To finalize the installation, install and define a configuration by running `hyperdrive service install`, then `hyperdrive service config`.

If you're running on a testnet and wish to use checkpoint sync, you can use [one of the URLs from this list](https://eth-clients.github.io/checkpoint-sync-endpoints/).

### Updating

Once installed, Hyperdrive can be updated via the package manger as usual.

**E.g. for Debian:**

`sudo apt update && sudo apt dist-upgrade && sudo apt autoremove`

### Recovery

In case of hardware failure, operators may recover their prior wallet via the `hyperdrive wallet recover` command.&#x20;
