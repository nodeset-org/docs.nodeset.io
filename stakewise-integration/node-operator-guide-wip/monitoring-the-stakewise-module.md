# Monitoring the StakeWise Module

{% hint style="info" %}
This page is specific to StakeWise module monitoring. For an overview of Hyperdrive monitoring in general, see [this page](../../node-operators/hyperdrive/monitoring-your-node.md).
{% endhint %}

## `hyperdrive service logs [`_`containerName`_`]`&#x20;

| Container    | Description                                                                                                                  | Helpful for...                                                                                          |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| sw\_operator | The [StakeWise v3-operator](https://github.com/stakewise/v3-operator) which is maintained by the StakeWise team              | Understanding vault statuses, diagnosing deposit issues                                                 |
| sw\_vc       | A StakeWise-specific validator client instance for the beacon client selected in the Hyperdrive Ethereum node configuration. | Diagnosing validator key errors or connection issues between the StakeWise module and the Ethereum node |

## `hyperdrive service daemon-logs`` `_`logName`_

| Daemon Log Name | Description                                                                              | Helpful for...                                        |
| --------------- | ---------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| sw-api          | Handles CLI and API processing for the StakeWise module                                  | Diagnosing CLI or API errors for the StakeWise module |
| sw-tasks        | Handles automated tasks for StakeWise (e.g. sending pre-signed exit messages to NodeSet) | Diagnosing issues with StakeWise                      |

