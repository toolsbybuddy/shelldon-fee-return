# Fee Return Methodology

## High-Level Steps

1. **Calculate total fees to distribute** — Verify exact SOL and WETH amounts claimed from Bags.fm and Base ✅ DONE
2. **Snapshot holders** — Capture holder lists at a fixed point in time for both chains ✅ DONE
3. **Filter holders** — Remove LP contracts, our own wallets, burn addresses, and other non-eligible accounts ✅ DONE (Bags.fm) / 🔄 IN PROGRESS (Base)
4. **Calculate proportional distribution** — Each eligible holder receives a share proportional to their token holdings ✅ DONE (Bags.fm) / 🔄 IN PROGRESS (Base)
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

**Fee claims:**
- ~0.065 WETH + ~1.467 WETH = ~1.53 WETH total
- Claimed via Bankr interface
- _TODO: Add Base transaction hashes for WETH claims_

**Amount to distribute:** ~1.53 WETH

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
- **Total holders:** 473 (via Blockscout API)
- **Data source:** Blockscout API (`base.blockscout.com`)

---

## Step 3: Filter Holders

### Bags.fm Exclusions ✅ DONE
| Address | Reason | Tokens | % of Supply |
|---------|--------|--------|-------------|
| `HLnpSz9h2S4hiLQ43rnSD9XkcUThA7B8hQMKmDaiTLcC` | Meteora LP Pool Authority (2 token accounts) | 855,980,358.03 | 85.63% |

**Note:** Our wallet (`At7vrkYgPswMBUo6cZKuEe6o3wQ6gfSsvYpmrwBdV9qA`) does not appear in the holder list — we held fees, not tokens.

**Eligible holders after filtering:** 65

### Base Exclusions 🔄 IN PROGRESS
| Address | Reason | % of Supply |
|---------|--------|-------------|
| `0x498581fF718922c3f8e6A244956aF099B2652b2b` | PoolManager (LP) | 62.28% |
| `0x16045e90008cBEC3e836fB24a7881E8D4343D81e` | Our wallet (Team Shelldon) | 2.40% |
| `0xD59cE43E53D69F190E15d9822Fb4540dCcc91178` | DecayMulticurveInitializer | 2.22% |
| `0x000...dead` / `0x000...0000` | Burn addresses | TBD |
| _~210 contracts under classification_ | LP/DEX vs smart wallets | — |

**Eligible holders after filtering:** _In progress — contract classification ongoing_

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

### Base Distribution Calculation 🔄 IN PROGRESS

Pending completion of holder filtering (Step 3). Distribution formula will follow the same proportional approach.

Full calculations will be in: `data/base_distribution.csv`

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

## Step 7: Distribute Base (WETH) Fees 🔄 IN PROGRESS

Base holders — if you're reading this, we haven't forgotten you. The Solana distribution is complete and the Base (WETH) distribution is actively being worked on. The same proportional methodology applies: your share will be calculated based on your token holdings at block 42,602,607.

We are currently:
- Classifying the ~210 smart contract addresses in the holder list (LP pools, DEX contracts, etc.)
- Finalizing the eligible holder set
- Calculating per-holder WETH amounts

Expected: distribution CSV and execution to follow shortly after Step 3/4 are finalized.

---

## Step 8: Publish Receipts

- [x] Repo made public
- [x] Bags.fm: all transaction hashes documented (`data/bags_distribution_worksheet_completed.csv`)
- [ ] Base: transaction hashes pending (Step 7)
- [ ] Post final wrap-up announcement once Base distribution complete
