# Monitoring the StakeWise Module

{% hint style="info" %}
This page is specific to StakeWise module monitoring. For an overview of Hyperdrive monitoring in general, see [this page](../../node-operators/hyperdrive/monitoring-your-node.md).
{% endhint %}

## Viewing Network Info

```
hyperdrive stakewise network status
```

The list will look like this:

```
Your node is registered with NodeSet.

Hoodi Dev Vault (0xb163b6d4E1B317F3B4BacE8770d74C1c21C4a131):
	Max Validators per User:    4
	Your Registered Validators: 4
	Your Available Validators:  0
	ETH Available for staking:  9872.000000
```

This shows the amount of ETH that's available to be used for new validator deposits in each vault, how many keys each NodeSet operator is allowed to run, how many you currently have, and how many you can still make.

## Viewing Validator Status

To view the status of keys that have been used in deposits already, including their details on the Beacon Chain, use this command:

```
hyperdrive stakewise validator status
```

This produces output like the following:

```
Validator 94f566037b51b6f6b6a3a676bba6b0b31f83b018327eca47aa2f1baf0b24f5110745a03b11073fddad2277b03ed751ac
  Vault: Hoodi Dev Vault (0xb163b6d4E1B317F3B4BacE8770d74C1c21C4a131)
  Seen on Beacon Yet: No

Validator 810bab09ed301446e04f6d8a28aff39457c8198ac485fb0abb08082d74099791907d2f4b27643276115a5d3fa1102f42
  Vault: Hoodi Dev Vault (0xb163b6d4E1B317F3B4BacE8770d74C1c21C4a131)
  Seen on Beacon Yet: No

Validator a526d331333773a2b4480121f482ea9bb05d589f4bf594f23e2100bfd36b88660c4e2329a3af36e215bf625cf1f13869
  Vault: Hoodi Dev Vault (0xb163b6d4E1B317F3B4BacE8770d74C1c21C4a131)
  Seen on Beacon Yet: No

Validator 903bee1b9f05c133548f4afae99b7c51cfd1646389a629554a49bf69cb7ce0e4216ee50e3b882a665ca595949fff65aa
  Vault: Hoodi Dev Vault (0xb163b6d4E1B317F3B4BacE8770d74C1c21C4a131)
  Seen on Beacon Yet: No
```

## Viewing Logs

Since the whole validator request and creation process is handled automatically behind-the-scenes, it's helpful to be able to look at the service logs to see what's happening.

### Operator

The StakeWise operator logs provide useful information to see when new validator requests are detected and made, and their progress. You can access them with this command:

```
hyperdrive service logs sw_operator
```

Here is an example of the logs for a validator request which succeeded:

```
hyperdrive_sw_operator  | 2025-04-16 16:10:07 INFO     Started registration of 1 validator(s)
hyperdrive_sw_operator  | 2025-04-16 16:10:10 INFO     Fetched oracle approvals for validator registration: deadline=1744820407, start index=1131260. Received 11 out of 11 approvals.
hyperdrive_sw_operator  | 2025-04-16 16:10:10 INFO     Submitting registration transaction
hyperdrive_sw_operator  | 2025-04-16 16:10:10 INFO     Waiting for transaction 0x00abbfda64fd40ab779850c6213792b006e0dee0ec6f84b11aede9bd38b74b64 confirmation
hyperdrive_sw_operator  | 2025-04-16 16:10:14 INFO     Successfully registered validator(s) with public key(s) 0x903bee1b9f05c133548f4afae99b7c51cfd1646389a629554a49bf69cb7ce0e4216ee50e3b882a665ca595949fff65aa
```

### Daemon Relay

The portion of the Hyperdrive StakeWise daemon that handles communication with the StakeWise operator is known as the **relay**. The daemon splits its relay logs into a separate file for simplicity, which you can view with this command:

```
hyperdrive service daemon-logs sw-relay
```

### The Validator Client

Looking at the VC logs is useful to explore attestation performance and troubleshooting any issues with Beacon Chain duties:

```
hyperdrive service logs sw_vc
```

