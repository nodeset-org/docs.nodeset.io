---
description: StakeWise reward withdrawals are a multi-step process
---

# Claiming Rewards

#### 1) Submit a Rewards Request

{% hint style="info" %}
Because NodeSet pays the gas for rewards request transactions, operators may only submit rewards requests **once every 3 months.**
{% endhint %}

First, you must submit a request to NodeSet to withdraw rewards on [the StakeWise page on the NodeSet operator dashboard](https://nodeset.io/dashboard/stakewise). NodeSet will then submit a transaction internally to trigger the StakeWise rewards withdrawal process to allocate rewards from the vault to your selected receiver address. However, these rewards will not be transferred or claimable yet.

#### 2) Wait for StakeWise and Ethereum Unstaking

When the rewards allocation begins processing, it takes a minimum of one day, but it may take significantly longer if there is an unstaking queue for Ethereum. After a short period of time StakeWise will provide an estimated date at which the withdrawal will be processed and claimable, and this information is also listed on the NodeSet dashboard.

#### 3) Return and Claim Rewards

Once the allocation from the vault is processed, **you must return to the dashboard** **again** to submit a transaction that will claim the rewards. This will finalize the process and finally move the rewards into your receiver account.

{% hint style="warning" %}
The NodeSet server will only update claim statuses every \~10 minutes. If you submit multiple claim transactions, only the first one will work and the rest will fail!
{% endhint %}

The final transaction must be submitted from the receiver address provided in step (1) or StakeWise will reject the transaction. This means that **you must maintain ownership of the receiver address until the rewards process is complete** so that you can sign the final transaction from it. To ensure success, NodeSet requires that you withdraw your rewards to one of your sign-in addresses.

{% hint style="info" %}
If you wish to claim your rewards to a different address, you must first associate your NodeSet account with that address by signing in with the new address and entering the same email address that you already have registered with your existing NodeSet account.
{% endhint %}

