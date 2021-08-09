# Chainlink's Smart Contract Developer Bootcamp

Developer bootcamp for learning how to write smart contracts in Solidity, and connect them to real-world data in a live, instructor-led group session with Chainlink Developer Advocates.

## Images

> #### Bootcamp

> ![Bootcamp](https://user-images.githubusercontent.com/75185644/128787371-504d9165-3830-47a2-8785-ab891585193b.PNG)

## Exercises covered:

- How to create a new smart contract project using the Hardhat Development Environment, then deploy it to the Kovan network and interact with the deployed smart contract.

- How to use the Hardhat Starter Kit to create, deploy and execute smart contracts that use Chainlink Data Feeds, Any-API and VRF. The following tasks were completed:

1. Deployed three smart contracts to the Kovan testnet
2. Interacted with a deployed smart contract to use Chainlink Data Feeds
3. Interacted with a deployed smart contract to perform an API request using a Chainlink Oracle
4. Interacted with a deployed smart contract to perform a request for randomness using Chainlink VRF

- How to start a local hardhat network, deploying smart contracts to a local network, deploying smart contracts to a local network that’s a fork of the mainnet, and interacting with smart contracts deployed locally. The following tasks were completed:

1. Deployed smart contracts to a local network
2. Interacted with deployed smart contracts and mock contracts on a local network
3. Created a fork of the Ethereum mainnet on a local network, deployed smart contracts to it, and interacted with the mainnet ETH/USD price feed.

- How to execute the unit and integration tests that come with the Hardhat Starter Kit, then do a Solidity Coverage test. The following tasks were completed:

1. Installed and used the Yarn package manager
2. Executed unit tests on a local hardhat network
3. Executed integration tests on a public network
4. Cheked the coverage of the unit tests.

## Technologies Used

- Solidity
- Chainlink Oracles
- Hardhat Development Environment
- Hardhat Starter Kit
- Alchemy
- Infura
- Yarn Package Manager

## Getting Started - Installation

Set your `KOVAN_RPC_URL` [environment variable.](https://www.twilio.com/blog/2017/01/how-to-set-environment-variables.html). You can get one for free at [Infura's site.](https://infura.io/) You'll also need to set the variable `PRIVATE_KEY` which is your private key from you wallet, ie MetaMask. This is needed for deploying contracts to public networks.

You can set these in your `.env` file if you're unfamiliar with how setting environment variables work. Check out our [.env example](https://github.com/smartcontractkit/hardhat-starter-kit/blob/main/.env.example). If you wish to use this method to set these variables, update the values in the .env.example file, and then rename it to '.env'

![WARNING](https://via.placeholder.com/15/f03c15/000000?text=+) **WARNING** ![WARNING](https://via.placeholder.com/15/f03c15/000000?text=+)

Don't commit and push any changes to .env files that may contain sensitive information, such as a private key! If this information reaches a public GitHub repository, someone can use it to check if you have any Mainnet funds in that wallet address, and steal them!

`.env` example:

```
KOVAN_RPC_URL='www.infura.io/asdfadsfafdadf'
PRIVATE_KEY='abcdef'
MAINNET_RPC_URL="https://eth-mainnet.alchemyapi.io/v2/your-api-key"
```

`bash` example

```
export KOVAN_RPC_URL='www.infura.io/asdfadsfafdadf'
export MNEMONIC='cat dog frog...'
export MAINNET_RPC_URL="https://eth-mainnet.alchemyapi.io/v2/your-api-key"
```

If you plan on deploying to a local [Hardhat network](https://hardhat.org/hardhat-network/) that's a fork of the Ethereum mainnet instead of a public test network like Kovan, you'll also need to set your `MAINNET_RPC_URL` [environment variable.](https://www.twilio.com/blog/2017/01/how-to-set-environment-variables.html) and uncomment the `forking` section in `hardhat.config.js`. You can get one for free at [Alchemy's site.](https://alchemyapi.io/).

You can also use a `PRIVATE_KEY` instead of a `MNEMONIC` environment variable by uncommenting the section in the `hardhat.config.js`, and commenting out the `MNEMONIC` line.

Then you can install all the dependencies

```bash
git clone https://github.com/smartcontractkit/hardhat-starter-kit/
cd hardhat-starter-kit
```

then

```bash
npm install
```

Or

```bash
yarn
```

## Auto-Funding

This Starter Kit is configured by default to attempt to auto-fund any newly deployed contract that uses Any-API or Chainlink VRF, to save having to manually fund them after each deployment. The amount in LINK to send as part of this process can be modified in the [Starter Kit Config](https://github.com/smartcontractkit/chainlink-hardhat-box/blob/main/helper-hardhat-config.js), and are configurable per network.

| Parameter  | Description                                       | Default Value |
| ---------- | :------------------------------------------------ | :------------ |
| fundAmount | Amount of LINK to transfer when funding contracts | 1 LINK        |

If you wish to deploy the smart contracts without performing the auto-funding, run the following command when doing your deployment:

```bash
npx hardhat deploy --tags main
```

## Deploy

Deployment scripts are in the [deploy](https://github.com/smartcontractkit/hardhat-starter-kit/tree/main/deploy) directory. If required, edit the desired environment specific variables or constructor parameters in each script, then run the hardhat deployment plugin as follows. If no network is specified, it will default to the Kovan network.

This will deploy to a local hardhat network

This will deploy to a local hardhat network

```bash
npx hardhat deploy
```

To deploy to testnet:

```bash
npx hardhat deploy --network kovan
```

## Test

Tests are located in the [test](https://github.com/smartcontractkit/hardhat-starter-kit/tree/main/test) directory, and are split between unit tests and integration tests. Unit tests should only be run on local environments, and integration tests should only run on live environments.

To run unit tests:

```bash
yarn test
```

To run integration tests:

```bash
yarn test-integration
```

## Run

The deployment output will give you the contract addresses as they are deployed. You can then use these contract addresses in conjunction with Hardhat tasks to perform operations on each contract

### Chainlink Price Feeds

The Price Feeds consumer contract has one task, to read the latest price of a specified price feed contract

```bash
npx hardhat read-price-feed --contract insert-contract-address-here --network network
```

### Request & Receive Data

The APIConsumer contract has two tasks, one to request external data based on a set of parameters, and one to check to see what the result of the data request is. This contract needs to be funded with link first:

```bash
npx hardhat fund-link --contract insert-contract-address-here --network network
```

Once it's funded, you can request external data by passing in a number of parameters to the request-data task. The contract parameter is mandatory, the rest are optional

```bash
npx hardhat request-data --contract insert-contract-address-here --network network
```

Once you have successfully made a request for external data, you can see the result via the read-data task

```bash
npx hardhat read-data --contract insert-contract-address-here --network network
```

### VRF Get a random number

The VRFConsumer contract has two tasks, one to request a random number, and one to read the result of the random number request. This contract needs to be funded with link first:

```bash
npx hardhat fund-link --contract insert-contract-address-here --network network
```

Once it's funded, you can perform a VRF request with the request-random-number task:

```bash
npx hardhat request-random-number --contract insert-contract-address-here --network network
```

Once you have successfully made a request for a random number, you can see the result via the read-random-number task:

```bash
npx hardhat read-random-number --contract insert-contract-address-here --network network
```

## Verify on Etherscan

You'll need an `ETHERSCAN_API_KEY` environment variable. You can get one from the [Etherscan API site.](https://etherscan.io/apis)

```
npx hardhat verify --network <NETWORK> <CONTRACT_ADDRESS> <CONSTRUCTOR_PARAMETERS>
```

example:

```
npx hardhat verify --network kovan 0x9279791897f112a41FfDa267ff7DbBC46b96c296 "0x9326BFA02ADD2366b30bacB125260Af641031331"
```

### Linting

```
yarn lint:fix
```

---
