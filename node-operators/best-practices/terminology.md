# Terminology

### **Packages**

On its own, Hyperdrive does not do anything other than provide a CLI and TUI interface, and users are required to install _packages_ that provide meaningful functionality. Currently, there are only two packages available for Hyperdrive: [Constellation](broken-reference) and [StakeWise](../../stakewise-integration/introduction.md).&#x20;

Each package has its own requirements and usage, so make sure to check out the specific documentation for each of the packages you choose to use.

### **Environments**

An _environment_ is an isolated installation of an operating system with one or more pieces of software installed. Because NodeSet currently only supports Linux, an environment in the context of Hyperdrive is usually synonymous with a single Linux installation.

All node operations are made up of at least one environment, and usually they contain two or more.&#x20;

### Nodes

A _node_ is a special kind of environment (or group of environments) that include all the software necessary for interaction with a particular network. By default, Hyperdrive will install all the node software necessary for installed packages inside the same environment, but users may choose to connect to external environments instead.

For example, to read or submit a transaction to change the state of the Ethereum network post-merge, both an execution layer client such as Geth, Nethermind, or Besu and a consensus layer client such as Lighthouse or Nimbus must be available. In this context, an Ethereum node is defined as the combination of EL and CL client software.
