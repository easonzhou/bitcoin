# Mining and Consensus Mechanisms

## What is Mining?

Mining is the process of:
1. Validating new transactions
2. Adding them to the blockchain
3. Creating new bitcoins as a reward

## Proof of Work (PoW)

### How It Works

Miners compete to find a **nonce** that, when combined with block data, produces a hash meeting specific criteria (starts with certain number of zeros).

```
Block Data + Nonce → Hash Function → Valid Hash?
"Transaction data..." + 12345 → SHA-256 → 00000abc... ✓
```

### The Mining Process

1. **Collect transactions** from the mempool
2. **Create a candidate block**
3. **Compute hash** with different nonce values
4. **Check if hash meets difficulty target**
5. **If yes**: Broadcast block to network
6. **If no**: Try again with different nonce

### Difficulty Adjustment

- Target: One block every ~10 minutes
- Adjusts every 2,016 blocks (~2 weeks)
- If blocks are mined too quickly → difficulty increases
- If blocks are mined too slowly → difficulty decreases

## Mining Rewards

### Block Reward (Subsidy)
- Started at 50 BTC (2009)
- Halves every 210,000 blocks (~4 years)
- Current: 6.25 BTC (as of 2020-2024)
- Next halving: 3.125 BTC (2024)
- Final bitcoin mined: ~2140

### Transaction Fees
- Users pay fees to prioritize their transactions
- Miners collect all fees from transactions in their block
- Will become primary incentive after all bitcoins are mined

## Mining Hardware Evolution

1. **CPU Mining** (2009-2010): Regular computers
2. **GPU Mining** (2010-2013): Graphics cards
3. **FPGA Mining** (2011-2013): Specialized chips
4. **ASIC Mining** (2013-present): Purpose-built machines

## Mining Pools

Individual mining is difficult, so miners join **pools**:
- Combine computational power
- Share rewards proportionally
- More consistent payouts
- Popular pools: Foundry USA, AntPool, F2Pool

## Other Consensus Mechanisms

### Proof of Stake (PoS)
- Validators stake coins instead of computing power
- More energy efficient
- Used by Ethereum 2.0

### Delegated Proof of Stake (DPoS)
- Token holders vote for validators
- Faster transaction speeds

### Practical Byzantine Fault Tolerance (PBFT)
- Used in permissioned blockchains
- Faster consensus for known participants
