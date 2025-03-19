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
> │   └── config.toml
> └── key-gen(binary)
> ```

## Usage

```bash
./key-gen
```

## Configuration

If you are curious about the configuration here is the description of the each field:

- `addresses`: The GRPC addresses of the nodes you wish to connect to.
- `mnemonic_phrase`: The mnemonic phrase of the account you will use to send transactions for generating keys.
- `asc_contract`: The ASC contract address.
- `rsa_public_key`: The file path to the RSA public key.
- `secret_key_id`: The identifier for the secret key.

> [!NOTE]
>
> Now here 2 things you need to know:
>
> ### 1.RSA Public Key 
> 
> `rsa_public_key` is the path to the RSA public key file.
> this file you can get it from [here](https://github.com/airchains-network/binhub/releases/download/v0.0.1/public_key.pem)
> 
>
> 2. `secret_key_id` is the id of the secret key. This is used to identify the secret key in the ASC contract.
>\
>
> 