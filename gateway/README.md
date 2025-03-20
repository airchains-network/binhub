# GATEWAY

This is the gateway service. It is responsible for routing requests to the appropriate service.

## Overview

The Gateway Service is a crucial component responsible for routing requests to the appropriate service within the network. It facilitates secure and efficient communication between operators, ensuring smooth execution of Fully Homomorphic Encryption (FHE) tasks such as decryption and re-encryption.

## Functionality

The Gateway Service is designed to:

- Establish and maintain connections between operators
- Securely route requests based on predefined rules
- Enable seamless execution of FHE operations
- Support high-performance request handling for encrypted computations

## System Requirements

### Directory Structure

```bash
working-directory/
├── config/
│   ├── default.toml    # connector connection file for the gateway
│   └── gateway.toml    # gateway configuration file
└── gateway            # Binary executable
```

### Installation

To install the Gateway Service, follow these steps:

1. Download the Gateway Service binary executable from the repository.
2. Create a `config` directory in the working directory.
3. Add the `default.toml` and `gateway.toml` configuration files to the `config` directory.
4. Run the Gateway Service binary executable.

```bash
wget https://github.com/airchains-network/binhub/releases/download/v0.0.0/operatord
```

### Configuration

The Gateway Service requires the following configuration settings:

create a `config` directory in the working directory and add the following configuration files: `default.toml` and `gateway.toml`.
