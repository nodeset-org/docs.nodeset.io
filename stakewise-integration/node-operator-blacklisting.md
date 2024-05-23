# Node Operator Blacklisting

When NodeSet uploads keys to a StakeWise vault, nodes are responsible for making the deposit transaction to finalize a deposit. Normally, Hyperdrive does this automatically. If there is something wrong with a node, however, this transaction may not be triggered. In this case, to unblock deposits for other operators, this node will be blacklisted by NodeSet and a new list will be uploaded to the vault without that user's keys included.

Users who are blacklisted will receive an email notification and added to a private support channel in our Discord server.

Note that being blacklisted is NOT the same as being expelled from NodeSet entirely. This is a StakeWise-specific status and it will be reversed once the problem is resolved.

#### **Why was I blacklisted?**&#x20;

There are a few reasons this deposit transaction may have not triggered on your end:

* There wasn't enough Ether in your wallet at the time to make the transaction. We recommend keeping \~0.01 ETH per validator in your node wallet to cover gas costs.
* Your node was offline. If your node is offline (network connection issues, system powered down, etc), then it can't make this transaction.
* Your node was not synced properly. If your node isn't synced, it can't make transactions.
* An issue with Hyperdrive itself, which may be resolved by updating Hyperdrive to the latest version or restarting it by running `hyperdrive service stop` and `hyperdrive service start`.

#### How can I determine the issue?&#x20;

First, check the status of each service with `hyperdrive service status` and your service logs with `hyperdrive s l`. If you already have some validators active, you can check their performance by entering the public keys into https://holesky.beaconcha.in (holesky) or https://beaconcha.in (mainnet). If you don't see any obvious problems with your node, please post your StakeWise logs in the #blacklisted channel in our Discord server:

* The StakeWise daemon API and Tasks logs are located in `~/.hyperdrive/logs/stakewise`
* The StakeWise operator log is retrievable with `sudo cp $(docker container inspect hyperdrive_sw_operator -f {{.LogPath}}) ~/sw_operator.log && sudo chmod +r ~/sw_operator.log`
