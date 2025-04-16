# What's New in v1.2

StakeWise module v1.2 comes with support for [StakeWise v3 vaults](https://docs.stakewise.io/protocol-overview-in-depth/introduction).

One of the major drawbacks of the previous vaults was the queue system; everyone that wanted to participate in the vault would generate their own validator keys, then upload them to NodeSet which would aggregate them all into one big file. This file represented the deposit queue - once assets became available to stake, StakeWise would ask the node owning the key at the top of the list to deposit, then the next one, and so on.

The issue here is that if the person owning the first key _didn't_ deposit for some reason (perhaps their node was misconfigured or they didn't have enough ETH to cover the gas cost of depositing), they would block the entire queue. Nobody could deposit until they did, so they'd hold everyone up. NodeSet circumvented this by implementing a manual blacklisting system, where node operators that were found to be unresponsive would be temporarily removed from StakeWise participation and therefore the queue, so the next person in line could try to deposit.

This blacklisting system, while functional, was not ideal. StakeWise's v3 vaults solve this problem by allowing _anyone_ with permission to use the vault to deposit whenever assets are available, regardless of order. NodeSet.io's permission system has been modified to take advantage of this, allowing any registered node operator to create validators for the vault - up to a maximum number of validators per user. This is similar to the mechanics used in the Constellation module, so if you're a Constellation node operator, you'll feel right at home.
