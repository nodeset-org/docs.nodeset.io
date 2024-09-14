# Planning Your Node Architecture

When running multiple services, there are many ways to organize your operational setup.&#x20;

**For most operators, NodeSet recommends a distributed node architecture with fallback nodes that use different client software** because this represents a maximally resilient and organized architecture.

### Golden Rules

1.  **Do NOT mix personal and professional assets in the same environment**

    For security's sake, you should never put your personal assets in an environment with ANY software which isn't strictly necessary. All software has easy access to the other software in that environment, so for maximum safety, any environment with sensitive information such as a private key should be isolated.
2.  **Do NOT install multiple Hyperdrive instances in same environment**

    Although it is technically possible to do so (with some effort), this is not supported and not recommended.
3.  **Install a firewall for all environments**

    When using a firewall, all incoming and outbound ports must be explicitly defined. This ensures software connections are intentional and not accidental.

### **Types of Operational Architectures**

Broadly, a node operation falls into the category of either a "Distributed" or "Atomic" architecture, though hybrid setups are possible. Just like designing a building or computer program, Node Operators should consider their individual needs and plan ahead consciously rather than simply adding more functionality over time.

{% hint style="info" %}
When planning your setup, remember to create fallback and backup plans! If something goes wrong, what will you do? What if you aren't able to fix the problem remotely?
{% endhint %}

### Distributed

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Three examples of an external node architecture</p></figcaption></figure>

A distributed node architecture is one where each service connects to a single external node which lives in a separate environment.

**Pros**

* High flexibility and security for network setup
* Significantly lower hardware and network requirements
* Easy to support multiple networks (Holesky, Ethereum mainnet, etc)

**Cons**

* Without a fallback node, any issue with the node will disable all connected services

**Choose this if...**

* You only have one or a few machines
* You are comfortable with less resilience in exchange for less impactful downtime
* You want to keep your networking setup simple

### Atomic

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt="" width="375"><figcaption><p>An example of an atomic node architecture</p></figcaption></figure>

An atomic architecture is one where every service is completely isolated, running its own local copy of node software.

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
