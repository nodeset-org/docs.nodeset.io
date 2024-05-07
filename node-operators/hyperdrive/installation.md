# Installation

Installing Hyperdrive can be done in two ways: via the `apt` package manager for Debian-based systems, or manually via the CLI (for any Linux or macOS system).

### Via the Package Manager (for Debian-based systems with `apt`)

If your system uses the `apt` package manager, you can install Hyperdrive by enabling our repository.

#### Install Docker

Start by installing Docker for your system following the [Docker installation instructions](https://docs.docker.com/engine/install/).

Next, add your user to the group of Docker administrators:

```
sudo usermod -aG docker $USER
```

Finally, exit the terminal session and start a new one (log out and back in or close and re-open SSH) for the new permissions to take effect.

#### Install Hyperdrive

Update the system packages and install some prerequisites:

```
sudo apt update && sudo apt install curl gnupg apt-transport-https ca-certificates
```

Save the Hyperdrive repository signing key:

```
sudo install -m 0755 -d /etc/apt/keyrings && sudo curl -fsSL https://packagecloud.io/nodeset/hyperdrive/gpgkey -o /etc/apt/keyrings/hyperdrive.asc
```

Add the Hyperdrive repository to your `apt` list:

```
sudo tee -a /etc/apt/sources.list.d/hyperdrive.list << EOF
deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/hyperdrive.asc] https://packagecloud.io/nodeset/hyperdrive/any/ any main
deb-src [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/hyperdrive.asc] https://packagecloud.io/nodeset/hyperdrive/any/ any main
EOF
```

Install Hyperdrive via `apt`:

```
sudo apt update && sudo apt install hyperdrive
```

### Manual Install (for all systems)

If you can't or don't want to use the `apt` process, you can install Hyperdrive manually instead.

1. Download the CLI from [the latest GitHub release](https://github.com/nodeset-org/hyperdrive/releases/latest).&#x20;

Note there are four options: two for Linux and two for Darwin (macOS); both are available for `amd64` and `arm64`. To have parity with the package installer, we recommend saving it to `/usr/bin/hyperdrive`. For example, on an `x64` Linux system, you could do:

```
sudo wget https://github.com/nodeset-org/hyperdrive/releases/latest/download/hyperdrive-cli-linux-amd64 -O /usr/bin/hyperdrive && sudo chmod +x /usr/bin/hyperdrive
```

Make sure you run `chmod +x` on it before trying to use it.

2. Install Hyperdrive via the CLI:

```
hyperdrive service install
```

This will also handle installing all of the dependencies and permissions for you.
