---
description: Hyperdrive can be installed beside a [RocketPool stack](http://docs.rocketpool.net/guides/node/) on the same node.
---


# Hybrid Local installation

This guide will cover the case where Rocket Pool is already installed on Linux host with the [docker method](https://docs.rocketpool.net/guides/node/docker#creating-a-standard-rocket-pool-node-with-docker) and [hyperdrive should be installed beside it](./installation.md)

Once this is done, here are the additional instructions to follow.

## Modification to Rocket Pool

### In the `rocketpool s c` menu:

1. Go to `Execution Client (ETH1)` and set `Expose RPC ports` to `Open to Localhost`:

<img width="463" alt="Screenshot 2024-10-04 at 10 06 24" src="https://github.com/user-attachments/assets/c6585f61-fe6b-44d4-8996-e674d79dec46">

2. Go to `Execution Client (ETH2)` and set `Expose API port` to `Open to Localhost`:
 
<img width="463" alt="image" src="https://github.com/user-attachments/assets/9be95351-51fa-4c96-a443-fbed2bcf3d4b">


Then save and quit.

### In the `hyperdrive s c` menu

1. In `Hyperdrive and TX fees`, the `Additional Docker Networks` should be set to `rocketpool_net`:

<img width="463" alt="image" src="https://github.com/user-attachments/assets/7cfcc36d-6d91-41ea-a913-69837fb506a1">

2. In `Execution Client`, the `Client Mode` should be set to `Externally Managed`, the `HTTP URL` set to `http://rocketpool_eth1:8545` and the `Websocket URL` set to `ws://rocketpool_eth1:8546`:

<img width="463" alt="image" src="https://github.com/user-attachments/assets/4f9e65f0-1ca4-4a6c-9994-b265b9412e04">

3. In `Beacon Node`, the `Client Mode` should be set to `Externally Managed`, the `HTTP URL` set to `http://rocketpool_eth2:5052`

<img width="463" alt="image" src="https://github.com/user-attachments/assets/173ae33a-7545-453b-8aa2-4b4c6ce6fb22">

4. `MEV-Boost` should be disabled:

<img width="468" alt="Screenshot 2024-10-04 at 10 04 48" src="https://github.com/user-attachments/assets/6ec5f7f4-9782-40c0-8452-9b3776451daf">

Then save and quit, answer `yes` when restarting the services is proposed.

### Verification

Your RocketPool installation should be in sync:

```
~$ rocketpool n y

Your Smart Node is currently using the Holesky Test Network.

Your consensus client is on the correct network.

Your primary execution client is fully synced.
You do not have a fallback execution client enabled.
Your primary consensus client is fully synced.
You do not have a fallback consensus client enabled.
```

And after some time, your hyperdrive client too:

```
~$ hp s y

Hyperdrive is currently using the Holesky Test Network.

Your primary execution client is fully synced.
You do not have a fallback execution client enabled.
Your primary beacon client is fully synced.
You do not have a fallback beacon client enabled.
```
