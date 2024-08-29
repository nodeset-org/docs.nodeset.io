# Planning Your Node Architecture

When running multiple services which each require a connection to a full Ethereum node, there are many ways to organize your setup. Broadly, a node operation falls into the category of either an "External" or "Internal" architecture, though hybrid setups are sometimes used. Just like designing a building or computer program, Node Operators should consider their individual needs and plan ahead consciously rather than simply adding more functionality.

For most operators, NodeSet recommends an external architecture with a fallback node using different clients as the most resilient and organized architecture.

{% hint style="info" %}
When planning your setup, remember to create fallback and backup plans! If something goes wrong, what will you do? What if you aren't able to fix the problem remotely?
{% endhint %}

### External

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Three examples of an external node architecture</p></figcaption></figure>

An external node architecture is one where each separate service connects to a single external node, which usually lives on entirely separate hardware within the same network.&#x20;

**Pros**

* High flexibility and security for network setup
* Significantly lower hardware and network requirements
* Easy to support multiple networks (Holesky, Ethereum, etc)

**Cons**

* Without a fallback node, any issue will disable all services

**Choose this if...**

* You only have one or a few machines
* You are comfortable with less resilience in exchange for less impactful downtime
* You want to keep your networking setup simple



### Internal

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt="" width="375"><figcaption><p>An example of an internal node architecture</p></figcaption></figure>

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
