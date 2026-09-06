# Election DApp

A blockchain voting app built with Solidity, Truffle, and Web3. Voters connect with MetaMask, pick a candidate, and cast one vote that is recorded on a local Ethereum network.

## Features

- Two candidates are created when the contract is deployed
- Each address can vote only once
- Invalid candidate IDs are rejected
- The UI shows live results and hides the ballot after you vote
- Truffle tests cover initialization, voting, and the double-vote guard

## Project layout

```
contracts/     Solidity contracts (Election.sol)
migrations/    Truffle deployment scripts
src/           Frontend (HTML, JS, Bootstrap)
test/          Contract tests
```

## Prerequisites

- [Node.js](https://nodejs.org/)
- [Truffle](https://trufflesuite.com/truffle/) (`npm install -g truffle`)
- [Ganache](https://trufflesuite.com/ganache/) for a local blockchain
- [MetaMask](https://metamask.io/) in your browser

## Setup

```bash
npm install
```

1. Start Ganache on `127.0.0.1:7545` (this matches `truffle-config.js`).
2. Import a Ganache account into MetaMask and connect MetaMask to the Ganache network.
3. Compile and deploy the contract:

```bash
truffle compile
truffle migrate --reset
```

4. Run the tests:

```bash
truffle test
```

5. Start the local frontend:

```bash
npm run dev
```

The app serves files from `src/` and the compiled contract artifacts in `build/contracts/`. Open the page in a browser with MetaMask, select a candidate, and vote.

## How voting works

The `Election` contract stores candidates and a mapping of addresses that have already voted. `vote(uint _candidateId)` checks that the sender has not voted and that the candidate exists, then increments that candidate's count and emits `votedEvent`.
