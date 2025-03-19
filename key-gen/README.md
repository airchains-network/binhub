# Key Generation Binary

Key generation binary is used to generate the keys for your execution environment.

> [!IMPORTANT]
>
> ## Prerequisites Configuration
>
> Before you start, you need to configure the `config.toml` file. Please create a config directory and put the `config.toml` file in it.
> Remember to put the config directory in the same directory as the binary.  
> Here is how the folder structure should look like:
>
> ```bash
> working-directory/
> ├── config
> │   ├── config.toml
> │   └── public_key.pem
> └── keygen(binary)
> ```

## Download the binary

You can download the binary from [here](https://github.com/airchains-network/binhub/releases/download/v0.0.0/keygen)

```bash
wget https://github.com/airchains-network/binhub/releases/download/v0.0.0/keygen
```

## Download the public key .pem file

You can download the binary from [here](https://github.com/airchains-network/binhub/releases/download/v0.0.0/public_key.pem)

```bash
wget https://github.com/airchains-network/binhub/releases/download/v0.0.0/public_key.pem

cp public_key.pem config/public_key.pem
```

## Usage

```bash
./keygen
```

## Configuration

If you are curious about the configuration here is the description of the each field:

- `addresses`: The GRPC addresses of the nodes you wish to connect to.
- `mnemonic_phrase`: The mnemonic phrase of the account you will use to send transactions for generating keys.
- `asc_contract`: The ASC contract address.
- `rsa_public_key_path`: The file path to the RSA public key.
- `secret_key_id`: The identifier for the secret key.

> [!NOTE]
>
> Here are two important things to understand:
>
> ### 1. RSA Public Key
>
> The RSA public key is used to encrypt the secret key.
>
> ### 2. Secret Key ID
>
> The `secret_key_id` is a unique identifier for your secret key. It corresponds to your execution environment's KMS key name. Keep this ID confidential.
>
