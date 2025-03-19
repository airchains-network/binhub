# Key Generation Binary

A utility for generating cryptographic keys for secure execution environments.

## Overview

This binary facilitates the generation of cryptographic keys essential for your execution environment's security infrastructure. It implements RSA encryption and integrates with a Key Management System (KMS).

## System Requirements

### Directory Structure

```bash
working-directory/
├── config/
│   ├── config.toml    # Configuration file
│   └── public_key.pem # RSA public key
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

| Parameter             | Description                                              | Required |
| --------------------- | -------------------------------------------------------- | -------- |
| `addresses`           | Array of GRPC node endpoints for network connectivity    | Yes      |
| `mnemonic_phrase`     | HD wallet mnemonic for transaction signing               | Yes      |
| `asc_contract`        | Smart contract address for ASC integration               | Yes      |
| `rsa_public_key_path` | Path to RSA public key for identifier encryption         | Yes      |
| `secret_key_id`       | Unique identifier that will be encrypted as KMS key name | Yes      |

## Security Architecture

### RSA Encryption & Key Management System (KMS)

The system implements a two-layer security mechanism:

1. **Secret Key Identifier Protection:**

   - The user provides a secret key identifier
   - This identifier is encrypted using RSA public key (`public_key.pem`)
   - The encrypted identifier serves as a unique KMS key name

2. **KMS Integration:**
   - Each execution environment has its own KMS key
   - The encrypted secret key identifier acts as the KMS key name
   - Without knowing the original secret key identifier, attackers cannot:
     - Identify the correct KMS key name
     - Access the execution environment's KMS key

This architecture ensures that:

- Only authorized users with the correct secret key identifier can access specific execution environment keys
- The relationship between execution environments and their KMS keys remains confidential
- The system maintains secure key isolation between different execution environments

## Usage

Execute the binary in your working directory:

```bash
./keygen
```

## Security Considerations

- Store the `config.toml` file securely
- Never share your mnemonic phrase
- Keep your `secret_key_id` confidential as it's the key to accessing your execution environment's KMS key
- Ensure proper permissions on the `config` directory
