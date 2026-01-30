---
sidebar_position: 2
---

# Cosmovisor

:::note IMPORTANT:
Instructions for installing cosmovisor on an already running node
:::

## Install cosmovisor
```bash
go install cosmossdk.io/tools/cosmovisor/cmd/cosmovisor@latest
```

## Stop your node and disable service
```bash
sudo systemctl stop shidod
sudo systemctl disable shidod
```

## Delete shido binary
```bash
sudo rm -r /usr/local/bin/shidod
```

### Prepare binaries for Cosmovisor FOR <i class="fa-brands fa-ubuntu"></i> UBUNTU 20.04 (in some cases must be used with sudo)
```bash

cd $HOME

mkdir -p $HOME/.shidod/cosmovisor/genesis/bin

curl -L -o shidod https://github.com/ShidoGlobal/shidochain-tera-upgrade/releases/download/tera/shidod

sudo cp shidod $HOME/.shidod/cosmovisor/genesis/bin/

sudo chmod +x $HOME/.shidod/cosmovisor/genesis/bin/shidod

rm -rf shidod

```

### Prepare binaries for Cosmovisor FOR <i class="fa-brands fa-ubuntu"></i> UBUNTU 22.04/24 (in some cases must be used with sudo)
```bash

cd $HOME

mkdir -p $HOME/.shidod/cosmovisor/genesis/bin

curl -L -o shidod https://github.com/ShidoGlobal/shidochain-tera-upgrade/releases/download/ubuntu24.04/shidod

sudo cp shidod $HOME/.shidod/cosmovisor/genesis/bin/

sudo chmod +x $HOME/.shidod/cosmovisor/genesis/bin/shidod

rm -rf shidod

```

### Create application symlinks
```bash
ln -s $HOME/.shidod/cosmovisor/genesis $HOME/.shidod/cosmovisor/current -f
sudo ln -s $HOME/.shidod/cosmovisor/current/bin/sedashidodd /usr/local/bin/shidod -f
```

## Create service

```bash
sudo tee /etc/systemd/system/shidod.service > /dev/null << EOF
[Unit]
Description=Shido node service
After=network-online.target
[Service]
User=$USER
ExecStart=$(which cosmovisor) run start
Restart=on-failure
RestartSec=10
LimitNOFILE=65535
Environment="DAEMON_HOME=$HOME/.shidod"
Environment="DAEMON_NAME=shidod"
[Install]
WantedBy=multi-user.target
EOF
```

- Enable & Start the service and check the logs

```bash
sudo systemctl daemon-reload
sudo systemctl enable shidod.service

sudo systemctl start shidod
sudo journalctl -u shidod -f --no-hostname -o cat
```

## Future node updates

- You will only need to download the binary file in <span style={{ color: 'orange' }}>"$HOME/.shidod/cosmovisor/upgrades/*upgrade_name*/bin"</span> and cosmovisor will automatically update your node when the update height is reached