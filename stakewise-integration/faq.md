# FAQ

#### How are rewards distributed for NodeSet's StakeWise v3 vaults?

The vault fee is split between the vault admin, NodeSet, and operators via smart contracts. The exact portions of each of these are determined by the vault admin. All participating node operators split the operator rewards paid by the vault admin equally, regardless of how many validators they run. This means that NodeSet will limit and order the deposits referred to the vault to help create a more even distribution among participating operators.

#### Who is chosen to be a StakeWise vault operator for NodeSet?

All NodeSet operators are eligible for participation.

#### What happens if a node operator loses their keys or becomes incapacitated?

There are two main safeguards in place for this. First, the [StakeWise oracle DAO](https://docs.stakewise.io/for-developers/oracles) will automatically exit validators which have a balance lower than 31.8 ETH. Secondly, operators send NodeSet a pre-signed exit message for each of their StakeWise v3 validators, and we can broadcast these messages if an operator loses their keys or becomes incapacitated. These are temporary safety measures which are only necessary until something like [EIP 7002 is included](https://eips.ethereum.org/EIPS/eip-7002) in Ethereum.

Note that even in the case where both NodeSet and our node operators are offline permanently, depositors may still withdraw their assets thanks to the [StakeWise oracle DAO](https://docs-v3.stakewise.io/for-developers/oracles).

#### Why do Node Operators need to pay to register validators?

This is a StakeWise requirement to prevent vaults from being exploited by operators that intentionally create and exit validators at the expense of the vault. Validator registration costs approximately 0.0003 ETH with a 1 gwei gas price and may happen at any time. Even when running the maximum number of validators, ongoing vault activity may cause exits and new registrations, so we recommend operators always keep a minimum balance of 0.01 ETH in their SW node wallet. The payback period for a validator depends on the vault parameters for operator compensation, but usually, it only takes operators approximately a week or two of uptime to repay gas costs for new validator registration.
