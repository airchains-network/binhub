# GATEWAY SERVICE

The Gateway Service is a critical component responsible for routing requests to the appropriate service within the network. It ensures secure and efficient communication between operators, facilitating the smooth execution of Fully Homomorphic Encryption (FHE) tasks such as decryption and re-encryption.

## Overview

The Gateway Service plays a pivotal role in:

- Establishing and maintaining connections between operators.
- Securely routing requests based on predefined rules.
- Enabling seamless execution of FHE operations.
- Supporting high-performance request handling for encrypted computations.

## System Requirements

### Directory Structure

The directory structure for the Gateway Service should be organized as follows:

```bash
working-directory/
├── config/
│   ├── default.toml    # Connector connection file for the gateway
│   └── gateway.toml    # Gateway configuration file
└── gateway            # Binary executable
```

## Installation

### Step 1: Download the Gateway Service Binary

Download the Gateway Service binary from the official repository:

```bash
wget https://github.com/airchains-network/binhub/releases/download/v0.0.0/operatord
```

### Step 2: Create the Configuration Directory

Create a `config/` directory inside your working directory:

```bash
mkdir -p config
```

### Step 3: Add Configuration Files

Place the following files inside the `config/` directory:

- `default.toml`
- `gateway.toml`

## Configuration Details

### 1. `default.toml` - Connector Configuration

| Parameter   | Description                                           | Source/Example Value                                               |
| ----------- | ----------------------------------------------------- | ------------------------------------------------------------------ |
| `addresses` | Oracle RPC URL for blockchain interaction             | `http://localhost:26657`                                           |
| `addresses` | Blockchain GRPC URL                                   | `http://localhost:9090`                                            |
| `contract`  | Parent ASC contract address for blockchain operations | `"parent_asc_contract_address" (from Airchains)`                   |
| `mnemonic`  | Mnemonic phrase for secure authentication             | `"mnemonic seed phase" (used to create new key in Varanasi chain)` |
| `addresses` | KMS Core URL for key management                       | `"kms-core-url"`                                                   |

### 2. `gateway.toml` - Gateway Configuration

| Parameter                     | Description                                       | Source/Example Value                                                                    |
| ----------------------------- | ------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `oracle_predeploy_address`    | Address for Oracle Predeploy contract             | `"gateway_contract_address" (from deployment_config.json) via operator contract deploy` |
| `relayer_key`                 | Private key used for relaying transactions        | `"relayer_private_key" (from deployment_config.json) via operator contract deploy`      |
| `parent_asc_contract_address` | Parent ASC contract address                       | `"parent_asc_contract_address" (from Airchains)`                                        |
| `asc_contract_address`        | ASC contract address                              | `"asc_contract_address" (deployed in Varanasi chain) via asc-wasm-contract`             |
| `mnemonic`                    | Mnemonic seed phrase for cryptographic operations | `"mnemonic seed phase" (used to create new key in Varanasi chain)`                      |
| `address`                     | Base URL of the KMS service                       | `"http://localhost:9090"`                                                               |
| `url`                         | KV Store base URL                                 | `"kms-kv-store-url"`                                                                    |
| `key_id`                      | Key ID for cryptographic operations within KMS    | `"key_id" (from key_id.txt, generated via keygen)`                                      |

## Usage

To start the Gateway Service, run the following command:

```bash
./gateway
```
