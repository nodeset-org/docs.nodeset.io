# Terminology

### **Packages**

On its own, Hyperdrive does not do anything other than provide a CLI and TUI interface, and users are required to install _packages_ that provide meaningful functionality. Currently, there are only two packages available for Hyperdrive: [Constellation](broken-reference) and [StakeWise](../../stakewise-integration/introduction.md).&#x20;

Each package has its own requirements and usage, so make sure to check out the specific documentation for each of the packages you choose to use.

### **Environments**

An _environment_ is an isolated installation of an operating system with one or more pieces of software installed. Because NodeSet currently only supports Linux, an environment in the context of Hyperdrive is usually synonymous with a single Linux installation.

All node operations are made up of at least one environment, and usually they contain two or more.&#x20;

Many users only have one environment installed per computer for the sake of simplicity, but there are several virtualization solutions that allow reuse of the same hardware for multiple environments, typically using the [KVM](https://en.wikipedia.org/wiki/Kernel-based\_Virtual\_Machine) feature of the Linux kernel:

* [Proxmox](https://www.proxmox.com/en/proxmox-virtual-environment/)
* [virt-manager](https://virt-manager.org/)
* [Gnome-boxes](https://wiki.gnome.org/Apps/Boxes)
* [oVirt](https://www.ovirt.org/)

### Nodes

A _node_ is one or more pieces of software necessary for interaction with a particular decentralized network. By default, Hyperdrive will install all the node software necessary for installed packages inside the same environment, but users may choose to connect to external environments instead.

For example, to read or submit a transaction to change the state of the Ethereum network post-merge, both an execution layer client such as Geth, Nethermind, or Besu and a consensus layer client such as Lighthouse or Nimbus must be available. In this context, an Ethereum node is defined as the combination of EL and CL client software.

Sometimes, computers or environments with node software installed are also referred to as a "node".
