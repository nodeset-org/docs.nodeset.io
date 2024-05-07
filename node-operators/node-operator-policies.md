# Node Operator Policies

This page describes the policies applied to NodeSet node operators. These policies may be updated at any time, and material changes will be announced in advance.

All effectiveness checks referenced below are derived from the reports by the [rated.network](http://rated.network) API.

***

### Operator Communication Channels

{% hint style="warning" %}
**NodeSet will NEVER contact you through any channel other than the ones listed below. NodeSet will NEVER send you a direct message about your node through Discord or other services.**
{% endhint %}

* Email
* Announcements in the #operator-announcement channel of [our Discord server](https://discord.gg/dNshadxVkg)

### Penalty and Ejection Policy

{% hint style="warning" %}
**Ejections from NodeSet are PERMANENT!** If you have an issue with your node, you should reach out to us as soon as possible to ensure you are not ejected. We will work with you to exit your validators or rescue your node to help you avoid ejection.
{% endhint %}

Operators must continuously meet performance requirements to operate with NodeSet. This means that **node operator effectiveness must remain above the minimum threshold of 95% at all times** or they incur a penalty.

Operators who do not meet performance requirements are penalized with strikes and will be ejected immediately after receiving 3 strikes or suffering extended downtime. To account for maintenance and temporary downtime from events outside operator control, strikes reset after 3 months of not receiving any additional strikes. **NodeSet will not make exceptions for any operator for any reason other than large, network-level events.**

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
