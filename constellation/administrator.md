# Administrator

## Administrator <a href="#id-5b03" id="id-5b03"></a>

To achieve decentralization goals, Constellation must distribute ETH as thinly and evenly as possible across as large a set of NOs who have a low barrier to entry. Generally, if someone has been validating on RP with a high effectiveness rating, they should expect to be able to join and receive rewards with very little effort involved. However, even though NOs can’t access depositor funds, a broadly open NO set requires safeguards to ensure NOs are accountable to depositors. This is where the administrator comes in.

The administrator is responsible for keeping the system stable and is incentivized to do so via a portion of the rETH commission earned by the protocol (minus the NO share). To fulfill its duty, the administrator can adjust parameters like commission rates and Deposit Pool size, and most importantly, they are responsible for growing and maintaining the Node Operator set.

There is technology in development which will likely allow the administrator role to be fully automated via on-chain mechanisms in the future, such as ZK-ID services and CL/EL communication within Ethereum, but for now this role contains some manual steps. We’re still determining the exact incarnation of the administrator, but as developers, we can articulate some minimum details already. At launch, the administrator will take the form of an off-chain entity, and although the smart contracts will necessarily leave the exact procedures for admitting and kicking NOs to the administrator’s discretion, we expect it will look something like this:

**Admittance Procedure**

1. NO registers their intention to participate with the administrator. This includes proof of ownership of an existing RP node via a signed message from its address.
2. Automatic checks for provided node address are completed, e.g. all minipools on the node must have an appropriate effectiveness level, etc.
3. NO passes a simple sybil check with the administrator, including a short video interview.

**Kick Conditions**

* Node is offline for too long
* Any minipool on the node is slashed

In extreme cases of NO negligence, the administrator can eject an operator and recover any funds assigned to their node via the stored exit messages. Realistically, we expect that there will be rare or no use of this power and that its existence is both an effective deterrent against NO mismanagement and an effective incentive for operators to behave honestly.

It’s also important to note that, like NOs, the administrator has no access to depositor funds, and they only get rewarded by the continuous, stable operation of the protocol. In general, the administrator is conceived as a highly limited role with very serious restrictions on its behavior so as to preserve the integrity of the protocol, including delays in parameter changes and operator on/offboarding. It’s crucial that the administrator role is under severe restrictions to minimize trust for this role until it can be fully removed. As it stands, depositors will have minimal trust assumptions for the administrator, and node operators should only need to trust the administrator will effectively perform sybil checks to keep rewards fair.
