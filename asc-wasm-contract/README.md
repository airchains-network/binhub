# ASC Wasm Contract

This contract is used for secure key management operations in a blockchain environment. It provides a set of cryptographic services including:

- Key generation for creating new encryption keys
- Decryption of encrypted data using stored keys
- Re-encryption to transform encrypted data to be decryptable with different keys
- Common Reference String (CRS) generation for cryptographic operations

The contract implements proof verification mechanisms to ensure security and includes payment validation for data storage based on ciphertext size. It's designed to maintain a secure and auditable record of cryptographic operations through blockchain events and state storage.  
Essentially, it's a Key Management System (KMS) that leverages blockchain technology to provide secure, verifiable cryptographic operations while maintaining transparency through the blockchain's immutable ledger.

## Steps to deploy the contract

1. Download the contract from the [ASC Wasm Contract](https://github.com/airchains-network/binhub/asc-wasm-contract/asc.wasm) repository.
2. Deploy the contract
3. Verify the contract
