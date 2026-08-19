# Security review — scope, method, and what has actually been verified

**Reviewer:** Dane Brown — Kairo Vault Technologies GK (Huge Green Candle)
**Role:** OneXah DAO council, Audit & security — **an insider position, see §0**
**Status:** ongoing programme, not a completed audit
**Last on-chain re-confirmation:** 2026-08-19

This document exists so the proposal can describe its security posture in terms a sitting L1 member can
check, rather than in adjectives. It closes data-room items §4.3 (document the audit/security work) and
tightens the §3 framing guardrail.

---

## 0. Independence — read this before citing anything below

**This is not a third-party independent audit, and the proposal must not describe it as one.**

The reviewer sits on the OneXah DAO council in the Audit & security role. That is an *insider* position.
Work performed from inside a project — however rigorous the method, however reproducible the evidence — does
not carry the independence property that "independently audited" claims to a governance table.

Accurate phrasings:

- ✅ "Security work is performed by a council member with a published, reproducible method; every claim below
  is independently re-checkable by any third party from public chain data."
- ✅ "Hooks are verified source-to-deployment with byte-exact reproduction; the verification method is public
  and the results are falsifiable."
- ❌ "Independently audited."
- ❌ "Third-party audited."
- ❌ "Audited by Kairo Vault Technologies" *(implies an arms-length engagement that has not occurred)*.

The distinction matters commercially and it matters here: a sitting member who discovers an overstated
independence claim during due diligence will discount everything else in the submission. The honest framing
is stronger than the overstated one, because the *method* is reproducible by anyone who doubts it.

If OneXah later wants a genuinely independent review, it has to be commissioned from a party with no council
seat and no governance stake.

---

## 1. Method

The standard applied is **re-derivation, fail-closed**:

1. **Two independent node endpoints, and an honest word about what that is worth.** Every on-chain read is
   taken from at least two endpoints (`xahau.network`, `xahau.org`), which report distinct `pubkey_node`
   identities — so they are genuinely distinct servers, not one box behind two names. Disagreement between
   them is treated as fatal and stops the check; it is never silently resolved by preferring one node.
   **But endpoint diversity is not operator diversity.** Both domains are Xahau-core-associated and both sit
   behind the same CDN, so a common operator cannot be ruled out, and a fault or falsehood originating with
   that operator would appear on both. The gold standard is agreement across *separately operated*
   infrastructure; that is an open item (§4), not a claim being made here. Every result below is stated with
   the hash and size so a member can re-derive it on any node they trust, including their own.
2. **Source == deployed.** A hook is only "verified" if the repository source builds to bytecode whose
   SHA-512-half matches the `HookDefinition` `CreateCode` actually live on mainnet, by `HookHash`.
3. **Reproduced, not just compared.** Where possible the WASM is rebuilt from `.c` using the project's own
   build container and flags, and the resulting hash compared. A matching checked-in `.wasm` is weaker
   evidence than a rebuild that lands on the same hash.
4. **Behaviour read from the import table and source**, not from documentation. What a hook *can* do is
   bounded by the host functions it imports and the transaction types it emits.
5. **Claims are scoped to what was tested.** Anything not established by the above is written down as an
   open item rather than assumed safe.

---

## 2. Verified: the Raven guard hook

The Odin's Eye Raven guard is installed across the OneXah protocol accounts, so its custody properties are
load-bearing for the whole stack.

| Property | Result |
|---|---|
| Build | Raven v4.8 |
| `HookHash` | `91366A468CFBACE50A9105993D08091D0F0FDDE890D738473EEAE4850DF46D02` |
| Deployed size | 30,800 bytes |
| Source == deployed | ✅ repo `raven.wasm` SHA-512[:32] byte-identical to on-chain `CreateCode` |
| Independently rebuilt | ✅ rebuilt from `raven.c` via the project's own buildbox (`-O3`, stripped) → identical hash |
| Endpoints agreeing | 2 (`xahau.network`, `xahau.org`; see §1 on operator diversity) |
| Installed on | **9 of the 11 accounts swept** — AMM ×3, Lending ×2, Perps, LPX staking, DAO, Faucet |
| Re-confirmed live | 2026-08-19 |

