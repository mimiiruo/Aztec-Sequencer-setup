# 👨🏻‍💻 Aztec Sequencer Guide 👨🏻‍💻

## 🖥️ System Requirements

### Pre-Requirements 🛠️
- **Docker & Docker Compose**
- **Aztec Tool**
- **Sepolia RPC URL**
- ⚠️ **Note**: Let Docker run in background if using local device

---

## 🚀 Installation Steps

### Step 1: Update System
```bash
sudo apt-get update && sudo apt-get upgrade -y
```

### Step 2: Install Node.js
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash - && sudo apt update && sudo apt install -y nodejs
```

### Step 3: Install Required Packages
```bash
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev screen ufw -y
```

### Step 4: Install Docker & Docker Compose
```bash
# Update package index and install prerequisites
sudo apt update && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common

# Add Docker's official GPG key
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Add Docker repository
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker
sudo apt update && sudo apt install -y docker-ce && sudo systemctl enable --now docker

# Add user to docker group
sudo usermod -aG docker $USER && newgrp docker

# Install Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/$(curl -s https://api.github.com/repos/docker/compose/releases/latest | jq -r .tag_name)/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose && sudo chmod +x /usr/local/bin/docker-compose
```

### Step 5: Verify Docker Installation
```bash
docker --version && docker-compose --version
```

### Step 6: Install Aztec CLI
```bash
bash -i <(curl -s https://install.aztec.network)
```

### Step 7: Configure Shell/Path
```bash
echo 'export PATH="$HOME/.aztec/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

### Step 8: Verify Aztec Installation
```bash
aztec -h
```

### Step 9: Set Correct Version for Testnet
```bash
aztec-up 1.1.2
```

---

## 🌐 Network Configuration

### Load Wallet with Sepolia Faucet
Get Sepolia ETH from these faucets:
- [Sepolia Faucet (pk910)](https://sepolia-faucet.pk910.de/)
- [Alchemy Sepolia Faucet](https://www.alchemy.com/faucets/ethereum-sepolia)

### Configure Firewall
```bash
sudo ufw allow 22
sudo ufw allow ssh
sudo ufw enable
sudo ufw allow 40400
sudo ufw allow 8080
```

---

## 🔑 Get Sepolia and Beacon API Keys (Free)

### Method 1: Primary Source
1. **Go to**: [https://tinyurl.com/y8v7tm2d](https://tinyurl.com/y8v7tm2d)
2. **Sign up manually** with email address (you'll receive $100 voucher)
   - ⚠️ **Don't sign up with Google**
3. **Select Ethereum Sepolia**
4. **Scroll down** and select Growth Plan for the RPC you need (Sepolia or Beacon)
5. **Click Select Voucher**
6. **Select $50 Voucher**
7. **Click Pay with Balance**
8. **Your API key** will be available in the API section

### Alternative Sources
- [drpc.org](https://drpc.org/dashboard)
- [MetaMask Developer](https://developer.metamask.io/key/active-endpoints)
- [Alchemy](https://www.alchemy.com)

---

## 🍥 Start Your Sequencer

### Step 1: Create Screen Session
```bash
screen -S aztec
```

### Step 2: Start Your Node

⚠️ **Important**: Make the necessary replacements before executing:

```bash
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls Eth_Sepolia_RPC \
  --l1-consensus-host-urls Eth-beacon_sepolia_RPC \
  --sequencer.validatorPrivateKeys 0xYourPrivateKey \
  --sequencer.coinbase YourAddress \
  --p2p.p2pIp Your_ip
```

### 🔧 Required Replacements:

| Parameter | Replace With | Example |
|-----------|--------------|---------|
| `Eth_Sepolia_RPC` | Your actual Sepolia RPC URL | `https://sepolia.infura.io/v3/YOUR_API_KEY` |
| `Eth-beacon_sepolia_RPC` | Your actual Beacon Sepolia RPC URL | `https://sepolia-beacon.infura.io/v3/YOUR_API_KEY` |
| `0xYourPrivateKey` | Your EVM wallet private key | `0x1234567890abcdef...` |
| `YourAddress` | Your EVM wallet address | `0x742d35Cc6635C0532...` |
| `Your_ip` | Your external IP address | Use: `curl ifconfig.me` |

### 📝 Important Notes:
- ⚠️ **Don't forget** the `0x` prefix for your private key
- **Initial download and sync** will take some time
- **Keep your private key secure** and never share it

---

## 🔧 Useful Commands

| Command | Description |
|---------|-------------|
| `screen -ls` | List all screen sessions |
| `screen -r aztec` | Reattach to Aztec screen session |
| `Ctrl + A + D` | Detach from screen session |
| `curl ifconfig.me` | Get your external IP address |
| `docker ps` | Check running Docker containers |

---

## 🆘 Troubleshooting

### Common Issues:

1. **Docker permission denied**:
   ```bash
   sudo usermod -aG docker $USER
   newgrp docker
   ```

2. **Aztec command not found**:
   ```bash
   source ~/.bashrc
   echo $PATH
   ```

3. **Node sync issues**:
   - Check your RPC URLs are working
   - Ensure firewall ports are open
   - Verify your private key format (with 0x prefix)

4. **Screen session lost**:
   - Check with `screen -ls`
   - Recreate with `screen -S aztec`

---

## ⚠️ Security Warnings

- **Never share your private key** with anyone
- **Use a dedicated wallet** for sequencer operations
- **Keep your system updated** regularly
- **Monitor your node** for any unusual activity

---

*Guide created by Ez Labs Nodes*
