<div align="center">

<p><img src="./docs/assets/horizontal_logo.svg" width="800"></p>

<p>
<h3><a href="https://mantle.xyz">Website</a> &nbsp&nbsp | &nbsp&nbsp&nbsp<a href="https://docs.mantle.xyz">Tech Docs</a>
</p>

<p>

</br>

[![](https://github.com/mantlenetworkio/mantle/actions/workflows/build-image.yml/badge.svg)](https://github.com/mantlenetworkio/mantle/actions/workflows/build-image.yml)

</p>

</div>

<hr>

- :book: [Introduction](#introduction)
- :dart: [Goals](#goals)
- :rocket: [Quick Start](#quick-start)
  - :link: [Useful Addresses](#useful-addresses)
  - :computer: [Set up Local Environment](#set-up-local-environment)
  - :wrench: [Using the Mantle SDK](#using-the-mantle-sdk)
  - 🧩 [Using the Node RPC API](#using-the-node-rpc-api)
  - 🎛 [Spin up a Verifier Node](#spin-up-a-verifier-node)
- :ledger: [Directory Structure](#directory-structure)
- :sparkles: [How to Contribute](#how-to-contribute)
- :copyright: [License](#license)

<hr>

## Introduction

DONOT USE THIS; THIS IS PERSONAL FORK

Mantle is a suite of Ethereum scaling solutions including an optimistic rollup and ZK rollup built using an iterative modular chain approach, and supported by Mantle’s native token $MNT.

It is designed to bolster support for hyper-scaled throughput decentralized applications (dApps) — from derivatives decentralized exchanges (DEXs), to gaming, to operations of decentralized autonomous organizations (DAOs).

<br/>

## Goals

Layer 2 rollups are built to address the scaling limitations of Ethereum by taking transaction processing to a separate execution layer, but this inevitably exposes users to the high gas fees and limited throughput on Layer 1.

Mantle's modular architecture helps achieve greater network efficiency for resources at hand, while maintaining the same level of security for all network actors. Increased network performance also enables better fraud proof and ZK proof technology, essentially unlocking the true potential of L2 rollups.

Different parts of the Mantle tech stack are specialized to tackle specific issues.

- [**Data Availability**](https://docs.mantle.xyz/introducing-mantle/a-gentle-introduction/solving-data-availability): Data Availability powered by EigenDA technology, an innovative re-staking solution that leverages Ethereum's validator network to bring the security of L1 to L2
- [**EVM-level Fraud Proofs**](https://docs.mantle.xyz/introducing-mantle/a-gentle-introduction/fraud-proofs): Improved fraud proofs that are evaluated using EVM-level instructions

> We encourage you to check out the [**Mantle tech docs**](https://docs.mantle.xyz) to learn more about the inner workings of Mantle.

</br>

## Quick Start

### Useful Addresses

|         Name          | Mainnet| Testnet                                |
| :-------------------: | --------------------------- | ------------------------------------ |
|     Token Faucet      | N/A                         | https://faucet.testnet.mantle.xyz/   |
|     Mantle Bridge     | https://bridge.mantle.xyz/  | https://bridge.testnet.mantle.xyz/   |
|    Mantle Explorer    | https://explorer.mantle.xyz/| https://explorer.testnet.mantle.xyz/ |
|  Mantle Node RPC URL  | https://rpc.mantle.xyz/     | https://rpc.testnet.mantle.xyz/      |
|       Chain ID        | 5000 | 5001                                 |

</br>

DApps need to connect to nodes for fetching block data and sending transactions to the Mantle network. Our JSON-RPC API supports **HTTPS** and **WebSocket** connections.

|  Service  | Mainnet                 | Testnet                             |
| :-------: | ----------------------- |------------------------------- |
|    RPC    | https://rpc.mantle.xyz/ | https://rpc.testnet.mantle.xyz/ |
| WebSocket | wss://ws.mantle.xyz     | wss://ws.testnet.mantle.xyz     |

</br>

### Using the Mantle SDK

You can use `npm` or `yarn` package managers to download and install the `@mantleio/sdk` package. We'll use `yarn` in this example.

1. Set up a project directory.

```sh
mkdir MantleSDK
cd MantleSDK
npm init --yes
```

2. Download and install the SDK package using this command.

```sh
yarn add -D @mantleio/sdk
```

3. Create a `<filename>.js` script and get started by making a request, for instance, to fetch the current L1 gas price.

```js
const ethers = require("ethers")
const mantle = require("@mantleio/sdk")

const l2RpcProvider = new ethers.providers.JsonRpcProvider("https://rpc.testnet.mantle.xyz")

async function main() {

    console.log(await mantle.getL1GasPrice(l2RpcProvider))
}

main();
```
4. Run your script using the `node <filename>.js` command to see the output.

> Feel free to browse through our [compilation of tutorials](https://mantlenetworkio.github.io/mantle-tutorial/) that use the Mantle SDK to demonstrate common functionality such as bridging assets between Mantle and Ethereum, and more.

The [SDK docs](https://sdk.mantle.xyz/index.html) provide complete reference of all the methods available as part of the Mantle SDK to facilitate interaction between applications and Mantle network.


</br>

### Spin up a Verifier Node

There are [multiple roles](https://docs.mantle.xyz/for-validators/network-roles#defining-network-roles) associated with Mantle nodes. Rollup Verifiers mainly sync rollup data from Mantle's trusted Sequencer ([to be decentralized in the future!](https://docs.mantle.xyz/introducing-mantle/a-gentle-introduction/decentralized-sequencer)). dApp builders who run their own verifier nodes have the benefit of being able to simulate L2 transactions, [among other advantages](https://docs.mantle.xyz/for-validators/network-roles#why-run-a-rollup-verifier-node), and have ready access to them without rate-limiting (as opposed to public RPCs).

Here's a [tutorial](https://docs.mantle.xyz/for-validators/deploying-a-rollup-verifier) describing the process of deploying a verifier node.

<br/>

## Directory Structure

<pre>
root
├── <a href="./packages">packages</a>
│   ├── <a href="./packages/common-ts">common-ts</a>: Common tools for building apps in TypeScript
│   ├── <a href="./packages/contracts">contracts</a>: L1 and L2 smart contracts for Mantle
│   ├── <a href="./packages/core-utils">core-utils</a>: Low-level utilities that make building Mantle easier
│   ├── <a href="./packages/data-transport-layer">data-transport-layer</a>: Service for indexing Mantle-related L1 data
│   ├── <a href="./packages/fault-detector">fault-detector</a>: Service for detecting Sequencer faults
│   ├── <a href="./packages/message-relayer">message-relayer</a>: Tool for automatically relaying L1<>L2 messages in development
│   ├── <a href="./packages/replica-healthcheck">replica-healthcheck</a>: Service for monitoring the health of a replica node
│   └── <a href="./packages/sdk">sdk</a>: provides a set of tools for interacting with Mantle

~~ Production ~~
├── <a href="./batch-submitter">batch-submitter</a>: Service for submitting batches of transactions and results to L1
├── <a href="./mt-batcher">mt-batcher</a>: Service for submitting batches of transactions to EigenDA
├── <a href="./mt-challenger">mt-challenger</a>: EigenDA data fraud proof
├── <a href="./bss-core">bss-core</a>: Core batch-submitter logic and utilities
├── <a href="./gas-oracle">gas-oracle</a>: Service for updating L1 gas prices on L2
├── <a href="./integration-tests">integration-tests</a>: Various integration tests for the Mantle network
├── <a href="./l2geth">l2geth</a>: Mantle client software, a fork of <a href="https://github.com/ethereum/go-ethereum/tree/v1.9.10">geth v1.9.10</a>  (deprecated for BEDROCK upgrade)
├── <a href="./l2geth-exporter">l2geth-exporter</a>: A prometheus exporter to collect/serve metrics from an L2 geth node
├── <a href="./proxyd">proxyd</a>: Configurable RPC request router and proxy
</pre>

</br>

## How to Contribute

Read through [CONTRIBUTING.md](./CONTRIBUTING.md) for a general overview of our contribution process.
Then check out our list of [good first issues](https://github.com/mantlenetworkio/mantle/contribute) to find something fun to work on!

<br/>

## License

Code forked from [`optimism`](https://github.com/ethereum-optimism/optimism) under the name [`optimism`](https://github.com/mantlenetworkio/bitnetwork/tree/master/l2geth) is licensed under the [GNU GPLv3](https://gist.github.com/kn9ts/cbe95340d29fc1aaeaa5dd5c059d2e60) in accordance with the [original license](https://github.com/ethereum-optimism/optimism/blob/master/COPYING).


All other files within this repository are licensed under the [MIT License](https://github.com/mantlenetworkio/bitnetwork/blob/master/LICENSE) unless stated otherwise.
