# Node Operator Policies

This page describes the policies applied to NodeSet node operators. These policies may be updated at any time, and material changes will be announced in advance.

All effectiveness checks referenced below are derived from the reports by the [rated.network](http://rated.network) API.

***

## Applications

Node operators may apply to join NodeSet at [http://nodeset.io/join](http://nodeset.io/join)

If you do not meet the requirements listed below, you can still apply! We reprocess applications on a regular basis, usually every two weeks. This means you may apply even if you don't meet the criteria (or if you are unsure). We will contact you to let you know the initial status of the application and then again if/when your status changes.

### Basic Application Requirements

All applicants must fulfill these requirements to join NodeSet.

1. Operators must maintain at least one solo validator, Rocket Pool validator, or a validator on behalf of another staking protocol/business. This validator must have at least 6 months of continuous operation with a minimum effectiveness rating of 95% over the most recent 90 days.
2. Operators must supply NodeSet with a disaster recovery plan.
3. Operators must pass a live video interview with questions regarding your ability to troubleshoot issues and maintain a node
4. NodeSet will conduct additional manual sybil checks. Further details are not public to preserve the security of this process.
5. Operators must agree to Terms of Service for each service for which they operate.

### Operational Requirements

1. Sufficiently powerful computer hardware to run 50-100 validators with exceptional performance, including future considerations for network upgrades such as EIP-4484 or restaking.
2. Robust monitoring system (e.g. Prometheus + Grafana)
3. Automated notifications from [Beaconcha.in](https://beaconcha.in) or a similar service
4. Remote SSH connection for troubleshooting when away from home (e.g. [Tailscale](https://tailscale.com/))
5. [Rescue Node](https://rescuenode.com/) utilization during pruning (if necessary)

### Required Notifications

All NodeSet operators should set up monitoring and notifications for their nodes. The suggested notifications for [Beaconcha.in](https://beaconcha.in) are selected in the screenshot below. In the future, NodeSet will enroll you in these notifications automatically.

![](https://lh4.googleusercontent.com/\_kLOVnZ8rOn\_UF1V4frgEpLF2dS-6wyYzyHxAhN6J61tppP-oxUzbxLHVNyMKgkXKAAjwjoC\_egmCsnJzvzpBv19gyGGhuYT8M\_XVpAlAjF5e7VirK6TGaONVN-XDqWKuhHP-T4GVDPpGJMfJq2qDsQ)

### Operator Communication Channels

{% hint style="warning" %}
**NodeSet will NEVER contact you through any channel other than the above. NodeSet will NEVER send you a direct message about your node through Discord or other services.**
{% endhint %}

* Email
* Announcements in the #operator-announcement channel of [our Discord server](https://discord.gg/dNshadxVkg)

### Penalty and Ejection Policy

{% hint style="warning" %}
**Ejections from NodeSet are PERMANENT!** If you have an issue with your node, you should reach out to us as soon as possible to ensure you are not ejected. We will work with you to exit your validators or rescue your node to help you avoid ejection.
{% endhint %}

Operators must continuously meet performance requirements to operate with NodeSet. This means that **node operator effectiveness must remain above the minimum threshold of 95% at all times** or they incur a penalty.

Operators who do not meet performance requirements are penalized with strikes and will be ejected immediately after receiving 3 strikes or suffering extended downtime. To account for maintenance and temporary downtime from events outside operator control, strikes reset after 3 months of not receiving any additional strikes. **NodeSet will not make exceptions for any operator for any reason.**

| **Scenario**                          | **Penalty** |
| ------------------------------------- | ----------- |
| Average 1-month effectiveness < 95%   | Strike      |
| Weekly effectiveness >= 70% and < 90% | Strike      |
| Weekly effectiveness >= 50% and < 70% | 2 Strikes   |
| Weekly effectiveness < 50%            | Ejection    |

Operators may also be ejected for behavioral violations, including but not limited to:

* Persistently violating professional and community guidelines
* Being slashed (e.g., double signing attestations)
* MEV theft
* Providing false or misleading information in the application
* Behavior that NodeSet deems detrimental to the network or community
