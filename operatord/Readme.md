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

To run the operator binary you need to export these environment variables.

```bash
export FHEVM_GO_KEYS_DIR=<PATH_TO_KEYS_DIR>
export TFHE_EXECUTOR_CONTRACT_ADDRESS=<TFHE_EXECUTOR_CONTRACT_ADDRESS>
```

> [!NOTE]
> The `FHEVM_GO_KEYS_DIR` is the path to the keys directory.  
> For keys directory you need to paste your keys which you get from the [keygen](../key-gen/README.md) binary
> to `$HOME/.operatord/zama/keys/network-fhe-keys` directory.
>
> ```bash
> mkdir -p $HOME/.operatord/zama/keys/network-fhe-keys
> cp ./pks ./sks $HOME/.operatord/zama/keys/network-fhe-keys
> ```
>
> The `TFHE_EXECUTOR_CONTRACT_ADDRESS` is the address of the tfhe executor contract.  
> For now you can just use the default address `0x`

### 3. Run the operator

To run the operator you need setup your operator first by running the `setup.sh` script.  
You can find the script in the [`operatord/setup.sh`](./setup.sh) file.

```bash
./setup.sh
```

After running the setup script you can run the operator binary.

```bash
operatord start --pruning=nothing --trace --log_level info \
    --minimum-gas-prices=0.0001aether \
    --json-rpc.gas-cap=50000000 \
    --json-rpc.api eth,txpool,net,web \
    --rpc.laddr tcp://0.0.0.0:26657
```

### 4. Deploy Contracts

After setting up the operator you have to deploy few contracts to the network.

> [!NOTE]
> These contracts are essential for the operator to work properly for zkFHE related transaction execution.
> Here are the contracts which are required to be deployed:
>
> - ACL Contract (Access Control List)
> - TFHE Executor Contract
> - KMS Verifier Contract
> - Gateway Contract

#### Step 1: Clone the Repository

Clone the `fhevm-contract-deployer` repository from GitHub:

```bash
git clone https://github.com/airchains-network/fhevm-contract-deployer
cd fhevm-contract-deployer
```

#### Step 2: Install Dependencies and Configure Environment Variables

Before deploying the contract, ensure that all dependencies are installed and the required environment variables are configured.

##### Configuration

Create a `.env` file in the root directory of the project with the following parameters:

> [!CAUTION]
> You have to pass the private key of the account which you used to setup the operator.
> basically the one which has the tokens in the wallet from the genesis.
> you can find the private key in the `privkey` file in the operator directory.
>
> ```bash
> cat $HOME_OPERATORD/privkey
> ```
>
> **Mnemonic**
>
> Here the mnemonic is the fresh mnemonic which is gonna be used to deploy the contract.
>
> > **Reason**
> > Since the contracts address has to be computed based on the mnemonic, so we need to use the fresh mnemonic.
>
> **Network URL**
>
> Here you have to pass the rpc url of the network. eg `http://localhost:8545`

```env
NETWORK_URL=
MNEMONIC=
PRIVATE_KEY=
```

| Parameter     | Description                                               | Required |
| ------------- | --------------------------------------------------------- | -------- |
| `NETWORK_URL` | RPC node endpoint for network connectivity                | Yes      |
| `MNEMONIC`    | Mnemonic phrase for contract deployment                   | Yes      |
| `PRIVATE_KEY` | Private key to fund the respective accounts from Mnemonic | Yes      |

Install the required dependencies using the following command:

```bash
npm install
```

Once the dependencies are installed and the environment variables are set, you are ready to deploy the contract.

#### Step 3: Deploy the Contract

To deploy the contract, run the following command:

```bash
node deploy.js
```

The contract will be deployed to the network, and the contract address will be displayed in the console.

### 5. Update TFHE Executor Contract Address

After deployment, update the `TFHE_EXECUTOR_CONTRACT_ADDRESS` using the value from `deployment_config.json`. The file contains the tfhe_executor_contract_address, which must be set before restarting the operator:

```json
{
  "tfhe_executor_contract_address": "0x1234567890abcdef1234567890abcdef12345678"
}
```

update the `TFHE_EXECUTOR_CONTRACT_ADDRESS` environment variable with the new address:

```bash
export TFHE_EXECUTOR_CONTRACT_ADDRESS=0x1234567890abcdef1234567890abcdef12345678
```

### 6. Restart the Operator

After updating the `TFHE_EXECUTOR_CONTRACT_ADDRESS`, restart the operator to apply the changes:

```bash
operatord start --pruning=nothing --trace --log_level info \
    --minimum-gas-prices=0.0001aether \
    --json-rpc.gas-cap=50000000 \
    --json-rpc.api eth,txpool,net,web \
    --rpc.laddr tcp://
```
