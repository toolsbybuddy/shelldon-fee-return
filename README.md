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
| Fees distributed | ✅ 58 transfers, 0 failures | ✅ 434 sent, 1 burned, 19 dust |

**🎉 Fee return COMPLETE — March 1, 2026**

## Base Distribution Summary

- **Batch 1:** 149 recipients — [Tx](https://basescan.org/tx/0x245fd9c753f5ae74aca80a348b73e893d9847726425b6e2b65b95451b51dfc46)
- **Batch 2:** 150 recipients — [Tx](https://basescan.org/tx/0x824eb703bcbfd2cb90ce7636a795353d8aefb81bc3e81575acbd9f3bbf7b8859)
- **Batch 3:** 135 recipients — [Tx](https://basescan.org/tx/0x56cf7ab51687baf69afd2aa96721bfaf89401fa505bc25c2db37312360d0bb29)
- **Remainder burned:** 0.001698 WETH — [Tx](https://basescan.org/tx/0x42ff1ec433dc292d617085090a5585f48233880a8f9e9ba76d37b42c41da1cc9)

## Contents

- `METHODOLOGY.md` — Step-by-step process, calculations, and all transaction links
- `data/` — Holder snapshots and distribution calculations
  - `bags_holders_raw.csv` — Raw Bags.fm holder data
  - `bags_distribution.csv` — Calculated SOL distributions
  - `bags_distribution_worksheet_completed.csv` — Completed transfers with tx hashes
  - `base_distribution.csv` — Calculated WETH distributions with tx hashes (454 holders)
- `transactions/` — Additional transaction receipts

## Verification

All data sources, block numbers, and transaction hashes are included so anyone can independently verify every step.

- **Base holders:** Query Blockscout API at block 42,602,607 for token `0x9cF5A43947CA5d5Aa42E5C2003051672283E5bA3`
- **Bags.fm holders:** Solana slot 402,553,927 for mint `DFEe1t1GEdfUoR8eiPgpprRNczpTnjZ2Bs9qhKmEBAGS`
- **WETH claims:** BaseScan tx links in METHODOLOGY.md and base_distribution.csv
- **Token burn:** [BaseScan](https://basescan.org/tx/0x4e9468eaddffa85ba5e07d4382bb63bc0316b120f1d346d62e82af53d301852b)
