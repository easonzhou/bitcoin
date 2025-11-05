# Bitcoin Transactions Explained

## Transaction Structure

A Bitcoin transaction contains:
- **Inputs**: References to previous transaction outputs (where coins come from)
- **Outputs**: New destinations for the coins (where they're going)
- **Amount**: How much BTC is being transferred
- **Transaction Fee**: Difference between inputs and outputs

## UTXO Model (Unspent Transaction Output)

Bitcoin doesn't track "balances" - it tracks **unspent outputs**.

### The Fundamental Concept

Unlike traditional bank accounts that show a single balance (e.g., "You have $1,000"), Bitcoin works like physical cash in your wallet. Instead of one balance, you have multiple bills/coins of different denominations.

**Example**: Your "balance" might be:
- 0.5 BTC from Alice (UTXO #1)
- 0.3 BTC from Bob (UTXO #2)
- 0.2 BTC from mining (UTXO #3)
- **Total: 1.0 BTC** (but stored as 3 separate UTXOs)

### How UTXOs Are Created and Spent

Every transaction **destroys** old UTXOs and **creates** new ones.

#### Example 1: Simple Payment

```
Starting State:
You: [1.0 BTC UTXO]
Alice: [empty]

You want to send 0.3 BTC to Alice

Transaction:
  Inputs:  [1.0 BTC] ← Your UTXO (destroyed)
  Outputs: [0.3 BTC → Alice] ← New UTXO for Alice
           [0.69 BTC → You]  ← New UTXO for you (change)
  Fee: 0.01 BTC → Miners

Ending State:
You: [0.69 BTC UTXO]
Alice: [0.3 BTC UTXO]
```

#### Example 2: Multiple Inputs (Combining UTXOs)

```
Starting State:
You have:
  - UTXO #1: 0.3 BTC
  - UTXO #2: 0.4 BTC
  - UTXO #3: 0.2 BTC
  Total: 0.9 BTC (but in 3 pieces)

You want to send 0.7 BTC to Bob

Transaction:
  Inputs:  [0.3 BTC] ← UTXO #1 (destroyed)
           [0.4 BTC] ← UTXO #2 (destroyed)
           [0.2 BTC] ← UTXO #3 (destroyed)
           Total inputs: 0.9 BTC
  Outputs: [0.7 BTC → Bob] ← New UTXO for Bob
           [0.199 BTC → You] ← Change UTXO
  Fee: 0.001 BTC (Input 0.9 - Output 0.899)

Ending State:
You now have:
  - Change: 0.199 BTC
  Total: 0.199 BTC
Bob: [0.7 BTC UTXO]
```

#### Example 3: Multiple Outputs (Batch Payment)

```
Starting State:
You: [2.0 BTC UTXO]

You want to pay multiple people at once

Transaction:
  Inputs:  [2.0 BTC] ← Your UTXO (destroyed)
  Outputs: [0.5 BTC → Alice]
           [0.3 BTC → Bob]
           [0.4 BTC → Carol]
           [0.79 BTC → You (change)]
  Fee: 0.01 BTC

Ending State:
Alice: [0.5 BTC UTXO]
Bob: [0.3 BTC UTXO]
Carol: [0.4 BTC UTXO]
You: [0.79 BTC UTXO]
```

#### Example 4: Exact Amount (No Change)

```
Starting State:
You: [1.0 BTC UTXO]

You want to send exactly 0.99 BTC to David

Transaction:
  Inputs:  [1.0 BTC]
  Outputs: [0.99 BTC → David]
  Fee: 0.01 BTC (no change output needed!)

Ending State:
David: [0.99 BTC UTXO]
You: [0 BTC] (completely spent)
```

### UTXO Chain Example

Let's trace UTXOs through multiple transactions:

```
Genesis: Coinbase mining reward
↓
[50 BTC UTXO] → Miner
↓
Transaction 1: Miner pays merchant
Inputs:  [50 BTC]
Outputs: [30 BTC → Merchant]
         [19.99 BTC → Miner (change)]
Fee: 0.01 BTC
↓
[30 BTC UTXO] → Merchant | [19.99 BTC UTXO] → Miner
↓
Transaction 2: Merchant pays employee
Inputs:  [30 BTC]
Outputs: [5 BTC → Employee]
         [24.998 BTC → Merchant (change)]
Fee: 0.002 BTC
↓
[5 BTC UTXO] → Employee | [24.998 BTC UTXO] → Merchant
```

Each UTXO can be traced back to its origin (coinbase transaction).

### Why This Model?

**Advantages:**
1. **Prevents double-spending**: Once a UTXO is spent, it's marked as used forever
2. **Parallel processing**: Different UTXOs can be verified independently
3. **Privacy**: Harder to link all addresses to one person
4. **Auditability**: Can verify total supply by counting all UTXOs

**Comparison to Account Model (like Ethereum):**

| UTXO Model (Bitcoin) | Account Model (Ethereum) |
|---------------------|-------------------------|
| Track individual outputs | Track account balances |
| Must spend entire UTXO | Deduct exact amount |
| More privacy | Simpler to understand |
| Parallel validation | Sequential nonce required |
| Like physical cash | Like bank accounts |

### Common UTXO Scenarios

**Dust UTXOs:**
```
Problem: You have many tiny UTXOs
  - 0.0001 BTC
  - 0.0002 BTC
  - 0.00015 BTC
  (20 more tiny UTXOs...)

To spend them all, you need many inputs
→ Large transaction size
→ High fees (might cost more than value!)
```

**UTXO Consolidation:**
```
When fees are low, combine small UTXOs:

Transaction:
  Inputs:  [0.0001 BTC]
           [0.0002 BTC]
           [0.00015 BTC]
           ... (23 more)
  Outputs: [0.0049 BTC → Yourself]
  Fee: 0.0001 BTC

Result: 1 UTXO instead of 23 (cheaper future transactions)
```

### Key Points
- ✅ Inputs must be fully spent (all or nothing)
- ✅ Unused amount returns as "change" to you
- ✅ Cannot partially spend a UTXO
- ✅ More UTXOs = larger transaction size = higher fees
- ✅ Your "balance" is the sum of all your UTXOs
- ✅ Each UTXO can only be spent once (prevents double-spending)

## Transaction Lifecycle

### 1. Creation
```
Alice creates transaction:
- Input: Proof she owns 1 BTC
- Output: Send 0.5 BTC to Bob
- Sign with private key
```

### 2. Broadcasting
- Transaction sent to Bitcoin network
- Enters the **mempool** (waiting area)
- Propagates to all nodes

### 3. Validation
Nodes check:
- ✓ Valid signatures
- ✓ Inputs not already spent (no double-spending)
- ✓ Input amounts ≥ Output amounts
- ✓ Correct transaction format

### 4. Mining
- Miner includes transaction in a block
- Solves Proof of Work puzzle
- Broadcasts new block

### 5. Confirmation
- 1 confirmation: Included in 1 block
- 6 confirmations: Generally considered final (~1 hour)
- More confirmations = more secure

## Transaction Fees

### How Fees Work
```
Fee = Total Inputs - Total Outputs
```

### Fee Calculation
- Measured in **satoshis per byte** (sat/vB)
- Larger transactions (more inputs/outputs) = higher fees
- Users set their own fees

### Fee Priority
- **High fee**: Fast confirmation (next block)
- **Medium fee**: Confirmation within a few blocks
- **Low fee**: May take hours or days
- **Too low**: Might be dropped from mempool

### Dynamic Fee Market
- When network is busy → fees increase
- When network is quiet → fees decrease
- Wallets often suggest appropriate fees

## Transaction Types

### Standard Transaction (P2PKH)
Pay to Public Key Hash - most common

### SegWit (P2WPKH)
- Segregated Witness
- Lower fees, more efficient
- Addresses start with 'bc1'

### Multi-Signature (MultiSig)
- Requires multiple signatures to spend
- Used for shared wallets, escrow
- Example: 2-of-3 (any 2 out of 3 people must sign)

### Time-Locked Transactions
- Can only be spent after certain time/block height
- Used for payment channels, inheritance planning

## Example Transaction Breakdown

```json
{
  "txid": "abc123...",
  "version": 2,
  "inputs": [
    {
      "previous_output": "def456:0",
      "script_sig": "signature...",
      "sequence": 4294967295
    }
  ],
  "outputs": [
    {
      "value": 50000000,
      "script_pubkey": "OP_DUP OP_HASH160 ... OP_CHECKSIG"
    },
    {
      "value": 49950000,
      "script_pubkey": "OP_DUP OP_HASH160 ... OP_CHECKSIG"
    }
  ],
  "locktime": 0
}
```

## Common Mistakes to Avoid

❌ Sending to wrong address (irreversible!)  
❌ Setting fee too low (transaction stuck)  
❌ Not checking fee before confirming  
❌ Trusting 0-confirmation transactions for large amounts  
❌ Reusing addresses (privacy concern)  
