# Best Practices

## Intro

With NodeSet, your node's performance impacts other people's rewards. Therefore, [NodeSet requires  strict performance standards for operators](policies.md#penalty-and-ejection-policy). These best practices help you uphold community standards and elevate your operation to a more professional level.

## Notifications

Setting up notifications for your node will immediately notify you if there is an issue so you can fix it faster. Our suggested minimum set of notifications for [Beaconcha.in](https://beaconcha.in) are selected in the screenshot below. In the future, NodeSet will contact you automatically if there is an issue.

![](https://lh4.googleusercontent.com/\_kLOVnZ8rOn\_UF1V4frgEpLF2dS-6wyYzyHxAhN6J61tppP-oxUzbxLHVNyMKgkXKAAjwjoC\_egmCsnJzvzpBv19gyGGhuYT8M\_XVpAlAjF5e7VirK6TGaONVN-XDqWKuhHP-T4GVDPpGJMfJq2qDsQ)

## Monitoring

A monitoring tool stack will help you understand your node's status at a glance and quickly diagnose issues. Please see the following pages for more information:

StakeWise v3: [https://docs.stakewise.io/for-operators/operator-service/monitoring](https://docs.stakewise.io/for-operators/operator-service/monitoring)

Rocket Pool: [https://docs.rocketpool.net/guides/node/grafana](https://docs.rocketpool.net/guides/node/grafana)



## Security and External Access

Setting up external access to your node while preventing unauthorized activity is crucial for performing maintenance while away. [This Rocket Pool documentation page](https://docs.rocketpool.net/guides/node/securing-your-node) will help you secure your node, and [this guide for Tailscale](https://docs.rocketpool.net/guides/node/tailscale) provides instructions for allowing safe access to your node no matter where you are in the world.



## Plan Your Node Architecture

When running multiple services which each require a connection to a full Ethereum node, there are many ways to organize your setup. Broadly, a node operation falls into the category of either an "External" or "Internal" architecture, though hybrid setups are sometimes used. Just like designing a house or computer program, Node Operators should consider their individual needs and plan ahead consciously rather than simply adding another service.

For most operators, NodeSet recommends an external architecture with a fallback node using different clients as the most resilient and organized architecture.

{% hint style="info" %}
When planning your setup, remember to create fallback and backup plans! If something goes wrong, what will you do? What if you aren't able to fix the problem remotely?
{% endhint %}

### External

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Three examples of an external node architecture</p></figcaption></figure>

An external node architecture is one where each separate service connects to a single external node, which usually lives on entirely separate hardware within the same network.&#x20;

**Pros**

* High flexibility and security for network setup
* Significantly lower hardware and network requirements

**Cons**

* Without a fallback node, any issue will disable all services

**Choose this if...**

* You only have one or a few machines
* You are comfortable with less resilience in exchange for less impactful downtime
* You want to keep your networking setup simple



### Internal

<figure><img src="../.gitbook/assets/image (2).png" alt="" width="375"><figcaption><p>An example of an internal node architecture</p></figcaption></figure>

An internal architecture is one where every service is completely isolated, running its own local copy of a full node.

**Pros**

* High-redundancy setup means fewer cascading failures

**Cons**

* More complicated network setup (each node requires its own peering ports, etc)
* High hardware requirements
* Downtime is longer in case of a node failure

**Choose this if...**

* Hardware and network requirements are not a concern
* You prefer redundancy even with the risk of longer downtime
* You have no problem managing a complex network setup
