# ASC Wasm Contract

This contract is used for secure key management operations in a blockchain environment. It provides a set of cryptographic services including:

- Key generation for creating new encryption keys
- Decryption of encrypted data using stored keys
- Re-encryption to transform encrypted data to be decryptable with different keys
- Common Reference String (CRS) generation for cryptographic operations

The contract implements proof verification mechanisms to ensure security and includes payment validation for data storage based on ciphertext size. It's designed to maintain a secure and auditable record of cryptographic operations through blockchain events and state storage.  
Essentially, it's a Key Management System (KMS) that leverages blockchain technology to provide secure, verifiable cryptographic operations while maintaining transparency through the blockchain's immutable ledger.

## Steps to deploy the contract

> [!WARNING]
> We are assuming that you are in ubuntu or any debian based system.  
> If you are not, We recommend you to use [Docker](https://www.docker.com/) to deploy the contract.  
> Docker Docs are coming soon.

1. Download the contract from the [binhub repo's release](https://github.com/airchains-network/binhub/releases/download/v0.0.0/asc.wasm).
2. Deploy the contract
3. Verify the contract

> [!TIP]
>
> ## Dependencies
>
> - [junctiond](https://github.com/airchains-network/junction/releases/download/v0.3.1/junctiond-linux-amd64) (v0.3.1) : this binary is used for deploying the contract in junction network.
> - [rust](https://www.rust-lang.org/tools/install) : this is used by the junction binary since it contains the wasm module.

### 1. Download the contract

to download the contract, run the following command:

```bash
wget https://github.com/airchains-network/binhub/releases/download/v0.0.0/asc.wasm
```

### 2. Deploy the contract

to deploy the contract, run the following command:

> [!NOTE]
>
> - `<key-name>` is the name of the key to use for the deployment.
> - `<node-rpc-url>` is the url of the node rpc. (ex - `tcp://localhost:26657`)
> - `<keyring-backend>` is the keyring backend to use.

```bash
junctiond tx wasm upload ./asc.wasm --from <key-name> --chain-id varanasi-1 --node <node-rpc-url> --gas-prices 0.25uamf --gas auto --gas-adjustment 1.3 -y --output json --keyring-backend <keyring-backend>
```

### 3. Instantiate the contract

to instantiate the contract, run the following command:

> [!NOTE]
>
> - `<code-id>` is the code id of the contract. You can get it from the previous command.
> - `<key-name>` is the name of the key to use for the deployment.
> - `<node-rpc-url>` is the url of the node rpc. (ex - `tcp://localhost:26657`)
> - `<keyring-backend>` is the keyring backend to use.

```bash
junctiond tx wasm instantiate <code-id> '{"proof_type": "debug", "kms_core_conf": { "centralized": "default" }}' --label "configuration_0" --from <key-name> --output json --chain-id varanasi-1 --node <node-rpc-url> --gas-prices 0.025uamf --gas auto --gas-adjustment 1.3 -y --no-admin --keyring-backend <keyring-backend>
```

You will get the contract address in the response. search for event `instantiate` in the response.
there you will get the contract address in the `attributes` section.

```json
{
  "tx": {
    "body": { body },
    "auth_info": { auth-info },
    "signatures": ["some-signature"]
  },
  "tx_response": {
    "height": "some-height",
    "txhash": "some-txhash",
    "codespace": "",
    "code": 0,
    "data": "...",
    "raw_log": "",
    "logs": [],
    "info": "",
    "gas_wanted": "some-gas-wanted",
    "gas_used": "some-gas-used",
    "tx": {
      "@type": "/cosmos.tx.v1beta1.Tx",
      "body": { body },
    "timestamp": "2025-03-04T09:28:47Z",
    "events": [
      {other-events},
      {
        "type": "instantiate",
        "attributes": [
          {
            "key": "_contract_address",
            "value": "<CONTRACT-ADDRESS>",
            "index": true
          },
          {
            "key": "code_id",
            "value": "some-code-id",
            "index": true
          },
          {
            "key": "msg_index",
            "value": "0",
            "index": true
          }
        ]
      }
    ]
  }
}
```

> [!TIP]
>
> You can use the following command to get the contract address from the response.  
> Just replace `<tx-hash>` with the transaction hash and `<node-rpc-url>` with the node rpc url.
>
> ```bash
> TX_RESPONSE=$(junctiond query tx <tx-hash> --node <node-rpc-url> --output json)
> CONTRACT_ADDRESS=$(echo "$TX_RESPONSE" | jq -r '.events[] | select(.type == "instantiate") | .attributes[] | select(.key == "_contract_address") | .value')
> echo $CONTRACT_ADDRESS
> ```

