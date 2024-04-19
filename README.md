# Ethos AVS - Operator Onboarding

This doc contains setup instructions for registering with the Ethos AVS on Holesky testnet. For now, we are only allowing whitelisted operators to register.

Please reach out to us anytime if you face any issues with this, we are happy to help!

## Register with EigenLayer

**You may skip this section if you are already registered as an operator on EigenLayer.**

If not, instructions to generate keys and register your operator with EigenLayer can be [found here](https://docs.eigenlayer.xyz/eigenlayer/operator-guides/operator-installation).

💡 Please ensure you backup your private keys to a safe location. By default, the encrypted keys will be stored in `~/.eigenlayer/operator_keys/`

## Whitelist your operator

Send us your operator's ECDSA address so it can be whitelisted on the Ethos AVS.

## Register with the Ethos AVS

**1. Clone this repo**
```bash!
git clone git@github.com:Ethos-Works/ethos-avs-operator-onboarding.git
```

**2. Fill out the operator config in `config-files/operator.holesky.yaml`**

This config file includes these fields (some of these values are already set for Holesky):
```bash!
operator_address: <OPERATOR_ADDRESS>

# Ethos AVS contract addresses
avs_registry_coordinator_address: 0x55d1E957a0071F57Ae5b38EfCb70B796aA768A7e
operator_state_retriever_address: 0xd085215c0b4375B19946Dd87b14ef67Be35F9ff5

# ETH RPC URL
eth_rpc_url: <ETH_RPC_URL>
eth_ws_url: <ETH_WS_URL>

chain_id: 17000

# Operator keys
ecdsa_private_key_store_path: <ECDSA_PRIVATE_KEY_FILE_PATH>
bls_private_key_store_path: <BLS_PRIVATE_KEY_FILE_PATH>

# This sets the logger level (true = info, false = debug)
production: true
```

For `ecdsa_private_key_store_path` and `bls_private_key_store_path`, you need to set these values to the file paths where your operator's private keys are stored. These paths should be relative to the root of the `ethos-avs-operator-onboarding` repository you cloned. By default, these are stored at `~/.eigenlayer/operator_keys/` if you used the EigenLayer CLI to generate them.

**3. Set your key decryption passwords**

You would have entered passwords while creating your private keys earlier. These passwords are needed to decrypt your operator's private keys. You should set these in environment variables:
```bash!
export OPERATOR_ECDSA_KEY_PASSWORD=<PASSWORD_HERE>
export OPERATOR_BLS_KEY_PASSWORD=<PASSWORD_HERE>
```

**4. Register with the Ethos AVS**

You can run this command to register your operator with the Ethos AVS:
```bash!
./bin/ethos-cli --config config-files/operator.holesky.yaml register-operator-with-ethos-avs
```

If you would like to de-register your operator from the Ethos AVS, you can use this command:
```bash!
./bin/ethos-cli --config config-files/operator.holesky.yaml deregister-operator-with-ethos-avs
```

If you face any issues with this process, please feel free to reach out to us.
