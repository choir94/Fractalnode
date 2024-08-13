# Fractalnode
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
It’s crucial to back up your private key. Use this command to retrieve it:

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


# Importing Your Wallet into Unisat Wallet

To use your Fractal Bitcoin wallet with Unisat Wallet, follow these instructions:

### 1. Install Unisat Wallet

[Download Unisat Wallet](https://chromewebstore.google.com/detail/unisat-wallet/ppbibelpcjmhbdihakflkdcoccbgbkpo?pli=1) from the Chrome Web Store and open it.

![Unisat Wallet](https://github.com/user-attachments/assets/a5cb92dc-417b-4868-bcbb-68e24e3dd354)

### 2. Access the Settings Menu

Click the wallet name in the top left corner, then click the "+" icon in the top right.

![Settings Menu](https://github.com/user-attachments/assets/116dedbd-a1f8-44cf-b7dd-828d6efe4207)

### 3. Restore Your Wallet Using the Private Key

Select the "Restore from single private key" option.

![Restore from Private Key](https://github.com/user-attachments/assets/ada6a10e-0c6b-4007-8acf-18376100e426)

### 4. Enter Your Private Key

Paste your private key into the input field.

![Enter Private Key](https://github.com/user-attachments/assets/1e61209c-1128-4bd6-a87e-f8ed96924fc6)

### 5. Choose Wallet Type

Make sure to select the "Legacy" option when choosing your wallet type.

![Select Wallet Type](https://github.com/user-attachments/assets/09497321-4475-4831-8ff6-d786d0fe295d)

### 6. Explore Fractal Bitcoin

You can view your transactions and wallet details using the [Fractal Explorer](https://explorer.fractalbitcoin.io/).

---

This guide will help you successfully import your Fractal Bitcoin wallet into Unisat Wallet. Remember to always securely back up your private keys.

## Join channel TELEGRAM for diskusi and information

https://airdrop_node




