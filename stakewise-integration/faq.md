# FAQ

#### How are rewards distributed for NodeSet's StakeWise v3 vaults?

The vault fee is split between the vault admin, NodeSet, and operators via smart contracts. The exact portions of each of these are determined by the vault admin. All participating node operators split the operator rewards paid by the vault admin equally, regardless of how many validators they run. This means that NodeSet will limit and order the deposits referred to the vault to help create a more even distribution among participating operators.

#### Who is chosen to be a StakeWise vault operator for NodeSet?

All NodeSet members are eligible for participation, but NodeSet will not add operators to the StakeWise vaults until there are sufficient deposits.

#### What happens if a node operator loses their keys or becomes incapacitated?

There are two main safeguards in place for this. First, the [StakeWise oracle DAO](https://docs.stakewise.io/for-developers/oracles) will automatically exit validators which have a balance lower than 31.8 ETH. Secondly, operators send NodeSet a pre-signed exit message for each of their StakeWise v3 validators, and we can broadcast these messages if an operator loses their keys or becomes incapacitated. These are temporary safety measures which are only necessary until something like [EIP 7002 is included](https://eips.ethereum.org/EIPS/eip-7002) in Ethereum.

Note that even in the case where both NodeSet and our node operators are offline permanently, depositors may still withdraw their assets thanks to the [StakeWise oracle DAO](https://docs-v3.stakewise.io/for-developers/oracles).

#### Why do Node Operators need to pay to register validators?

This is a StakeWise requirement to prevent vaults from being exploited by operators that intentionally create and exit validators at the expense of the vault. Validator registration costs approximately 0.01 ETH at 30 gwei gas and can happen at any time. Even when running the maximum number of validators, ongoing vault activity may cause exits and new registrations, so we recommend operators always keep a minimum balance of 0.1 ETH in their SW node wallet. Payback period for a validator depends on the vault parameters for operator compensation, but as a rule of thumb, it takes operators approximately one week of uptime to repay gas costs for new validator registration.

**Why do I see these warnings in my Hyperdrive logs when running the StakeWise package?**

```
WARNING  There are no available validators in the current deposit data to proceed with registration. To register additional validators, you must upload new deposit data.
```

```
WARNING  Cannot find validator with public key 0x... in keystores.
```

```
WARNING  Deposit data tree root and vault's validators root don't match. Have you updated vault deposit data?
```

StakeWise's client code was not designed to be used with many decentralized operators, so these lines in your logs (i.e. `hyperdrive service logs`) are expected. We are working with the StakeWise team to improve their tooling to support our use-case more gracefully.
