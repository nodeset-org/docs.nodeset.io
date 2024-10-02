# Public Betas

NodeSet maintains a public beta repository for testing prerelease versions of Hyperdrive. Participation in these betas is voluntary and can be done by any NodeSet operator.

To use public beta versions, you will need to configure Hyperdrive's beta package repository. The instructions are similar to those in [the installation guide](installation.md) but the repository is different.

## Installation via the Package Manager (for Debian-based systems with `apt`) <a href="#via-the-package-manager-for-debian-based-systems-with-apt" id="via-the-package-manager-for-debian-based-systems-with-apt"></a>

If your system uses the `apt` package manager, you can install Hyperdrive betas by enabling the beta repository.

Start by installing and configuring Docker as in [the stable release installation guide](installation.md#install-docker). If you already have a stable version of Hyperdrive installed, you've already done this.

**Configure the Beta Repository**

Update the system packages and install some prerequisites:

```
sudo apt update && sudo apt install curl gnupg apt-transport-https ca-certificates
```

Save the Hyperdrive Beta repository signing key:

```
sudo install -m 0755 -d /etc/apt/keyrings && sudo curl -fsSL https://packagecloud.io/nodeset/hyperdrive-beta/gpgkey -o /etc/apt/keyrings/hyperdrive-beta.asc
```

Add the Hyperdrive Beta repository to your `apt` list:

```
sudo tee -a /etc/apt/sources.list.d/hyperdrive-beta.list << EOF
deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/hyperdrive-beta.asc] https://packagecloud.io/nodeset/hyperdrive-beta/any/ any main
deb-src [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/hyperdrive-beta.asc] https://packagecloud.io/nodeset/hyperdrive-beta/any/ any main
EOF
```

Now, you can install beta version of Hyperdrive via `apt`:

```
sudo apt update && sudo apt install hyperdrive -y
```

Note that if you had a stable release of Hyperdrive already installed, this will upgrade it to the either the latest beta release or the latest stable release - whichever is newer.

If you'd like to target a specific version (e.g., v1.1.0 Beta 1) instead of using the latest version, use the following syntax:

```
sudo apt install hyperdrive=1.1.0~b1
```

After installing a new version, you must edit the configurtation of hyperdrive, review the changes and save it by running:

```
hyperdrive service config
```
Then `Review changes and Save`.

## Manual Install (for All Systems) <a href="#manual-install-for-all-systems" id="manual-install-for-all-systems"></a>

If your system doesn't use `apt` or if you prefer to install beta versions manually, follow the same installation instructions as [the stable release guide](installation.md#manual-install-for-all-systems). The only difference is that instead of using a release version, you can use the GitHub prerelease page for your release of choice.&#x20;
