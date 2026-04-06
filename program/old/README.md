# Archived samples (`program/old`)

This folder is **historical reference only**. Nothing here is imported by the production bot (`main.ts`).

## Production vs this folder

| | Production (`main.ts`) | This archive |
|---|------------------------|--------------|
| Instruction builder | `program/instruction.ts` (repo root) | `program/old/instruction.ts` |
| On-chain program | `6UZznePGgoykwAutgJFmQce2QQzfYjVcsQesZbRq9Y3b` | `CJrTqPA9Y37bxE6VXRtjTkK8irRrEWuKh5gHSsqXJrVt` |
| Hop payload | Compact layout (7 bytes per hop in the current encoder) | Older layout: **75 bytes per hop** (mints + per-hop min output embedded in data) |

Do **not** swap `old/instruction.ts` into `main.ts` unless the deployed program matches that encoding.

## Files

| File | Purpose |
|------|---------|
| `instruction.ts` | Older `buildArbitrageInstructionData` / `parseArbitrageInstructionData` / `validateRoute` for the **legacy** program id above. |
| `hop.ts` | 2-hop fork test (SOL → PUMP → SOL). Uses a **local keypair path** in code; edit for your machine or replace with env. |
| `2-hop.ts` | 2-hop sample (Meteora-style pools). Loads `PRIVATE_KEY` from app `constants` (`.env`). |
| `3-hop.ts` | 3-hop sample (Orca + Meteora + Raydium-style accounts). Uses `PRIVATE_KEY` and `RPC_ENDPOINT` from app `constants`. |
| `4-hop.ts` | 4-hop sample; uses a **generated** keypair and local airdrop pattern for fork testing. |

## Running (optional)

- Prefer a **local validator** or a dedicated dev wallet. Do not point fork experiments at production keys you care about.
- From the repository root, examples:

  `npx ts-node program/old/hop.ts`

- Pool accounts, mints, and RPC assumptions may be **out of date** relative to mainnet; treat outputs as examples, not guarantees.

## Known gaps

Some scripts reference `DexProgram` names (for example `MeteoraDammV2`) that do not match the enum in `old/instruction.ts` (`dyn2`, `dlmm`, …). Those files were left as-is; fixing them is only needed if you revive a script against a matching on-chain build.

## Maintenance

If you only need the current bot behavior, you can ignore this directory. If you revive a script, align **program id**, **instruction layout**, and **account order** with the on-chain program you actually deploy.
