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

**Once we have whitelisted your address**, please follow the steps below to complete your registration.

**1. Clone this repo**
```bash!
git clone git@github.com:Ethos-Works/ethos-avs-operator-onboarding.git
```

**2. Fill out the operator config in `config-files/operator.holesky.yaml`**

This config file includes these fields (some of these values are already set for Holesky):
```bash!
operator_address: <OPERATOR_ADDRESS>
chain_id: 17000

# Ethos AVS contract addresses
avs_registry_coordinator_address: 0x52381Bb5A499fbAC8aDf9223049Ab82175BFba43
operator_state_retriever_address: 0xB4Ab1E260b8e764c1484E8c830CB32dBC65a5179

# ETH RPC URL
eth_rpc_url: <ETH_RPC_URL>

# Operator ECDSA key
ecdsa_private_key_store_path: <ECDSA_PRIVATE_KEY_FILE_PATH>

# This sets the logger level (true = info, false = debug)
production: true
```

You need to set `ecdsa_private_key_store_path` to the file path where your operator's private key is stored. This path should be relative to the root of the `ethos-avs-operator-onboarding` repository you cloned. By default, this is stored at `~/.eigenlayer/operator_keys/` if you used the EigenLayer CLI to generate it.

**3. Set your key decryption password**

You would have entered a password while creating your private key earlier. This password is needed to decrypt your operator's private key. You should set this as an environment variable:
```bash!
export OPERATOR_ECDSA_KEY_PASSWORD=<PASSWORD_HERE>
```

**4. Register with the Ethos AVS**

You can run this command to register your operator with the Ethos AVS:
```bash!
./bin/ethos-cli --config config-files/operator.holesky.yaml register-operator-with-ethos-avs
```

To confirm that your operator has been registered with Ethos, you can run this command:
```bash!
./bin/ethos-cli --config config-files/operator.holesky.yaml print-operator-is-active
```

If you would like to de-register your operator from the Ethos AVS, you can use this command:
```bash!
./bin/ethos-cli --config config-files/operator.holesky.yaml deregister-operator-with-ethos-avs
```

If you face any issues with this process, please feel free to reach out to us.
