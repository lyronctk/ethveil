# Veil ⚡

**Veil is your ultimate defender against private key theft.** 

Veil protects your assets by frontrunning unauthorized transactions and transferring all user assets to a secure, pre-specificied backup address. It can be setup within seconds, *without revealing your private key at any point in the process*.

This project was made as part of [Hack Lodge S22](https://hacklodge.org/).

## Overview
The immutability of transactions and lack of recourse in the event of a personal wallet hack has led to poor UX for crypto users. As recent events have shown, private keys can be stolen via highly-targeted hacks or [security flaws in wallet infrastructure](https://decrypt.co/106680/solana-hack-blamed-slope-mobile-wallet-exploit). Veil is intended to be the first-iteration towards mechanisms that mitigate the effects of private key theft.

<img width="867" alt="image" src="https://user-images.githubusercontent.com/97858468/185810062-228b9d12-a362-47b8-85ba-68021f7be222.png">

## Usage
Visit our [website](ethveil.xyz) to get set up. Using Veil will require you to install a client tool that will presign certain transactions under the event that your wallet's funds are under attack. The client runs entirely locally. Veil will monitor the mempool for unauthorized transactins and broadcast the pre-signed rescue transactions to transfer funds to your backup address. 

Follow the format of `.env.template` to update your `.env` file with the appropriate variables.

### CLI Command

Our CLI command will compile a Rust Binary to pre-sign approve and rescue transactions. Requires Rust 1.56.1 or higher. You can install rust [here](https://www.rust-lang.org/tools/install).
```
git clone git@github.com:lyronctk/veil.git
cd veil/cli; cargo install --path .
veil \
  --private-key $YOUR_PRIVATE_KEY \
  --backup-address $YOUR_BACKUP_ADDRESS \
  --contract-address $YOUR_CONTRACT_ADDRESS \
  --min-gas 10 \
  --max-gas 100 \
  --gas-step 10 \
  --nonce $YOUR_NONCE \
  --erc20-addresses $ERC_20_ADDRESS_TO_PROTECT \
  --chain-id 1
  --output-path "not-your-private-keys.csv"
```

### Server
Our server exposes endpoints to post approve transactions to the network along with store pre-signed rescue transactions in a database. 
```
cd veil/backend
yarn install
yarn start-server
```

### Frontend
Our frontend allows a simple self-service UX that allows you to easily generate pre-signed transactions and upload them to your DB.  
```
cd veil/frontend
yarn install
yarn build
yarn start
```

### Watchtower
Our watchtower will constantly monitor the mempool to frontrun unauthorized transactions. 
```
cd veil/backend
yarn install
yarn start-tower
```

## Disclaimer
This product is still in beta and active development and is not ready for production use. 
