# Aztec Validator Node - Automated Docker Installer

This automated tool simplifies the process of setting up an Aztec Validator Node using Docker, making it easy to migrate to a new VPS or deploy from scratch.

## One-Click Installation

```bash
rm -rf autoinstall-aztec-docker.sh && wget https://raw.githubusercontent.com/ezlabsnodes/autoinstall/main/autoinstall-aztec-docker.sh && chmod +x autoinstall-aztec-docker.sh && sudo ./autoinstall-aztec-docker.sh
```

## Configuration Parameters

The installer will prompt you to enter the following required information:

- **ETHEREUM_RPC_URL**: Your L1 Execution Layer RPC endpoint
- **CONSENSUS_BEACON_URL**: Your L1 Consensus Layer Beacon RPC endpoint  
- **VALIDATOR_PRIVATE_KEYS**: Your validator's private key (comma-separated if multiple)
- **COINBASE**: Your wallet address (Ethereum address for rewards)

> **Note:** The P2P IP address will be detected automatically by the script.

## Installation Process

1. The script automatically detects your server's P2P IP
2. Creates all necessary configuration files
3. Launches your Aztec validator node in the background using Docker
4. Your node will be ready and running upon completion

## Node Management Commands

### Check Node Logs
```bash
docker logs -f aztec-sequencer
```

### Stop the Node
```bash
docker stop aztec-sequencer && docker rm aztec-sequencer
```

✅ **Installation Complete**

Your Aztec Validator Node is now running and ready to participate in the network!
