# Wallets and Cryptographic Keys

## Understanding Keys

### Private Key
- A secret 256-bit number
- **MUST keep absolutely secret**
- Used to sign transactions (prove ownership)
- Example: `E9873D79C6D87DC0FB6A5778633389F4453213303DA61F20BD67FC233AA33262`

### Public Key
- Derived from private key (one-way function)
- Can be shared with anyone
- Used to verify signatures
- Example: `04bfcab8722991ae774db48f934ca79cfb7dd991229153b9f732ba5334aafcd8e7266e47076996b55a14bf9913ee3145ce0cfc1372ada8ada74bd287450313534a`

### Bitcoin Address
- Derived from public key (hashed and encoded)
- What you share to receive payments
- Example: `1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa` (Satoshi's first address)

## Key Generation Flow

```
Random Number (Private Key)
    ↓
Elliptic Curve Multiplication (SECP256k1)
    ↓
Public Key
    ↓
SHA-256 → RIPEMD-160 → Base58Check Encoding
    ↓
Bitcoin Address
```

## Types of Wallets

### 1. Hot Wallets (Online)
**Software Wallets**
- Desktop: Electrum, Bitcoin Core
- Mobile: BlueWallet, Mycelium
- Web: Blockchain.com, Coinbase

**Pros**: Convenient, easy to use  
**Cons**: Vulnerable to hacking, malware

### 2. Cold Wallets (Offline)
**Hardware Wallets**
- Ledger Nano S/X
- Trezor Model T
- ColdCard

**Paper Wallets**
- Keys printed on paper
- Completely offline

**Pros**: Most secure for long-term storage  
**Cons**: Less convenient for frequent transactions

### 3. Custodial vs Non-Custodial

**Custodial** (Exchange wallets)
- Company controls your private keys
- Convenient but you don't truly own your coins
- "Not your keys, not your coins"

**Non-Custodial**
- You control your private keys
- Full responsibility for security
- True ownership

## Seed Phrases (BIP39)

A **mnemonic seed** is a 12-24 word phrase that can recover your wallet:

```
witch collapse practice feed shame open despair creek road again ice least
```

- Easier to write down than private keys
- Can regenerate all private keys and addresses
- **NEVER share your seed phrase with anyone**
- Store it safely offline (metal plate recommended)

## Security Best Practices

✅ **Use strong passwords**  
✅ **Enable 2FA where available**  
✅ **Backup your seed phrase** (multiple secure locations)  
✅ **Use hardware wallets** for large amounts  
✅ **Verify addresses** before sending  
✅ **Keep software updated**  
✅ **Be wary of phishing attempts**  

❌ **Never share private keys/seed phrases**  
❌ **Don't store large amounts on exchanges**  
❌ **Avoid public WiFi for transactions**  
❌ **Don't trust "too good to be true" offers**  
