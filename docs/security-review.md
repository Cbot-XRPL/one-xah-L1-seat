# Security & verification — what the Audit seat contributes

**Dane Brown — Kairo Vault Technologies GK** (Huge Green Candle), OneXah DAO council, Audit & security.
Point-in-time as of **2026-08-19** — re-run before formal submission rather than quoting from here.

A short summary of verification work on the live hooks. Not an audit report; detailed evidence lives in the
audit repo, where several sitting members already have access.

---

## What has been verified

**Both raven guard builds running on OneXah accounts have no fund-moving path.**

| | v4.8 | v4.6 |
|---|---|---|
| `HookHash` | `91366A46…F46D02` | `D9BD75DD…` |
| Size | 30,800 B | 25,512 B |
| Source == deployed | ✅ | ✅ (from the `live/raven-D9BD75DD` tag) |
| Emission templates | 4 × `Invoke`, 1 × `TrustSet` | identical |
| `Payment` template | **none** | **none** |

A guard installed on an account holding user funds therefore cannot move those funds. v4.8 is on 9 of the
11 accounts swept; ELP staking runs v4.6, which is why that build was verified too rather than left open.

**Provenance:** 11 accounts, 21 distinct live hook builds, **19 have preserved source** (16 on the
repository main line, 3 at a `live/*` tag). Two do not — one DAO-stack hook, and the Oden's Eye registry
hook, which belongs to a separate project and is arguably out of scope. Details on request.

## What this is not

- **Not an independent audit.** The reviewer holds a council seat, so this is insider work however
  reproducible the method. The proposal should not claim "independently audited" or "third-party audited"
  on the strength of it. What it can say: *verified source-to-deployment with byte-exact rebuilds, method
  published, results re-checkable by any third party from public chain data.*
- **Not a machine-checked proof.** The no-payment property comes from reading the source and import table
  at a byte-identical hash, not from a prover. If the hash changes, the finding expires with it.
- **Not an enforcement guarantee.** The raven guard deliberately fails open on a registry read miss, so it
  does not enforce while the Eye is unreachable. A considered availability tradeoff, not a defect.

## Method, briefly

Reads come from two node endpoints (`xahau.network`, `xahau.org`) with distinct `pubkey_node`, and
disagreement stops the check rather than being resolved by preference — though that is endpoint diversity,
not operator diversity, since both are Xahau-core-associated. A hook counts as verified only when
repository source builds to bytecode whose hash matches the live `HookDefinition`, and behaviour is read
from the import table rather than from documentation.
