# Security & verification

The protocol's security is led by **Cbot Labs (Cody)** — the primary audit and hook-engineering work: every
live build carries byte-for-byte source-to-deployment proof, `hookz` behavioural proofs, and Xahau testnet
battle-test proofs. **Kairo Vault Technologies (Dane Brown)**, a DAO council member, structured this
verification write-up and reviewed that work on-chain — a security firm's check; as a council seat, not an
independent third-party audit. Point-in-time — re-verify against chain before formal submission rather than
quoting here.

---

## Guard hooks carry no fund-moving path

**The raven guard carries no fund-moving path.** Its entire emission surface is `Invoke` + `TrustSet` —
there is **no `Payment` template** in the build — so a guard installed on an account holding user funds
cannot move those funds.

| | Raven guard — v4.9 (current fleet) |
|---|---|
| `HookHash` | `4B04925A…CFC8741` |
| Source == deployed | ✅ repository source rebuilds to the live hash (re-checked 2026-08-25) |
| Emission surface | `Invoke` + `TrustSet` |
| `Payment` template | **none** |

v4.9 is v4.8 hardened with audit fixes #152/#153 (report-gating on cooldown-persist + emit-success). The
guard runs fleet-wide — the DAO, all three AMM pools, both lending pools, and perps. Full live-build list:
**[live-hooks.md](live-hooks.md)**.

## Proofs on file

Held for every live hook (Cbot Labs engineering) and reproducible on request:

- **Byte-for-byte source-to-deployment** — repository source compiles to bytecode whose hash matches the live `HookDefinition`, exactly.
- **`hookz` behavioural proofs** — the hook's logic is exercised against its test environment.
- **Xahau testnet battle-test proofs** — mandatory before any mainnet change; freshly-funded accounts, adversarial cases.

## Scope

The byte-for-byte verification is fully reproducible — re-checkable by any member from public chain data.
Kairo Vault Technologies (Dane) has reviewed the protocol on-chain; we're straight that, as a council seat,
this is a security firm's review and **not an independent third-party audit**. The guard fails open on a
registry-read miss **by design** — an availability choice that never lets it move funds. Full method,
per-build provenance, and the review are available to sitting members on request.

## Method

A hook counts as verified only when repository source builds to bytecode whose hash matches the live
`HookDefinition`, and behaviour is read from the compiled import table rather than from documentation. Reads
are taken from two independent node endpoints (`xahau.network`, `xahau.org`) and a disagreement halts the
check rather than being resolved by preference.
