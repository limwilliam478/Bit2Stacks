
# 🪙 Bitcoin to Stacks Address Converter (Clarity Smart Contract)

This Clarity smart contract provides the foundation for converting **Bitcoin addresses** (Base58Check) into **Stacks addresses** (C32Check).  
It demonstrates the low-level encoding, decoding, and checksum handling required to bridge Bitcoin and Stacks address formats.

> ⚠️ **Note:** This version is a **prototype / educational reference**.  
> It includes scaffolding for full Base58 decoding and C32 encoding but currently uses simplified or fixed values.  
> The logic can be extended into a fully functional converter within Clarity’s static constraints.

---

## 📘 Overview

### What It Does
- Defines constants and helper functions for:
  - Base58 alphabet (used in Bitcoin addresses)
  - Hex and buffer manipulation
  - Counting and handling leading zero bytes
  - Stubbed out version and checksum logic
- Provides the structure for:
  - **Base58 decoding** (Bitcoin)
  - **C32 encoding** (Stacks)
  - **Version byte mapping** between BTC and STX

### What It Does *Not* Yet Do
- Full Base58 → byte decoding logic  
- Actual C32Check encoding  
- Dynamic checksum verification  
- Conversion of arbitrary Bitcoin addresses (currently uses hardcoded example data)

---

## 🧱 Smart Contract Structure

| Section | Description |
|----------|--------------|
| **Constants** | Defines Base58 alphabet, C32 alphabet, and version bytes for BTC and STX |
| **Error Codes** | Custom error identifiers for decoding and checksum failures |
| **Helper Functions** | String and buffer manipulation (`char-at`, `count-leading-ones`, `generate-zeros`, etc.) |
| **Base58 Logic** | Early draft functions for encoding/decoding Base58 strings |
| **Conversion Stubs** | Placeholder for Bitcoin → Stacks address conversion flow |

---

## ⚙️ Example Flow (Conceptual)

Here’s how the contract is structured to eventually process a Bitcoin address:

```

Bitcoin Address (Base58Check)
↓
Base58 Decode
↓
Version + Hash160 + Checksum
↓
Version Mapping
(BTC mainnet → STX mainnet)
↓
C32Check Encode
↓
Stacks Address

```

Example:
```

Input (BTC):  1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa
Output (STX): SP2J3JH3KX9Y...  (C32-encoded)

````

---

## 🧩 File: `btc-to-stx.clar`

### Key Functions

| Function | Type | Description |
|-----------|------|-------------|
| `char-at` | private | Returns a single character at a given index from a string |
| `count-leading-ones` | private | Counts Base58 leading `1`s (for zero bytes) |
| `generate-zeros` | private | Creates a zero-filled buffer |
| `hex-to-uint` | private | Converts a single hex byte to uint |
| `convert-string-to-b58-values` | private | Maps Base58 chars to integer values |
| `base58-decode-string` | private | Placeholder returning a fixed BTC P2PKH payload |
| `encode-base58-bytes` | private | Prototype for Base58 encoding |
| *(Planned)* `c32-encode` | private | Convert byte array to C32Check (Stacks) format |
| *(Planned)* `btc-to-stx` | public | Full BTC → STX conversion pipeline |

---

## 🚀 How to Deploy

1. Install [**Clarinet**](https://docs.hiro.so/clarinet/getting-started):
   ```bash
   npm install -g @hirosystems/clarinet
````

2. Create a new project:

   ```bash
   clarinet new btc-to-stx
   cd btc-to-stx
   ```

3. Add this contract to `contracts/btc-to-stx.clar`.

4. Check syntax and simulate:

   ```bash
   clarinet check
   clarinet console
   ```

5. You can then interact with the contract (e.g., test stub functions):

   ```bash
   (contract-call? .btc-to-stx base58-decode-string "1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa")
   ```

---

## 🧠 Future Improvements

| Task                             | Description                                    |
| -------------------------------- | ---------------------------------------------- |
| ✅ Implement true Base58 decoding | Convert Base58 → 25-byte payload (w/ checksum) |
| ✅ Implement checksum validation  | Double SHA256 verification                     |
| ✅ Implement version byte mapping | BTC mainnet/testnet → STX mainnet/testnet      |
| ✅ Implement C32 encoding         | Output full valid Stacks address               |
| ⚙️ Optimize for Clarity limits   | Static length management and no recursion      |

---

## 📜 License

MIT License — free to use, modify, and extend.

---
