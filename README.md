# clone-lin-maker-vat-fold

Experimental uint64-scale LIN clone of Maker/Sky `Vat.fold` (signed
`ilk.rate` / `dai` / `debt` fold). **Proofs live in**
[kbelludoo/lin-open](https://github.com/kbelludoo/lin-open).

- Class: EXPERIMENTAL (RAY' = 1e9; mainnet RAY = 1e27 and `rad = wad * ray` do not fit i64)
- Upstream: [makerdao/dss](https://github.com/makerdao/dss) `src/vat.sol` at
  `fa4f6630afb0624d04a003e920b0d71a00331d98` (AGPL-3.0-or-later). Hash-pinned,
  **not vendored**.
- LIN: `src/lin_maker_vat_fold.lin` — explicit `(rate, art, rate_delta, dai, debt, live)`,
  128-bit `|Art|*|delta|`, fail-closed on `live != 1` and overflow/underflow.
- C11 oracle: `test/oracles/maker_vat_fold_c11.c` (`__int128` XOR portable limbs)

Named goldens (`Art = RAY' = 1e9`): delta=+1e6 → rate **1001000000**, rad
**1e15**; delta=-1e6 → rate **999000000**, rad **-1e15**; live=0 → **0**.

Not claimed: uint256 / vat.ilks / wad×ray rad parity, TVL, replacing Maker/Sky/EVM.
Reproduce proofs in lin-open: `make maker-vat-fold-proof`
