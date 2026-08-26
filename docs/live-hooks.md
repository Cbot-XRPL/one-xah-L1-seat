# Live protocol hooks

Current mainnet hook builds, read from chain on **2026-08-25**. Every hook is hash-locked with recorded
lineage; anyone can confirm a `HookHash` here against the account's live `HookDefinition` with a node.

| Component | Account(s) | Live `HookHash` |
|---|---|---|
| AMM — one build on all three X/XAH pools | `rLPXFd…` / `rAMMznwk…` / `rRLPRi86…` | `C71EBD01…` |
| DAO — Core | `rxxxx9gmp…` slot 0 | `8F3133CF…` |
| DAO — Governance | `rxxxx9gmp…` slot 1 | `F3B5BB8D…` |
| DAO — Balancer | `rxxxx9gmp…` slot 2 | `ABBD16A9…` |
| DAO — Emission claim | `rxxxx9gmp…` slot 5 | `42D9EB1A…` |
| DAO — XXX buyback agent | `rxxxx9gmp…` slot 7 | `3323E2FD…` |
| DAO — Staking (LP + RVN split) | `rxxxx9gmp…` slot 8 | `17F635C3…` |
| Perps engine | `rPErP…` | `44CEC099…` |
| Lending (XAH) | `rLoAxwmn…` | `7E206143…` |
| Lending (EVR) — yield flywheel | `rLoANd…` | `9BC7773C…` |
| **Raven guard v4.9** — fleet-wide (DAO, all AMMs, both lending, perps) | 7 accounts | **`4B04925A…`** |
| BA-cron (native balance-reward poke) | fleet | `1C199BB0…` |
| Escape-hatch (vote-gated recovery) | AMMs + lending + perps | `9412F476…` |

Deployment discipline: every mainnet `SetHook` is preceded and followed by full-namespace state snapshots
("state byte-identical" is the standard of proof), testnet battle-testing is mandatory before any mainnet
change, and hook source is version-locked in the private audit repo. Re-verify against chain before quoting —
live hashes advance as hooks are upgraded.
