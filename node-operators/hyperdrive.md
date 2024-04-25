---
description: Hyperdrive is an all-in-one node management system for NodeSet node operators.
---

# Hyperdrive

[https://github.com/nodeset-org/hyperdrive](https://github.com/nodeset-org/hyperdrive)

NodeSet operators use the Hyperdrive client for managing their nodes. This client will&#x20;

### Installation

NodeSet provides packaged versions of each release so operators can manage their installations via the system package manager. If you've never installed Hyperdrive before, you should first add the NodeSet package repository to your package source list.

**E.g. Debian:**

`sudo add-apt-repository 'deb https://packagecloud.io/nodeset/hyperdrive'`

`sudo apt-get update`

`sudo apt-get install hyperdrive`

To finalize the installation, define your configuration by running `hyperdrive service install`, then `hyperdrive service config`.

### Updating

Once installed, the package can be updated via the package manger as usual.

**E.g. for Debian:**

`sudo apt update && sudo apt dist-upgrade && sudo apt autoremove`