**Fleet coverage improved, but is NOT complete — and the exception matters.** As of 2026-08-19 the verified
build `91366A46…` is installed on nine of the eleven accounts swept (AMM XAH/EVR, XAH/XXX, XAH/RVN; Lending
XAH, EVR; Perps; LPX staking; DAO; Faucet). An earlier check on 2026-08-12 found most of the fleet still on
an older raven that had not been through this verification, so this is a real improvement.

**The exception, now also verified.** The ELP staking account runs the older raven `D9BD75DD` (v4.6, 25,512
bytes). Rather than leave that as an open risk, it was verified on its own terms on 2026-08-19:

| Check | Result |
|---|---|
| Source == deployed | ✅ `live/raven-D9BD75DD` tag wasm byte-identical to on-chain `CreateCode`, on both endpoints |
| Host imports | 20 — the same set as v4.8 |
| Emission templates | 4 × `Invoke` (99) + 1 × `TrustSet` (20) — **identical emission surface to v4.8** |
| `Payment` emit template | **none** |

So the custody finding below **does** extend to `D9BD75DD`: that build cannot move funds either. The older
raven on the ELP account is not a live risk. Upgrading it to `91366A46…` remains desirable for fleet
uniformity, but it is a consistency item, not a security one. (The eleventh account, Oden's Eye, runs the
registry hook rather than a guard, so no raven is expected there.)

This is a point-in-time fact and must be re-run immediately before submission rather than quoted from here.

**Custody finding — the one that matters.** `raven.c` (790 lines) imports 20 host functions and emits
exactly two transaction types: `Invoke` (99) for reports to the Eye, and `TrustSet` (20) for issuer-scoped
freeze/thaw. **There is no `Payment` emission path anywhere in the hook.** A guard hook installed on an
account holding user funds therefore cannot move those funds. The Eye, operator and admin control surface
(`LBADD`/`LBDEL`/`FRZ`/`THAW`/`SETCFG`/`SETADMIN`) is a *control* surface, not a custody one.

**Honest limits on that finding**, both of which matter:

- The no-payment property is established by **reading** the source and the import table, not by a
  machine-checked proof — a whole-hook conservation prover did not converge at 30,800 bytes. It is a strong,
  reproducible argument, not a theorem.
- That source reading was performed on 2026-08-12. It carries forward to today only because the deployed
  bytecode is **byte-identical** — same `HookHash`, same 30,800 bytes, re-pulled 2026-08-19. If the hash
  changes, the finding expires with it and the analysis must be redone. A hash is the unit of trust here,
  not a date.

**Design property, stated plainly:** the guard **fails open** on a registry read miss. If the Eye is
unreachable, transactions pass rather than halt. This is a deliberate availability-over-enforcement tradeoff,
documented as such by the Odin's Eye architecture notes, and it is defensible for a guard sitting in front of
third-party payments. It does mean the guard is not an enforcement guarantee under Eye unavailability, and
the proposal should not describe it as one.

Reference: KVT verification note `KV-IV-2026-0812-001`.

---

## 3. In progress: fleet-wide source-to-deployment sweep

