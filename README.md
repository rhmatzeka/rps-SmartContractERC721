# Rock-Paper-Scissors On-Chain (with a Victory NFT)

A rock-paper-scissors game that runs entirely in a smart contract on **Base Sepolia**. Two players play a round, the contract decides the winner, and the winner can mint a **Victory NFT** (ERC-721) as a trophy.

Deployed on Base Sepolia at `0x15337b2E3ba123f46f533a209516A3833D1aF438`.

## How a game works

1. Player 1 calls `createGame()` and gets a game ID.
2. Player 2 calls `joinGame(gameId)`.
3. Each player calls `submitMove(gameId, move)` with Rock, Paper, or Scissors.
4. After both moves are in, the contract picks the winner (or a draw).
5. The winner calls `redeemVictoryNFT(gameId, tokenURI)` to mint their **RPS Victory NFT (RPSNFT)**.

Anyone can read a game with `getGame(gameId)`, and events (`GameCreated`, `GameJoined`, `MoveSubmitted`, `GameFinished`, `NFTRedeemed`) let apps follow along.

> Note: moves are sent in plain form, so the second player could see the first player's move on-chain before playing. A commit-reveal scheme would fix this; it's a good next step.

## Getting started

The contract is set up twice, so you can use either tool.

**Foundry** (repo root):

```bash
forge install
forge build
forge test
```

**Hardhat** (`hardhat-base/`):

```bash
cd hardhat-base
npm install
npx hardhat test
npx hardhat run scripts/playRPS.ts   # play a sample game
```

## Project structure

| Path | What it is |
| --- | --- |
| `src/RPSGame.sol` | The game contract (Foundry) |
| `test/RPSGame.t.sol` | Foundry tests |
| `script/RPSGame.s.sol` | Foundry deploy script |
| `hardhat-base/` | The same contract with Hardhat tests, a play script, and an Ignition deploy module |
