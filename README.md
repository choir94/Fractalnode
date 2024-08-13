# Fractalnode
## Join Channel Telegram

https://t.me/airdrop_node

# Fractal Bitcoin Node Setup Guide

To ensure smooth requirements:

| Specification        | Details                           |
|----------------------|-----------------------------------|
| **OS**               | Ubuntu 22.04 or later             |
| **RAM**              | Minimum 4 GB                      |
| **Disk Space**       | Minimum 100 GB available          |

## Installation

### Step 1: Install Necessary Packages

Update your system and install the required packages:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl build-essential pkg-config libssl-dev git wget jq make gcc chrony -y
```

### Step 2: Node Installation

#### a. Download the Fractal Node

Get the latest Fractal Node release:

```bash
wget https://github.com/fractal-bitcoin/fractald-release/releases/download/v0.1.6/fractald-0.1.6-x86_64-linux-gnu.tar.gz
```

#### b. Extract the Archive
Unpack the downloaded tar.gz file:

```bash
tar -zxvf fractald-0.1.6-x86_64-linux-gnu.tar.gz
```

#### c. Set Up the Data Directory
Move to the extracted directory and create a data folder:

```bash
cd fractald-0.1.6-x86_64-linux-gnu && mkdir data
```

#### d. Configure the Node
Copy the configuration file to the data directory:

```bash
cp ./bitcoin.conf ./data
```

#### e. Set Up the Service
Create a systemd service for your Fractal Node:

```bash
sudo tee /etc/systemd/system/fractald.service > /dev/null <<EOF
[Unit]
Description=Fractal Node
After=network.target

[Service]
User=root
WorkingDirectory=/root/fractald-0.1.6-x86_64-linux-gnu
ExecStart=/root/fractald-0.1.6-x86_64-linux-gnu/bin/bitcoind -datadir=/root/fractald-0.1.6-x86_64-linux-gnu/data/ -maxtipage=504576000
Restart=always
RestartSec=3
LimitNOFILE=infinity

[Install]
WantedBy=multi-user.target
EOF
```

#### f. Start the Node Service
Reload systemd, enable, and start your Fractal Node service:

```bash
sudo systemctl daemon-reload && \
sudo systemctl enable fractald && \
sudo systemctl start fractald
```

#### g. Verify the Node Logs
Check the service logs to confirm that the node is running correctly:

```bash
sudo journalctl -u fractald -fo cat
```

### Step 3: Create a New Wallet
To create a new wallet, execute the following commands:

```shell
cd /root/fractald-0.1.6-x86_64-linux-gnu/bin
./bitcoin-wallet -wallet=wallet -legacy create
```
This will generate a new wallet named wallet.
![Screenshot_6](https://github.com/user-attachments/assets/42465c83-699e-4069-831d-f0691a79445a)

#### Step 4: Backup Your Private Key
Itms crucial to back up your private key. Use this command to retrieve it:

```shell
bash
Copy code
# Navigate to the Fractal directory
cd /root/fractald-0.1.6-x86_64-linux-gnu/bin

# Dump the wallet's private key to a file
./bitcoin-wallet -wallet=/root/.bitcoin/wallets/wallet/wallet.dat -dumpfile=/root/.bitcoin/wallets/wallet/MyPK.dat dump

# Display the private key in a readable format
cd && awk -F 'checksum,' '/checksum/ {print "Your Wallet Private Key: " $2}' .bitcoin/wallets/wallet/MyPK.dat
```
Store your private key in a secure location.


# Import Your Wallet into Unisat Wallet
Klaim Faucet 
https://explorer.fractalbitcoin.io/faucet
join tesnet
https://app.infinityai.network?ref-code=45008a0c4f0e7939

https://fractal.unisat.io

## Join channel TELEGRAM for diskusi and information

https://t.me/airdrop_node

##thanks




