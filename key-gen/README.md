# Key Generation Binary

A utility for generating and managing secure keys for execution environments.

## Overview

This binary handles secure key generation and management for your execution environment, integrating with a robust key management infrastructure.

## System Requirements

### Directory Structure

```bash
working-directory/
├── config/
│   ├── config.toml    # Configuration file
│   └── public_key.pem # Public key for encryption
└── keygen            # Binary executable
```

## Installation

### 1. Download Binary

```bash
wget https://github.com/airchains-network/binhub/releases/download/v0.0.0/keygen
chmod +x keygen  # Make binary executable
```

### 2. Set Up Public Key

```bash
wget https://github.com/airchains-network/binhub/releases/download/v0.0.0/public_key.pem
mkdir -p config && cp public_key.pem config/public_key.pem
```

## Configuration

Create a `config.toml` file in the `config` directory with the following parameters:

| Parameter             | Description                                  | Required |
| --------------------- | -------------------------------------------- | -------- |
| `addresses`           | GRPC node endpoints for network connectivity | Yes      |
| `mnemonic_phrase`     | Mnemonic for transaction signing             | Yes      |
| `asc_contract`        | Contract address for chain integration       | Yes      |
| `rsa_public_key_path` | Path to the public key file                  | Yes      |
| `secret_key_id`       | Unique identifier for your environment's key | Yes      |

## Security Notes

- The system uses industry-standard encryption protocols
- Each execution environment maintains its own isolated key space
- Access to keys is strictly controlled through secure identifiers

## Usage

Execute the binary in your working directory:

```bash
./keygen
```

## Security Best Practices

- Keep your configuration files secure
- Never share your mnemonic phrase
- Maintain confidentiality of your `secret_key_id`
- Use appropriate file permissions
