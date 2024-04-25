---
description: >-
  The administrator keeps the system stable by adjusting protocol parameters,
  approving new operators, and ejecting underperforming operators.
---

# Administrator

## Administrator <a href="#id-5b03" id="id-5b03"></a>

Even though operators can’t ever access depositor assets, Constellation's node operator set must be sybil-protected to ensure fair distribution of assets. This is where the administrator comes in.

The administrator is responsible for keeping the system stable, and it is incentivized to do so via a portion of the rETH commission earned by the protocol (minus the NO share). To fulfill its duty, the administrator can adjust parameters like commission rates and the xRPL or xrETH deposit pool sizes, and most importantly, they are also responsible for growing and maintaining a fairly sybil-protected the node operator set.

There is technology in development which will likely allow the administrator role to be fully automated via on-chain mechanisms in the future, such as ZK-ID services and ZK oracles, but for now this role contains some manual steps.

In extreme cases of operator negligence, the administrator can eject that and recover any assets assigned to their node, although like all node operators, **the administrator never has direct access to or custody over any assets**. The administrator will only get rewarded by the continuous, stable operation of the protocol.&#x20;

The administrator is a highly limited role with very serious restrictions on its behavior so as to preserve the integrity of the protocol, including significant delays for many of its actions. Unfortunately, due to the dependency upon the Rocket Pool protocol which is not ossified, Constellation may not be ossified and therefore must allow a method for upgrades, although any proposed changes are heavily delayed in order to allow users plenty of time to exit the protocol if they disagree with changes.

Regardless, depositors have minimal trust assumptions for the administrator, and node operators should only need to trust the administrator will effectively perform sybil checks to keep rewards fair.
