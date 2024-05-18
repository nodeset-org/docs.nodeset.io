# Updating

### Via the Package Manager (for Debian-based systems with `apt`)

If you installed Hyperdrive via the package manager, you simply need to run the following to update it when a new release is out (along with any other system packages that are out of date):

```
sudo apt update && sudo apt dist-upgrade && sudo apt auto-remove
```

### Manual Update (for all systems)

If you installed Hyperdrive manually, start by downloading the new CLI using the same process you followed in step 1 of the [manual installation](installation.md#manual-install-for-all-systems) section.

Once it's downloaded, run the following command:

```
hyperdrive service install -d
```

Note the `-d` flag, which skips the installation of operating system dependencies that you should already have.

### After Updating

Regardless of which method you use to update, you must run `hyperdrive service config` or `hyperdrive service start` for the changes to take effect.
