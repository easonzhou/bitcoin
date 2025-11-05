# Blockchain Basics

## What is Blockchain?

A blockchain is a **distributed, immutable ledger** that records transactions across a network of computers. Think of it as a digital chain of blocks, where each block contains data and is linked to the previous one.

## Key Characteristics

1. **Decentralized**: No single authority controls the network
2. **Immutable**: Once data is recorded, it's extremely difficult to change
3. **Transparent**: All participants can view the transaction history
4. **Secure**: Uses cryptographic techniques to ensure data integrity

## How Does a Block Work?

Each block contains:
- **Data**: Transaction information
- **Hash**: A unique identifier (like a fingerprint)
- **Previous Hash**: Links to the previous block
- **Timestamp**: When the block was created
- **Nonce**: A number used in mining

## The Chain Structure

```
Block 1 (Genesis)     Block 2              Block 3
[Data]                [Data]               [Data]
[Hash: abc123]   →    [Hash: def456]  →    [Hash: ghi789]
[Prev: 000000]        [Prev: abc123]       [Prev: def456]
```

## Why Is It Secure?

- Changing one block would change its hash
- This breaks the chain for all subsequent blocks
- The network would reject the altered chain
- Would require controlling 51%+ of the network (extremely difficult)

## Common Use Cases

- Cryptocurrency (Bitcoin, Ethereum)
- Supply chain tracking
- Digital identity verification
- Smart contracts
- Healthcare records
- Voting systems
