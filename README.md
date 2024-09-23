# DeFi Kingdom Clone on Avalanche EVM Subnet

## Introduction

Welcome to the DeFi Kingdom Clone project! This project demonstrates how to set up and deploy a simplified version of a DeFi Kingdom on an Avalanche EVM Subnet. By utilizing Avalanche's high-performance blockchain and custom EVM subnets, we create a foundation for a blockchain-based game where players can interact with tokens and vaults, simulating DeFi mechanics.

## Project Overview

In this project, we:

- **Set Up an EVM Subnet on Avalanche**: Create a custom subnet to deploy our smart contracts, providing control over network parameters and native currency.
- **Deploy an ERC20 Token Contract**: Implement a basic ERC20 token that serves as the in-game currency.
- **Deploy a Vault Contract**: Create a vault contract that allows users to deposit and withdraw tokens, simulating liquidity pools in DeFi applications.

These components form the basis of a DeFi game where players can mint, transfer, and manage tokens, as well as interact with vaults to earn rewards through participation.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
  - [Deploying Contracts](#deploying-contracts)
  - [Interacting with Contracts](#interacting-with-contracts)
- [Contract Details](#contract-details)
  - [ERC20 Token Contract](#erc20-token-contract)
  - [Vault Contract](#vault-contract)
- [Testing](#testing)
- [License](#license)
- [Acknowledgments](#acknowledgments)

## Prerequisites

To run this project, you will need:

- Unix-based Operating System (macOS or Linux)
- [Node.js](https://nodejs.org/en/) and [npm](https://www.npmjs.com/)
- [Avalanche CLI](https://docs.avax.network/build/avalanchego-apis/cli)
- [Metamask](https://metamask.io/) browser extension
- [Remix IDE](https://remix.ethereum.org/)
- Basic understanding of Solidity and smart contract development

## Installation

### 1. Set Up Avalanche CLI

Install the Avalanche CLI by following the official documentation:

```bash
npm install -g avalanche-cli
```

### 2. Create an EVM Subnet

Use the Avalanche CLI to create and deploy your EVM subnet:

```bash
# Create a new subnet configuration
avalanche subnet create my-evm-subnet

# Deploy the subnet locally
avalanche subnet deploy my-evm-subnet --local
```

### 3. Add Subnet to Metamask

Add your custom subnet to Metamask:

- Open Metamask and go to **Settings > Networks > Add Network**.
- Enter the network details provided by the Avalanche CLI after deploying the subnet.
  - **Network Name**: Your Subnet Name
  - **New RPC URL**: RPC URL from Avalanche CLI output
  - **Chain ID**: Chain ID from Avalanche CLI output
  - **Currency Symbol**: Your native currency symbol
  - **Block Explorer URL**: (Optional) If you have one

### 4. Connect Remix to Metamask

- Open [Remix IDE](https://remix.ethereum.org/).
- In the **Deploy & Run Transactions** tab, select **Injected Provider - MetaMask** as the environment.
- Metamask will prompt you to connect; approve the connection.

## Usage

### Deploying Contracts

#### 1. ERC20 Token Contract

- In Remix, create a new file `ERC20.sol` and paste the ERC20 contract code provided.
- Ensure the Solidity compiler version is set to `^0.8.17`.
- Compile the contract using the **Solidity Compiler** tab.
- Deploy the contract:
  - In the **Deploy & Run Transactions** tab, make sure your account is selected.
  - Select `ERC20` from the contract dropdown.
  - Click **Deploy**.

#### 2. Vault Contract

- Create a new file `Vault.sol` and paste the Vault contract code provided.
- Compile the contract.
- Deploy the Vault contract:
  - Select `Vault` from the contract dropdown.
  - In the constructor parameters, input the address of the deployed ERC20 token contract.
  - Click **Deploy**.

### Interacting with Contracts

#### Minting Tokens

- In the deployed ERC20 contract instance in Remix, expand the **Deployed Contracts** section.
- Call the `mint` function:
  - Input the amount of tokens you wish to mint (remember to account for decimals if any).
  - Click **Transact** and confirm the transaction in Metamask.

#### Approving Tokens

- Approve the Vault contract to spend your tokens:
  - In the ERC20 contract, call the `approve` function.
  - Input the Vault contract address and the amount.
  - Click **Transact** and confirm in Metamask.

#### Depositing Tokens into Vault

- In the Vault contract, call the `deposit` function:
  - Input the amount of tokens to deposit.
  - Click **Transact** and confirm in Metamask.

#### Withdrawing Tokens from Vault

- Call the `withdraw` function on the Vault contract:
  - Input the number of shares to withdraw.
  - Click **Transact** and confirm in Metamask.

## Contract Details

### ERC20 Token Contract

A simplified implementation of the ERC20 token standard with basic functionalities:

- **Minting and Burning**: Allows users to mint new tokens and burn existing ones.
- **Transfer**: Users can transfer tokens to other addresses.
- **Approval and Allowance**: Users can approve others to spend tokens on their behalf.

#### Key Functions

- `mint(uint amount)`: Mints new tokens to the caller's address.
- `burn(uint amount)`: Burns tokens from the caller's address.
- `transfer(address recipient, uint amount)`: Transfers tokens to another address.
- `approve(address spender, uint amount)`: Approves a spender to transfer tokens.
- `transferFrom(address sender, address recipient, uint amount)`: Transfers tokens on behalf of another address.

#### Events

- `Transfer(address indexed from, address indexed to, uint value)`: Emitted when tokens are transferred.
- `Approval(address indexed owner, address indexed spender, uint value)`: Emitted when a new allowance is set.

### Vault Contract

A contract that simulates a liquidity pool where users can deposit and withdraw ERC20 tokens.

- **Deposits**: Users deposit tokens and receive shares representing their portion of the pool.
- **Withdrawals**: Users withdraw tokens by redeeming their shares.

#### Key Functions

- `deposit(uint amount)`: Deposits tokens into the vault and mints shares to the depositor.
- `withdraw(uint shares)`: Withdraws tokens based on the number of shares provided.

#### Mathematical Formulas

- **Calculating Shares on Deposit**:

  ```plaintext
  shares = (amount * totalSupply) / totalTokenBalance

  If totalSupply == 0:
      shares = amount
  ```

- **Calculating Amount on Withdrawal**:

  ```plaintext
  amount = (shares * totalTokenBalance) / totalSupply
  ```

#### Constructor

- `constructor(address _token)`: Initializes the Vault with the address of the ERC20 token.

#### Variables

- `IERC20 public immutable token`: The ERC20 token used in the vault.
- `uint public totalSupply`: Total shares issued.
- `mapping(address => uint) public balanceOf`: Mapping of user addresses to their share balance.

## Testing

- Use Remix to interact with the deployed contracts.
- Monitor transactions and balances using Metamask.
- Test different scenarios:
  - Mint tokens and check balances.
  - Approve and deposit tokens into the vault.
  - Withdraw tokens and verify balances and shares.
- Check events in Remix's console to ensure functions are emitting correct events.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- **Avalanche Documentation**: For guidance on setting up EVM subnets.
- **Solidity by Example**: Inspiration for the ERC20 and Vault contract implementations.
- **OpenZeppelin**: For standard implementations of smart contracts.
