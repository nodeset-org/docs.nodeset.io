---
description: >-
  In the event that you lose your StakeWise validator keys and need to
  regenerate them, Hyperdrive makes it easy to recover.
---

# Key Recovery

Start by recovering the Hyperdrive wallet itself from the mnemonic if you haven't already done so:

```
hyperdrive wallet recover
```

Once that's done, you can recover your StakeWise validator keys:

```
hyperdrive stakewise wallet recover-keys
```

This will ask NodeSet.io which keys you have registered already, and procedurally generate validator keys until it finds all of them:

```
The following validator keys have been registered and can be recovered:
Hoodi Dev Vault (0xb163b6d4E1B317F3B4BacE8770d74C1c21C4a131):
	0x94f566037b51b6f6b6a3a676bba6b0b31f83b018327eca47aa2f1baf0b24f5110745a03b11073fddad2277b03ed751ac
	0x810bab09ed301446e04f6d8a28aff39457c8198ac485fb0abb08082d74099791907d2f4b27643276115a5d3fa1102f42
	0xa526d331333773a2b4480121f482ea9bb05d589f4bf594f23e2100bfd36b88660c4e2329a3af36e215bf625cf1f13869
	0x903bee1b9f05c133548f4afae99b7c51cfd1646389a629554a49bf69cb7ce0e4216ee50e3b882a665ca595949fff65aa

NOTE: Key recovering may take a long time. Progress will be printed after checking every 5 keys.
Are you ready to begin key recovery? [y/n]
y

Searching index 0 to 4...
Searching index 5 to 9...
Searching index 10 to 14...
Recovered 0x810bab09ed301446e04f6d8a28aff39457c8198ac485fb0abb08082d74099791907d2f4b27643276115a5d3fa1102f42 (index 11)
Searching index 12 to 16...
Recovered 0x94f566037b51b6f6b6a3a676bba6b0b31f83b018327eca47aa2f1baf0b24f5110745a03b11073fddad2277b03ed751ac (index 12)
Searching index 13 to 17...
Recovered 0xa526d331333773a2b4480121f482ea9bb05d589f4bf594f23e2100bfd36b88660c4e2329a3af36e215bf625cf1f13869 (index 13)
Searching index 14 to 18...
Recovered 0x903bee1b9f05c133548f4afae99b7c51cfd1646389a629554a49bf69cb7ce0e4216ee50e3b882a665ca595949fff65aa (index 14)
Key recovery complete.

Restarting Validator Client to load the recovered keys... done!
Your recovered keys are now loaded.
Your node can now attest for these validators.
```

Note that this will only recover keys that you used for deposits already; it won't all of the keys you ever generated if later ones haven't been used yet. You'll have to create them again with the `hyperdrive stakewise wallet generate-keys` command.
