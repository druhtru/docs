---
sidebar_position: 1
---


# Node install

## System requirements

- <i class="fa-solid fa-microchip"></i> 4 or more physical CPU cores (**recommended 8 CPU**)
- <i class="fa-solid fa-hard-drive"></i> At least 200GB of NVME SSD disk storage. Hard drive I/O speed is crucial! (**recommended 700GB+ NVMe**)
- <i class="fa-solid fa-memory"></i> At least 8GB of memory (RAM) (**recommended 16GB**)
- <i class="fa-solid fa-globe"></i> **At least 100mbps** network bandwidth

## Dependencies Installation

```bash
sudo apt update
sudo apt install -y curl git jq lz4 wget unzip build-essential
```

```bash
sudo rm -rf /usr/local/go
curl -L https://go.dev/dl/go1.21.6.linux-amd64.tar.gz | sudo tar -xzf - -C /usr/local
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> $HOME/.bash_profile
source .bash_profile
```

## Node Installation

:::warning IMPORTANT:
Choose binary depending on your version of <i class="fa-brands fa-ubuntu"></i> Ubuntu **22.04/24+** or **20.04**
:::

### Download & copy binary FOR <i class="fa-brands fa-ubuntu"></i> UBUNTU 20.04 (in some cases must be used with sudo)
```bash
cd $HOME
curl -L -o shidod https://github.com/ShidoGlobal/mainnet-enso-upgrade/releases/download/ubuntu20.04/shidod
sudo cp shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

### Download & copy binary FOR <i class="fa-brands fa-ubuntu"></i> UBUNTU 22.04/24 (in some cases must be used with sudo)
```bash
cd $HOME
curl -L -o shidod https://github.com/ShidoGlobal/mainnet-enso-upgrade/releases/download/ubuntu22.04/shidod
sudo cp shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

### Download WASM
```bash
wget -O /usr/lib/libwasmvm.x86_64.so https://github.com/CosmWasm/wasmvm/releases/download/v2.1.4/libwasmvm.x86_64.so
sudo ldconfig
```

## Initialize the node for validator

```bash
shidod init YourNodeName --chain-id shido_9008-1
```

## Download genesis

```bash
wget -O genesis.json https://raw.githubusercontent.com/ShidoGlobal/mainnetShidoNodeSync/refs/heads/main/genesis.json --inet4-only
mv genesis.json ~/.shidod/config
```

## Set node CLI configuration

```bash
shidod config set client chain-id shido_9008-1
shidod config set client keyring-backend file
```

- Change timeout_commit

```bash
sed -i 's/timeout_commit = "3s"/timeout_commit = "1s"/g' "$HOME/.shidod/config/config.toml"
```

## Set minimum gas price

```bash
sed -i -e 's|^minimum-gas-prices *=.*|minimum-gas-prices = "0.25shido"|' $HOME/.shidod/config/app.toml
```

## Change laddr

```bash
sed -i -e "s%tcp://127.0.0.1:26657%tcp://0.0.0.0:26657%" $HOME/.shidod/config/config.toml
```

## Set peers (updated: 11.23.2024)

```bash
PEERS=5213f0f690ff199b1c1a0003f51a3eb5ed59fc1b@149.102.132.87:26656,b72f9e195e158dfff0b2b2aaec544f7bb5f26c47@185.230.138.22:26656,e1c3e9aed9ff22e8836ab5b83004a32c566c1b7e@84.247.178.32:26656,d457e45a34167e6280204e50eca332e2dae1305f@38.242.226.17:26656,67d6941dad124364277ccac354cebc92f5fe922d@84.247.178.16:26656,880aec571d22436a213d0888608c71c95b4037cc@84.247.177.232:26656,af8887c18eb6482b99a15f9233009b91aa69a8c3@38.242.228.138:26656,86d71035d6977a8b49bea28c1b20375c0bd90fa7@84.247.182.109:26656,6bd4c6797517f3f590ccedb475c9c27999a80693@185.213.27.103:26656,89b7d60f306e163efcebe3883bd618ba7f886c30@37.187.93.177:26686,9c37022c722b721660ca835fd47c8c32b6d023dd@78.46.174.72:28656,6cd3489a1e753f78878ac60ccefef2247ebc3df0@78.46.88.16:26656,ee6c1ec77a1563f288223b5add67f1e957942127@167.235.12.38:18356,ecfa8fecb479d1e30be4cac20dc8b0f3ef8b761d@167.235.102.45:23656
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.shidod/config/config.toml
```

## Create a service (if needed)

```bash
sudo tee /etc/systemd/system/shidod.service > /dev/null << EOF
[Unit]
Description=Shido node service
After=network-online.target
[Service]
User=$USER
ExecStart=/usr/local/bin/shidod start
Restart=on-failure
RestartSec=10
LimitNOFILE=4096
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

## To speed up synchronization with the network, you can use our [SNAPSHOTS](https://services.256x25.tech/docs/shido/snapshot)
