# Best Practices

## Intro

With NodeSet, your node's performance impacts others' rewards. Therefore, [NodeSet requires  strict performance standards for operators](../node-operator-policies.md#penalty-and-ejection-policy). These best practices help you uphold community standards and elevate your operation to a more professional level.

## Notifications

Setting up notifications for your node will immediately notify you if there is an issue so you can fix it faster. Our suggested minimum set of notifications for [Beaconcha.in](https://beaconcha.in) are selected in the screenshot below. In the future, NodeSet will contact you automatically if there is an issue.

![](https://lh4.googleusercontent.com/\_kLOVnZ8rOn\_UF1V4frgEpLF2dS-6wyYzyHxAhN6J61tppP-oxUzbxLHVNyMKgkXKAAjwjoC\_egmCsnJzvzpBv19gyGGhuYT8M\_XVpAlAjF5e7VirK6TGaONVN-XDqWKuhHP-T4GVDPpGJMfJq2qDsQ)

## Monitoring

A monitoring tool stack will help you understand your node's status at a glance and quickly diagnose issues. Please see the following pages for more information:

StakeWise v3: [https://docs.stakewise.io/for-operators/operator-service/monitoring](https://docs.stakewise.io/for-operators/operator-service/monitoring)

Rocket Pool: [https://docs.rocketpool.net/guides/node/grafana](https://docs.rocketpool.net/guides/node/grafana)

## Security and External Access

Setting up external access to your node while preventing unauthorized activity is crucial for performing maintenance while away. [This Rocket Pool documentation page](https://docs.rocketpool.net/guides/node/securing-your-node) will help you secure your node, and [this guide for Tailscale](https://docs.rocketpool.net/guides/node/tailscale) provides instructions for allowing safe access to your node no matter where you are in the world.

## Client Diversity

[See this page for NodeSet's client diversity policy.](./#client-diversity)

## Graffiti

Operators should identify themselves via their graffiti. This helps NodeSet understand our operator network better and will assist you in debugging if there is an issue.

The exact procedure for changing your graffiti depends on your setup. For example, you can use `rocketpool service config` to set your graffiti if you use Rocket Pool to manage your node, or you can look at your eth2 client's documentation if you manage it yourself.