A sweep of the live hooks across the OneXah protocol accounts (AMM pools, lending markets, perps, DAO,
staking, faucet, Oden's Eye) has been run against two nodes using the method in §1.

**Result:** the large majority of live hooks reproduce from the audit repository. A minority did **not** —
these are provenance gaps, meaning the exact source of a live build is not preserved where the repository's
own convention says it should be. To be precise about severity:

- These are **provenance** gaps, not known vulnerabilities. Nothing here is a demonstrated exploit.
- They matter anyway, because "the source of every live build is preserved" is a property the project
  claims, and for the affected hooks it was not true at the time of the sweep.

The specific hooks and accounts were reported to the OneXah engineering lead on 2026-08-12 with supporting
hashes. They are deliberately not enumerated in this public proposal repository — that disclosure decision
belongs to the project, not to the reviewer.

### Re-run 2026-08-19 — current state

The sweep was re-run against the live fleet on 2026-08-19 rather than quoted from the earlier pass, because
the deployed set had changed in the interim.

| | |
|---|---|
| Accounts checked | 11 (AMM ×3, Lending ×2, Perps, LPX + ELP staking, DAO, Faucet, Oden's Eye) |
| Distinct live hook builds | 21 |
| **Source preserved and reproducing** | **19 of 21** (16 on main, 3 at a `live/*` tag) |
| Outstanding | 2 builds, on 2 accounts |

Sixteen builds match a source build on the repository's main line; three more are preserved at a `live/*`
provenance tag, which is the convention working as intended. **Two live builds have no matching source on
main and no `live/*` tag.** One is a DAO-stack hook and is the gap to close before submission. The other is
the Oden's Eye registry hook — arguably out of scope, since Oden's Eye is a separate project whose source
would not be expected to live in this repository; it is listed for completeness rather than as a criticism.
Neither is enumerated here; that disclosure decision belongs to the project.

Two of the items raised on 2026-08-12 have since been resolved outright — the affected hooks are either no
longer deployed or now run a build that reproduces from the repository. The earlier pass also overstated:
at least one hook counted as a gap then is in fact preserved at a tag.

**Process note, offered as a finding rather than a complaint:** the two builds preserved by tag are stored
under a tag named for a *different* hook, whose own build is no longer deployed. The source is genuinely
there, but it is not discoverable from the tag name, and a third-party verifier following the repository's
stated convention would conclude it was missing — as this reviewer initially did. Naming a `live/*` tag per
build hash would make provenance self-evident to an outside checker.

**A sitting L1 member conducting due diligence is entitled to the full sweep on request.** That is the point
of writing this section rather than omitting it.

---

## 4. Open items

- [ ] Close the single outstanding provenance gap identified in the 2026-08-19 re-run (§3) by tagging or
      committing the source for that live build.
- [ ] Adopt per-build `live/<hook>-<hash>` tag naming so provenance is self-evident to an outside verifier
      (§3 process note).
- [ ] Re-run the sweep immediately before formal submission — it is a point-in-time result, not a standing one.
- [ ] **Confirm at least one read from a separately operated node** (§1) — current endpoint diversity does
      not establish operator diversity, which is the standard this method is supposed to meet.
- [ ] Machine-checked (rather than source-read) proof of the Raven no-payment property — currently
      established for both live builds (`91366A46…`, `D9BD75DD`) by source and import-table reading.
- [ ] Upgrade the ELP staking account to `91366A46…` for fleet uniformity (consistency, not security —
      `D9BD75DD` is verified no-payment, see §2).
- [ ] Verification of the escape-hatch primitive's stated invariant — that no key is ever re-armed —
      against deployed bytecode rather than documentation.
- [ ] Independent (non-council) review, if the proposal intends to make an independence claim at all.

---

## 5. What this section supports in the proposal

The defensible security claim for the L1 submission is:

> Hooks are verified source-to-deployment against mainnet, with byte-exact rebuilds from source; the Raven
> guard — installed on all eight protocol accounts as of 2026-08-19 — has been shown to have no fund-moving
> emission path; the verification method is published, its limits are stated, and every result is
> reproducible by any third party from public chain data.

That is a stronger claim than "audited", because every part of it can be checked by a skeptic with a node
and an afternoon.

Note what is deliberately absent from that paragraph: the words *independent*, *audited*, and any count of
outstanding findings. Each was available and each would have been an overstatement.
