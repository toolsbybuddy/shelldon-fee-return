# Fee Return Methodology

## High-Level Steps

1. **Calculate total fees to distribute** — Verify exact SOL and WETH amounts claimed from Bags.fm and Base ✅ DONE
2. **Snapshot holders** — Capture holder lists at a fixed point in time for both chains ✅ DONE
3. **Filter holders** — Remove LP contracts, our own wallets, burn addresses, and other non-eligible accounts ✅ DONE
4. **Calculate proportional distribution** — Each eligible holder receives a share proportional to their token holdings ✅ DONE
5. **Burn Base tokens** — Send all 2.4B Base Shelldon tokens to burn address ✅ DONE
6. **Distribute Bags.fm (SOL) fees** — Send proportional SOL to each eligible Bags.fm holder ✅ DONE
7. **Distribute Base (WETH) fees** — Send proportional WETH to each eligible Base holder 🔄 IN PROGRESS
8. **Publish receipts** — All transaction hashes documented and repo made public ✅ DONE (partial — Base receipts pending step 7)

---

## Step 1: Calculate Total Fees to Distribute ✅ DONE

### Bags.fm (SOL)

**Fee claim transaction:**
- Tx: [`yfPP4KG4Go2kdgEjGQAinynE9mWWo5iPjXuHpio3yE9iQ9yTNs4Tw33ZB9UCy3Vv5FzcwoKrgpfvuETNH5DTJph`](https://solscan.io/tx/yfPP4KG4Go2kdgEjGQAinynE9mWWo5iPjXuHpio3yE9iQ9yTNs4Tw33ZB9UCy3Vv5FzcwoKrgpfvuETNH5DTJph)
- **Exact amount: 24.978981756 SOL** (verified on-chain — wallet went from 0.000000000 to 24.978981756)
- Date: February 21, 2026
- Claimed to wallet: `At7vrkYgPswMBUo6cZKuEe6o3wQ6gfSsvYpmrwBdV9qA`

**Post-claim transfers (moved SOL to team wallet for safekeeping before distribution plan was finalized):**
- Test: 0.005 SOL — [Tx](https://solscan.io/tx/46YLQTAdxBNSPxwKw8zY9FSatHCqvr5iLCKVmK5XS2JRnE6Xx2UPmYyrEeQBQebWWYv1PYBrCSjuPvpwWPghNQtR)
- Main: 26 SOL — [Tx](https://solscan.io/tx/3QVi8VpqJnuamdZ64JS4ABX9AaVDCeEqGosdnJ6MdzARoprmrt5nSFarduFtTGXjpxMyTcqBQ9YoQhCE5t4DjyKV)

**Exact amount to distribute: 24.978981756 SOL**

### Base (WETH)

**Fee claim transactions (via Bankr interface):**
- Tx 1: [`0x3e92dfd7949c09a57f20823274e503cac46c5e59bf13effd9ba7464202ee849a`](https://basescan.org/tx/0x3e92dfd7949c09a57f20823274e503cac46c5e59bf13effd9ba7464202ee849a)
  - **1.467524235502269958 WETH** received at block 42,474,950
- Tx 2: [`0x336179eafafed36a9342da06e31c4a65cb097f48364dda402e7fdd1b2cd756cb`](https://basescan.org/tx/0x336179eafafed36a9342da06e31c4a65cb097f48364dda402e7fdd1b2cd756cb)
  - **0.064796133347224477 WETH** received at block 42,474,971
- Claimed to wallet: `0x16045e90008cBEC3e836fB24a7881E8D4343D81e` (Bankr)
- Amounts verified on-chain via Blockscout token transfer records

**Exact amount to distribute: 1.532320368849494435 WETH**

---

## Step 2: Snapshot Holders ✅ DONE

### Bags.fm Holders
- **Snapshot date:** February 24, 2026, ~10:42 PM CST
- **Solana slot:** 402,553,927
- **Total holders:** 68 (per Bags.fm data)
- **Data source:** Bags.fm holder export (CSV)
- **Raw data:** `data/bags_holders_raw.csv`

### Base Holders
- **Snapshot date:** February 24, 2026, 10:42:41 PM CST
- **Base block:** 42,602,607
- **Total holders:** 474 (473 via Blockscout API + 1 team wallet confirmed on-chain)
- **Data source:** Blockscout API (`base.blockscout.com`)

---

## Step 3: Filter Holders ✅ DONE

### Bags.fm Exclusions ✅ DONE
| Address | Reason | Tokens | % of Supply |
|---------|--------|--------|-------------|
| `HLnpSz9h2S4hiLQ43rnSD9XkcUThA7B8hQMKmDaiTLcC` | Meteora LP Pool Authority (2 token accounts) | 855,980,358.03 | 85.63% |

**Note:** Our wallet (`At7vrkYgPswMBUo6cZKuEe6o3wQ6gfSsvYpmrwBdV9qA`) does not appear in the holder list — we held fees, not tokens.

**Eligible holders after filtering:** 65

### Base Exclusions ✅ DONE

**Classification method:** Bytecode analysis via Base JSON-RPC batch calls. All 210 contract addresses were checked using `eth_getCode` to determine their type.

**Contract breakdown (210 total):**
- **200 ERC-7702 smart wallets** — EOAs with delegated wallet implementations (bytecode: `0xef0100` + implementation address). These are real user wallets (mostly Coinbase Smart Wallet). **Included in distribution.**
- **1 ERC-1167 minimal proxy** — Proxy wallet pattern. **Included in distribution.**
- **1 TransparentUpgradeableProxy** — Has an owner/admin. **Included in distribution.**
- **2 known infrastructure** — PoolManager + DecayMulticurveInitializer. **Excluded.**
- **1 team wallet** — Our Bankr wallet. **Excluded.**
- **5 protocol contracts** — Identified by source code (see table). **Excluded.**

**Excluded addresses:**
| Address | Name | Reason | % of Supply |
|---------|------|--------|-------------|
| `0x498581fF718922c3f8e6A244956aF099B2652b2b` | Uniswap V4: PoolManager | LP pool singleton | 62.28% |
| `0xD59cE43E53D69F190E15d9822Fb4540dCcc91178` | DecayMulticurveInitializer | Clanker launch infrastructure | 2.22% |
| `0x16045e90008cBEC3e836fB24a7881E8D4343D81e` | Team Shelldon (Bankr) | Our wallet | 2.40% |
| `0x00000000009726632680FB29d3F7A9734E3010E2` | RainbowRouter | DEX aggregator | <0.01% |
| `0x0A6d96E7f4D7b96CFE42185DF61E64d255c12DFf` | FeeCollector | Protocol fee contract | <0.01% |
| `0x238a358808379702088667322f80aC48bAd5e6c4` | Vault | Protocol vault | <0.01% |
| `0xF93191d350117723DBEda5484a3b0996d285CECF` | FeeManager | Protocol fee manager | <0.01% |
| `0x4Ff1D40fb7B56665bf95D8D8e3A5320dE46709A1` | Unknown | Unverified, 0.10 tokens | <0.01% |
| `0x63242A4Ea82847b20E506b63B0e2e2eFF0CC6cB0` | Unknown | Unverified, 0.00 tokens | <0.01% |

**Eligible holders after filtering:** 465 (263 EOAs + 202 smart contract wallets)

---

## Step 4: Calculate Proportional Distribution

For each chain:
```
holder_share = (holder_tokens / total_eligible_tokens) * total_fees_to_distribute
```

Where `total_eligible_tokens` = sum of all eligible (non-excluded) holder balances.

### Bags.fm Distribution Calculation ✅ DONE

- **Total eligible tokens:** 143,669,862.13
- **Total SOL to distribute:** 24.978981756
- **Formula:** `holder_sol = (holder_tokens / 143,669,862.13) * 24.978981756`
- **Sum verification:** All 65 distributions sum to exactly 24.978981756 SOL ✅

Full per-holder breakdown: `data/bags_distribution.csv`

### Base Distribution Calculation ✅ DONE

- **Total eligible token balance:** 126,609,187,227.21 (sum of all eligible holder balances)
- **Total WETH to distribute:** 1.532320368849494435
- **Formula:** `holder_weth = (holder_tokens / 126,609,187,227.21) * 1.532320368849494435`
- **Holders with nonzero share:** 454 (11 had balances too small to produce even 1 wei of WETH)
- **Sum verification:** Checksum matches total WETH to 18 decimal places ✅

**Note on token supply:** Holder balances sum to ~193B against a 100B total supply. This is an artifact of Uniswap V4's singleton PoolManager architecture and Clanker's DecayMulticurve accounting. It does not affect proportional fairness — each holder's share is calculated relative to all other eligible holders.

Full per-holder breakdown: `data/base_distribution.csv`

---

## Step 5: Burn Base Tokens ✅ DONE

- **Tokens burned:** 2,398,759,252.74 Base Shelldon
- **Burn address:** `0x000000000000000000000000000000000000dEaD`
- **Transaction:** [`0x4e9468eaddffa85ba5e07d4382bb63bc0316b120f1d346d62e82af53d301852b`](https://basescan.org/tx/0x4e9468eaddffa85ba5e07d4382bb63bc0316b120f1d346d62e82af53d301852b)
- **Date:** February 25, 2026

---

## Step 6: Distribute Bags.fm (SOL) Fees ✅ DONE

- **Total distributed:** 24.978981756 SOL
- **Recipients:** 58 transfers (65 eligible holders; 7 had zero calculated share due to rounding at lamport precision)
- **Execution:** 4 batches, 0 failures
- **Source wallet:** `At7vrkYgPswMBUo6cZKuEe6o3wQ6gfSsvYpmrwBdV9qA`
- **Date:** February 25, 2026

Full transfer log with all transaction hashes: `data/bags_distribution_worksheet_completed.csv`

---

## Step 7: Distribute Base (WETH) Fees ✅ DONE

**Executed:** March 1, 2026 via [disperse.app](https://disperse.app) using `disperseToken` (WETH, not native ETH — required for ERC-7702 smart wallet compatibility).

**Distribution method:** WETH transferred from Brave Wallet on Base through the Disperse contract at `0xd15fE25eD0dbA12fe05e7029C88b10c25e8880E3`.

| Batch | Recipients | WETH | Transaction |
|-------|-----------|------|-------------|
| 1 | 149 | ~1.4202 | [`0x245fd9c7...`](https://basescan.org/tx/0x245fd9c753f5ae74aca80a348b73e893d9847726425b6e2b65b95451b51dfc46) |
| 2 | 150 | 0.1023 | [`0x824eb703...`](https://basescan.org/tx/0x824eb703bcbfd2cb90ce7636a795353d8aefb81bc3e81575acbd9f3bbf7b8859) |
| 3 | 135 | 0.0081 | [`0x56cf7ab5...`](https://basescan.org/tx/0x56cf7ab51687baf69afd2aa96721bfaf89401fa505bc25c2db37312360d0bb29) |

- **434 holders paid** across 3 batches, 0 failures
- **1 remainder burned** (0.001698 WETH) to `0x...dEaD`: [`0x42ff1ec4...`](https://basescan.org/tx/0x42ff1ec433dc292d617085090a5585f48233880a8f9e9ba76d37b42c41da1cc9)
- **19 dust accounts** excluded (< 0.000001 WETH, combined ~0.0000054 WETH)

Full per-holder breakdown with tx hashes: `data/base_distribution.csv`

---

## Step 8: Publish Receipts

- [x] Repo made public
- [x] Bags.fm: all transaction hashes documented (`data/bags_distribution_worksheet_completed.csv`)
- [x] Base: contract classification and distribution calculations published (`data/base_distribution.csv`)
- [x] Base: all transaction hashes documented (`data/base_distribution.csv`)
- [x] All distributions complete — March 1, 2026
