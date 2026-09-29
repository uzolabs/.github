# Uzo Labs

**The developer path for BOT Chain.**

*Uzo* is Igbo for road, path, or way.

BOT Chain already has the pieces: a fast EVM chain, an explorer, a faucet, a DEX, a bridge and a native paymaster. What it doesn't have is a clear path from zero to a shipped app. Uzo is that path.

We start with BOT Chain and build everything chain-agnostic, so the same tools can serve any EVM chain that needs them.

## What we're building

| Product | What it does | Status |
| --- | --- | --- |
| `uzo-sdk` | Chain configs for viem and ethers, contract addresses, typed helpers for BDEX, the bridge and the paymaster | In progress |
| `templates` | Clone-and-deploy starters: token, NFT, DEX integration, bridge integration, gasless app, AI agent | In progress |
| Uzo RPC | Mainnet and testnet RPC with `eth_getLogs` and WebSockets enabled | Planned |
| Uzo Index | Hosted indexing so apps can query events without running a node | Planned |

## BOT Chain at a glance

| | Mainnet | Testnet |
| --- | --- | --- |
| Chain ID | 677 | 968 |
| RPC | https://rpc.botchain.ai | https://rpc.bohr.life |
| Explorer | https://scan.botchain.ai | https://scan.bohr.life |
| Native token | BOT | tBOT |
| Faucet | | https://faucet.botchain.ai/basic (10 tBOT per address per day) |

Note: `eth_getLogs` is disabled on the public mainnet RPC. Uzo RPC is being built to close that gap.

## Quick start with viem

```ts
import { defineChain, createPublicClient, http } from 'viem'

export const botChain = defineChain({
  id: 677,
  name: 'BOT Chain',
  nativeCurrency: { name: 'BOT', symbol: 'BOT', decimals: 18 },
  rpcUrls: { default: { http: ['https://rpc.botchain.ai'] } },
  blockExplorers: { default: { name: 'BOTScan', url: 'https://scan.botchain.ai' } },
  contracts: {
    multicall3: { address: '0x47FA21f684bBAD707A53a0f9BE59F1422F46C265' },
  },
})

const client = createPublicClient({ chain: botChain, transport: http() })
console.log(await client.getBlockNumber())
```

Soon: `npm i @uzolabs/sdk` and import `botChain` directly.

## Roadmap

1. **Fix the path.** SDK chain configs, network reference, viem and Chainlist contributions.
2. **Build the path.** Hardhat and Foundry quickstarts, BOTScan verification guide, starter templates.
3. **Hackathon ready.** AI agent template, paymaster tutorial, indexer starter.
4. **Run the rails.** Uzo RPC and Uzo Index as hosted services.

## Get involved

- Website: [uzolabs.xyz](https://uzolabs.xyz)
- X: [@uzolabs](https://x.com/uzolabs)
- Found a gap in the BOT Chain developer experience? Open an issue. That's our backlog.
