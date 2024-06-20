---
description: Understanding the status of Hyperdrive
---

# Monitoring Your Node

## `hyperdrive service logs [`_`containerName`_`]`&#x20;

The `service logs` command is used to view logs for each of the components of Hyperdrive.&#x20;

Using this command with no container specified will combine all the logs and is not recommended unless the output is programmatically parsed (e.g. via `grep`).&#x20;

| Container  | Description                                                  | Helpful for...                                    |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------- |
| bn         | Ethereum beacon node client (i.e. Nimbus, Prysm, etc)        | Determining sync status, configuration issues     |
| ec         | Ethereum execution layer client (i.e. Geth, Nethermind, etc) | Determining sync status, configuration issues     |
| prometheus | [Prometheus](https://prometheus.io/) monitoring service      | Diagnosing issues with Prometheus                 |
| grafana    | [Grafana](https://grafana.com/) dashboard service            | Diagnosing issues with Grafana                    |
| exporter   | Collects hardware metrics to forward to Prometheus           | Diagnosing issues with hardware metrics reporting |

## `hyperdrive service daemon-logs`` `_`logName`_

This command requires a specified _logName_ to read:

| Daemon Log Name | Description                                                               | Helpful for...                              |
| --------------- | ------------------------------------------------------------------------- | ------------------------------------------- |
| api             | Handles CLI and API processing                                            | Diagnosing CLI or API errors for Hyperdrive |
| tasks           | Handles automated tasks for Hyperdrive (e.g. authenticating with NodeSet) |                                             |

