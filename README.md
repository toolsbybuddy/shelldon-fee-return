# Shelldon Fee Return

Transparent documentation of the fee return process for non-endorsed $SHELLDON tokens on Bags.fm (Solana) and Base.

## What This Is

Team Shelldon received creator fees from $SHELLDON tokens that were launched by others on Bags.fm and Base. We committed to returning those fees to holders and burning our token holdings. This repo documents every step — methodology, calculations, and transaction receipts.

## Official $SHELLDON

Our commitment is to the community token on Pump.fun:
`CwfsRHzXg2kcfA7EaqVkAvb8RDpGfrNHtF6QcjPC73ZQ`

## Status

| Step | Bags.fm (SOL) | Base (WETH) |
|------|---------------|-------------|
| Fee amounts verified | ✅ 24.978981756 SOL | ✅ 1.532320368849 WETH |
| Holder snapshot | ✅ Slot 402,553,927 | ✅ Block 42,602,607 |
| Holder filtering | ✅ 65 eligible | ✅ 454 eligible |
| Distribution calculated | ✅ | ✅ |
| Token burn | N/A | ✅ 2.4B tokens burned |
| Fees distributed | ✅ 58 transfers, 0 failures | 🔄 Ready to execute |

## Contents

- `METHODOLOGY.md` — Step-by-step process, calculations, and all transaction links
- `data/` — Holder snapshots and distribution calculations
  - `bags_holders_raw.csv` — Raw Bags.fm holder data
  - `bags_distribution.csv` — Calculated SOL distributions
  - `bags_distribution_worksheet_completed.csv` — Completed transfers with tx hashes
  - `base_distribution.csv` — Calculated WETH distributions (454 holders)
- `transactions/` — Additional transaction receipts

## Verification

All data sources, block numbers, and transaction hashes are included so anyone can independently verify every step.

- **Base holders:** Query Blockscout API at block 42,602,607 for token `0x9cF5A43947CA5d5Aa42E5C2003051672283E5bA3`
- **Bags.fm holders:** Solana slot 402,553,927 for mint `DFEe1t1GEdfUoR8eiPgpprRNczpTnjZ2Bs9qhKmEBAGS`
- **WETH claims:** BaseScan tx links in METHODOLOGY.md
- **Token burn:** [BaseScan](https://basescan.org/tx/0x4e9468eaddffa85ba5e07d4382bb63bc0316b120f1d346d62e82af53d301852b)
