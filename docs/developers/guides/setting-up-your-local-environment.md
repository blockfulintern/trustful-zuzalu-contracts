# Setting up your local environment

## Pre-requisites

* Have these repositories forked on your environment ([frontend](https://github.com/blockful-io/trustful-zuzalu), [smart contracts](https://github.com/blockful-io/trustful-zuzalu-contracts))
* Have [YARN ](https://classic.yarnpkg.com/lang/en/docs/install/#windows-stable)installed
* RPC Node ([Alchemy ](https://www.alchemy.com/)or [Infura](https://www.infura.io/))

## Frontend Setup

Clone the repository

```bash
git clone https://github.com/YourUsername/trustful-zuzalu.git
```

### Installing dependencies

```bash
yarn i
```

After, run the development server:

```bash
yarn run dev
```

### Environment Variables

The project comes with a `.env.sample` abd `.env.local.sample files.` You must rename it to `.env` and `.env.local` respectively and fill the variables with your values. Most RPC providers offer free testnet nodes. You can use [Alchemy](https://www.alchemy.com/) or [Infura](https://infura.io/) to get a free node. This version is poting to the Scroll network and wil work only with this network. You can change the network required to access the application and deploy a new smart contract in the desired blockchain.

{% hint style="danger" %}
**WARNING**

The `NEXT_PUBLIC_WALLET_CONNECT_PROJECT_ID=` used in the `.env` file is public. They are not meant to be used in production.
{% endhint %}

If you want to use your own please create your Project ID in the [WalletConnect](https://cloud.walletconnect.com/) website (not mandatory).

```
NEXT_PUBLIC_WALLET_CONNECT_PROJECT_ID=
```

## Smart contract Setup

Start by getting `foundryup` latest version and installing the dependencies:ssss

```sh
$ curl -L https://foundry.paradigm.xyz | bash
$ yarn
```

If this is your first time with Foundry, check out the [installation](https://github.com/foundry-rs/foundry#installation) instructions.

## Clean

Delete the build artifacts and cache directories:

```sh
$ forge clean
```

## Compile

Compile the contracts:

```sh
$ forge build
```

### Test

Run the tests:

```sh
$ yarn test
```

### Deployment and Verify

First you need to export the following environment variables from `.env` in the terminal, then deploy the Resolver contract:

```sh
export API_KEY_OPTIMISTIC_ETHERSCAN="YOUR_KEY"
export RPC_OP="YOU_RPC"
export PRIVATE_KEY="YOUR_PKEY"
$ yarn deploy
```

To verify the contract, you need to add the deployed Resolver address to the environment variables and export it. Then run the verify script:

```sh
export ADDRESS_RESOLVER="DEPLOYED_ADDRESS"
$ yarn verify
```

### License

This project is licensed under MIT.
