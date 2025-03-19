# BinHub

BinHub is a resource repo for all the binary files for ZkFHE Evm Execution Environment.

## Components

### [ASC Wasm Contract](./asc-wasm-contract/README.md)

A secure key management contract implemented in WebAssembly that provides:

- Cryptographic key generation and management
- Secure data encryption/decryption operations
- Re-encryption capabilities
- Common Reference String (CRS) generation
- Blockchain-based proof verification system
- Payment validation for data storage

### [key-gen binary](./key-gen/README.md)

Binary tools for key generation and management in the ZkFHE environment.

## Getting Started

Each component has its own detailed documentation in their respective directories. Please refer to the individual README files for specific installation and usage instructions.

## System Requirements

- Ubuntu or Debian-based system (recommended)
- For ASC Wasm Contract:
  - [junctiond](https://github.com/airchains-network/junction/releases/download/v0.3.1/junctiond-linux-amd64) (v0.3.1)
  - [Rust](https://www.rust-lang.org/tools/install)

For detailed deployment instructions and usage guidelines, please refer to the component-specific documentation.
