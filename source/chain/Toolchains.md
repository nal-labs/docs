# Toolchains

## Foundry

Foundry is a smart contract development toolchain.

With Foundry you can manage your dependencies, compile your project, run tests, deploy smart contracts, and interact with the chain from the command-line and via Solidity scripts.

Check out the [Foundry Book](https://book.getfoundry.sh/) to get started with using Foundry with Nal.

---

### Using Foundry with Nal

Foundry supports Nal out-of-the-box.

Just provide the Nal RPC URL and Chain ID when deploying and verifying your contracts.

#### Mainnet

##### Deploying a smart contract

```bash
forge create ... --rpc-url=https://rpc.nal.network

```

##### Verifying a smart contract

```bash
forge verify-contract ... --chain-id 328527

```

#### Testnet[](https://docs.base.org/docs/tools/foundry#testnet)

##### Deploying a smart contract

```bash
forge create ... --rpc-url=https://testnet-rpc.nal.network

```

##### Verifying a smart contract 

```bash
forge verify-contract ... --chain-id 328527624

```

------

## Hardhat

Hardhat is an Ethereum development environment for flexible, extensible, and fast smart contract development.

You can use Hardhat to edit, compile, debug, and deploy your smart contracts to Nal.

---

### Using Hardhat with Nal

To configure [Hardhat](https://hardhat.org/) to deploy smart contracts to Nal, update your project’s `hardhat.config.ts` file by adding Nal as a network:

```ts
networks: {
   // for mainnet
   "nal-mainnet": {
     url: 'https://rpc.nal.network',
     accounts: [process.env.PRIVATE_KEY as string],
     gasPrice: 1000000000,
   },
   // for Sepolia testnet
   "nal-sepolia": {
     url: "https://testnet-rpc.nal.network",
     accounts: [process.env.PRIVATE_KEY as string],
     gasPrice: 1000000000,
   }
 },
 defaultNetwork: "nal-sepolia",
```