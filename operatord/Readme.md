# Operator

`Operatord` is a binary that is used to run the execution environment. It is a simple cosmos sdk application that is used to run the execution environment. It have all the evm execution environment features with some additional features.

## Features

- [x] EVM Execution
- [x] ZkFHE Execution

To Run the operator, you have to follow the steps below:

### 1. Download the operator binary

Download the operator binary from the [binhub repo's release](https://github.com/airchains-network/binhub/releases/download/v0.0.0/operator).

```bash
wget https://github.com/airchains-network/binhub/releases/download/v0.0.0/operatord
chmod +x operatord
```

### 2. Export the environment variables

To run the operator binary you need to export the environment variables.

$HOME/.operatord/zama/keys/network-fhe-keys

```bash
export FHEVM_GO_KEYS_DIR=<PATH_TO_KEYS_DIR>
export TFHE_EXECUTOR_CONTRACT_ADDRESS=<TFHE_EXECUTOR_CONTRACT_ADDRESS>
```

> [!NOTE]
> The `FHEVM_GO_KEYS_DIR` is the path to the keys directory.  
> For keys directory you need to paste your keys which you get from the [keygen](../key-gen/README.md) binary.
> to `$HOME/.operatord/zama/keys/network-fhe-keys` directory.
> 
> The `TFHE_EXECUTOR_CONTRACT_ADDRESS` is the address of the tfhe executor contract.  
> For now you can just use the default address `0x`

