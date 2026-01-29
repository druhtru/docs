---
sidebar_position: 6
---

# Upgrade

## Upgrade v3.3.0 (Tera)
### `Height: 27200000`

```bash
# Stop node
sudo systemctl stop shidod

# Removing the old version
sudo rm /usr/local/bin/shidod
```

# Download & copy binary FOR <i class="fa-brands fa-ubuntu"></i> **UBUNTU 20.04**  (in some cases must be used with **sudo**)
```bash
cd $HOME
curl -L -o shidod https://github.com/ShidoGlobal/shidochain-tera-upgrade/releases/download/tera/shidod
sudo mv shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

# Download & copy binary FOR <i class="fa-brands fa-ubuntu"></i> **UBUNTU 22.04/24** (in some cases must be used with **sudo**).
```bash
cd $HOME
curl -L -o shidod https://github.com/ShidoGlobal/shidochain-tera-upgrade/releases/download/ubuntu24.04/shidod
sudo mv shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

```bash
# Check if the node has been updated
shidod version

Output: 3.3.0

# Start node & check logs
sudo systemctl restart shidod && sudo journalctl -u shidod -f --no-hostname -o cat
```

## Upgrade v3.2.0
### `Height: 23500000`

```bash
# Stop node
sudo systemctl stop shidod

# Removing the old version
sudo rm /usr/local/bin/shidod
```

# Download & copy binary FOR <i class="fa-brands fa-ubuntu"></i> **UBUNTU 20.04**  (in some cases must be used with **sudo**)
```bash
cd $HOME
curl -L -o shidod https://github.com/ShidoGlobal/shido-upgrade-v3.2.0/releases/download/ubuntu20.04/shidod
sudo mv shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

# Download & copy binary FOR <i class="fa-brands fa-ubuntu"></i> **UBUNTU 22.04/24** (in some cases must be used with **sudo**).
```bash
cd $HOME
curl -L -o shidod https://github.com/ShidoGlobal/shido-upgrade-v3.2.0/releases/download/ubuntu22.04/shidod
sudo mv shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

```bash
# Check if the node has been updated
shidod version

Output: 3.2.0

# Start node & check logs
sudo systemctl restart shidod && sudo journalctl -u shidod -f --no-hostname -o cat
```

## Upgrade v3.1.0
### `Height: 17400000`

```bash
# Stop node
sudo systemctl stop shidod

# Removing the old version
sudo rm /usr/local/bin/shidod
```

# Download & copy binary FOR <i class="fa-brands fa-ubuntu"></i> **UBUNTU 20.04**  (in some cases must be used with **sudo**)
```bash
cd $HOME
curl -L -o shidod https://github.com/ShidoGlobal/mainnet-enso-upgrade/releases/download/ubuntu20.04/shidod
sudo mv shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

# Download & copy binary FOR <i class="fa-brands fa-ubuntu"></i> **UBUNTU 22.04/24** (in some cases must be used with **sudo**).
```bash
cd $HOME
curl -L -o shidod https://github.com/ShidoGlobal/mainnet-enso-upgrade/releases/download/ubuntu22.04/shidod
sudo mv shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

```bash
# Check if the node has been updated
shidod version

Output: 3.1.0

# Start node & check logs
sudo systemctl restart shidod && sudo journalctl -u shidod -f --no-hostname -o cat
```

## Upgrade v3.0.0
### `Height: 16850000`

```bash
# Stop node
sudo systemctl stop shidod

# Removing the old version
sudo rm /usr/local/bin/shidod
```

# Update WASWM
```bash
sudo rm /usr/lib/libwasmvm.x86_64.so
sudo wget -O /usr/lib/libwasmvm.x86_64.so https://github.com/CosmWasm/wasmvm/releases/download/v2.1.4/libwasmvm.x86_64.so
sudo ldconfig
```

# Download & copy binary FOR <i class="fa-brands fa-ubuntu"></i> **UBUNTU 20.04**  (in some cases must be used with **sudo**)
```bash
cd $HOME
curl -L -o shidod https://github.com/ShidoGlobal/mainnet-enso-upgrade/releases/download/ubuntu20.04/shidod
sudo cp shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

# Download & copy binary FOR <i class="fa-brands fa-ubuntu"></i> **UBUNTU 22.04/24** (in some cases must be used with **sudo**)
```bash
cd $HOME
curl -L -o shidod https://github.com/ShidoGlobal/mainnet-enso-upgrade/releases/download/ubuntu22.04/shidod
sudo cp shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

```bash
# Check if the node has been updated
shidod version

Output: 3.0.0

# Start node & check logs
sudo systemctl restart shidod && sudo journalctl -u shidod -f --no-hostname -o cat
```

## Upgrade v2.0.0
### `Height: 4303000`

```bash
# Clone new binary
git clone https://github.com/ShidoGlobal/shidoupgrade_v2.0.0.git

# Stop node
sudo systemctl stop shidod

# Removing the old version
sudo rm /usr/local/bin/shidod
```
- Copy binary FOR <i class="fa-brands fa-ubuntu"></i> **UBUNTU 20.04**  (in some cases must be used with **sudo**)
```bash
sudo cp shidoupgrade_v2.0.0/ubuntu20.04build/shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

- Copy binary FOR <i class="fa-brands fa-ubuntu"></i> **UBUNTU 22.04** (in some cases must be used with **sudo**)
```bash
sudo cp shidoupgrade_v2.0.0/ubuntu22.04build/shidod /usr/local/bin/
sudo chmod +x /usr/local/bin/shidod
```

```bash
# Check if the node has been updated
shidod version

Output: 9f5a14a

# Start node
sudo systemctl restart shidod
```