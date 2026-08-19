# OneXah DAO - Proposal for a Seat at the Xahau L1 Governance Table

**Candidate:** OneXah DAO (One Xahau / Protocol X), represented by a validator-backed seat account
**Submitted to:** The sitting members of the Xahau L1 Governance Table
**Requested seat:** Any vacant L1 seat (S7, S9-S19) - proposed: **S9**
**Status:** Draft for member review
**Date:** July 2026

---

## Executive summary

OneXah DAO respectfully proposes that it be voted into a vacant seat on the Xahau L1 Governance Table, per the mechanism defined in the genesis governance hook (`govern.c`).

The case rests on two pillars:

1. **Long-term infrastructure contribution.** Cbot, OneXah's founder, is a long-standing Xahau supporter and validator operator, providing hardware and consensus support to the network. The proposed seat account will be derived from an actively validating master key, satisfying the UNLReport eligibility gate the reward hook enforces - we intend to *earn* the seat's rewards the way the whitepaper intends: by validating reliably.

2. **Momentum-driving, user-generated contribution.** OneXah is one of the largest sources of diverse, organic transactional traffic on Xahau today: a live, non-custodial DeFi ecosystem - AMM, lending, perpetuals, staking, cross-chain swap, GameFi hub - where **every protocol is a Xahau Hook** and every user action is a signed Xahau transaction. The protocols are governed by an on-chain DAO with a global council and a growing community of token-holder voters, so the seat would represent not one company but a **community-governed constituency**.

Twelve of the twenty L1 seats are currently vacant. No new member has been added since genesis. Seating OneXah DAO would be the first addition in the table's history - and it would seat exactly what the Governance Game was designed to attract: an ecosystem stakeholder that builds on Xahau, drives usage to Xahau, validates for Xahau, and answers to a community rather than a keyholder.

---

## 1. Who we are

**One Xahau** (onexah.io, @One_Xahau) began in February 2026 as educational tooling and DEX culture for Xahau, and grew - through 1,300+ commits in five months - into a full-stack DeFi ecosystem built entirely from native Xahau Hooks. The on-chain DAO is **Protocol X** (governance token **XXX**), and the engineering is credited to **Cbot Labs**.

Everything is live on Xahau mainnet today:

| Product | What it is |
|---|---|
| **AMM** | Constant-product pools (XAH/EVR, XAH/XXX, XAH/RVN). Remit-everywhere design: no pre-existing trustline ever required. |
| **Lending** | Two deliberately oracle-free single-asset money markets (XAH, EVR). "Cross-asset borrowing requires a price oracle, and oracles are attack surface. Each pool is one asset, top to bottom." |
| **Perpetuals** | XAH-margined 1-10× leveraged spot with on-chain TWAP oracle, funding rate, and permissionless liquidation. New markets are created **by DAO vote**, not admin action. |
| **Protocol X DAO** | On-chain fee aggregation, emission, staking, bonding, and governance - ten hooks on one account. |
| **Cross-chain swap** | XAH↔XRP, 2-signature, zero-fee - proven in both directions on mainnet (June 2026). |
| **GameFi hub & public API** | Aggregates Xahau play-to-earn projects; keyless CORS-open read API plus a fully documented raw on-chain wire format so anyone can build against our hooks without us. |

A defining design property: **every position is a bearer token.** LP shares, lending deposits, and perps LP are real Xahau IOUs in the user's wallet. "Transfer the token, transfer the redemption right." Hooks compute redemption from the inbound IOU alone - never a sender-keyed lookup - so positions are tradable on the Xahau DEX, usable as collateral, and custodiable in any multisig.

> "Xahau took a different path… small native programs called Hooks that run *inside* the ledger, attached to accounts, validated by every node. No EVM. No mempool. No off-chain executor. Just deterministic WebAssembly that finishes before the transaction commits."
> *(One Xahau, "Why Xahau")*

We built here on purpose. We are Xahau-native, Xahau-only, and Xahau-aligned.

---

## 2. What we bring to the table (literally)

### 2.1 Traffic and usage - the momentum contribution

Every swap, deposit, borrow, repayment, liquidation, perp open/close, stake, claim, vote, proposal, and bond on One Xahau is a signed Xahau mainnet transaction - plus the hook-emitted follow-ups (Remits, GenesisMints, sweeps) and autonomous Cron ticks running on six-plus protocol accounts. This is diverse, recurring, organic transaction flow: DeFi users, LPs, liquidators, gamers, and governance participants, not a single-app monoculture.

Documented footprint (see the [data room](docs/data-room.md) for sources and the live-metrics checklist):

- **TVL ~$251k** (July 2026) with a visible growth curve from ~$20k in early June - >10× in five weeks.
- **DAO treasury ~247,000 XAH**, governed by on-chain vote (treasury spends execute as passed proposals, e.g. PID 10).
- **~29,000+ XAH/year** of Balance Adjustment yield claimed autonomously by our hooks - we reverse-engineered and documented Xahau's Cron mechanics to do it, and published the research.
- 24h AMM volume on the EVR pool alone in the ~250k XAH order of magnitude at peak.
- Hundreds of XAH in SetHook fees burned to the network across our upgrade history.

*(Live, chain-verifiable transaction counts for the five product accounts will be attached as an appendix before formal submission - see data room §4.)*

### 2.2 Validator and infrastructure - the long-term contribution

Cbot operates a **proposing Xahau validator** on dedicated, isolated hardware (separate box from all application infrastructure), alongside self-hosted node, RPC, and web infrastructure across multiple domains. This is a real independent operator with a multi-year Xahau track record - not a hosted app on rented keys.

Per the reward hook (`reward.c`), an L1 seat only earns governance rewards while its account, derived from a validator master key, appears in the on-ledger UNLReport's active validator list. **We are proposing a seat that validates.** The seat account will be the account derived from our validator's master key, and we commit to maintaining UNL-grade reliability as a condition we expect the table to hold us to.

### 2.3 Novel public goods contributed to the Xahau ecosystem

These are chain-level contributions any Xahau project can adopt, born from running serious value through Hooks:

1. **The escape-hatch primitive** - solves the "Parity freeze" problem for blackholed hook accounts. A tiny pre-installed hook that, only after a supermajority vote with forced quorum and timelock, can drain stuck value to the DAO - and *never* re-arms a key. "No key is ever re-armed. Recovery = funds exit; admin never re-enters." Live on all five product accounts.
2. **Xahau Cron research** - we documented the exact requirement set for autonomous cron execution (`lsfTshCollect` + `hsfCOLLECT` + the Cron ledger object materialized by pseudo-transaction) after discovering silently non-firing configurations, and proved autonomous Balance Adjustment claims on mainnet (+4,108 XAH in one tick).
3. **Oden's Eye** - a freeze-only, DAO-governed, cross-protocol security registry with fail-open product-side guards, live across six product accounts. A shared security good for the chain.
4. **The standalone hook suite** - DAO-free AMM/lending/perps reference deployments any third party can install on their own account. Xahau public infrastructure, not just our product.
5. **A fully open wire format** - our complete raw-transaction format (every HookParameter, hex-documented) is published keyless so builders and AI agents can integrate with the hooks directly, bypassing us entirely. Deliberate anti-lock-in.

### 2.4 Security discipline

Every live hook is hash-locked with recorded lineage; every mainnet SetHook is preceded and followed by full-namespace state snapshots ("state byte-identical" is our standard of proof); testnet battle-testing is mandatory before any mainnet change; and when an exploit was found in June 2026, it was contained, forensically documented, and hardened against within days - in public changelogs. "Verify on-chain before claiming 'done' or 'broken' - never trust a stale doc" is a standing engineering rule.

Our council's Audit & security seat maintains a **published, reproducible verification method** rather than an adjective: hooks are checked source-to-deployment against mainnet, with byte-exact rebuilds from source. The Raven guard is verified this way (v4.8, `HookHash 91366A46…`, 30,800 bytes, source == deployed == independently rebuilt) and shown to have **no fund-moving emission path** - a guard on an account holding user funds cannot move those funds. As of 2026-08-19 that verified build is installed on **nine of the eleven accounts swept**; one staking account still runs an older raven build that has not been through this verification, and is listed as an open item rather than glossed. Method, evidence, honest limits and open items: **[docs/security-review.md](docs/security-review.md)**.

We state plainly that this is **insider work, not a third-party audit** - the reviewer holds a council seat. We would rather a sitting member read a reproducible method than an unearned independence claim; every result above is re-checkable by any third party from public chain data.

---

## 3. The DAO - why this seat represents a community

The seat we propose is not a founder's seat. Protocol X governance is live and has an executed on-chain history:

- **Proposals are open** to any staker meeting the minimum, with a 100 XXX bond (burned/retained - governance is deflationary by design).
- **Passage requires both** a stake-weighted community majority (`yes > no`) **and** at least one council co-signature. "Neither side can act alone… The council can't originate an outcome against the community's will; it can only assent to a direction the community already chose."
- **Real outcomes on-chain already:** treasury spends (PID 10: 2,500 XAH community fund), emission product registration (PID 7, 11), a perps market created by vote (PID 12), and a **council member elected by community vote** (PID 13).
- **Master keys on all product accounts are disabled** in favor of 2-of-3 multisigs held by separate parties, with a published roadmap to full blackhole: "Non-custody and immutability stop being claims and become properties of the ledger."

### Council

A trusted council spanning multiple continents, with role coverage across the full operational surface:

| Member | Role |
|---|---|
| **Cbot (Cody)** | Founder, hook/contract development; Xahau validator operator |
| **Gadget (Mick)** | DevOps & network development - elected to the council by on-chain community vote (PID 13) |
| **7Rays (Mike)** | Community outreach; on-chain council member |
| **Dane Brown — Kairo Vault Technologies GK** (Huge Green Candle) | Audit & security; on-chain verification |

As the community grows toward hundreds and then thousands of token-holder voters, the L1 seat's positions will be directed the same way everything else in Protocol X is: proposed openly, voted by stake, co-signed by council, executed on-chain. **A vote for this seat is a vote to put a community at the table.**

---

## 4. The ask - and the exact mechanism

Per the governance hook installed on the genesis account (`rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh`), a seat change requires identical votes from **80% of sitting members** - with 8 seats currently filled, that is **6 of 8 members**.

We ask each sitting member to cast an Invoke transaction to the genesis account with:

- HookParameter `T` = `0x53` (`'S'`) followed by the raw seat byte - for seat S9: **`5309`**
- HookParameter `V` = OneXah's 20-byte seat AccountID *(to be published with the formal submission)*

Votes persist in hook state with no expiry; the vote that crosses the threshold seats the member in the same execution. Full step-by-step mechanics, with citations to `govern.c`, are in **[docs/on-chain-vote-guide.md](docs/on-chain-vote-guide.md)**.

### What we commit to as a member

1. **Validate.** Maintain a reliable, UNL-grade validator whose derived account holds the seat, accepting the reward hook's eligibility gate as our performance bond.
2. **Participate.** Vote on seat, hook, and reward topics actively and transparently, with our positions determined by OneXah DAO governance and published on-chain.
3. **Build.** Continue shipping Xahau-native protocols, public hook infrastructure, and protocol research (Cron mechanics, escape-hatch, security registry) as open contributions.
4. **Grow the network.** Keep driving diverse transactional demand to Xahau - DeFi, GameFi, cross-chain flow - and onboard the next wave of builders through our open APIs and standalone hook suite.
5. **Answer to a community.** Every seat position traceable to an open, stake-weighted, council-co-signed DAO process.

---

## 5. Why now

The Governance Game was designed for "community, enterprise, infrastructure providers" to steward Xahau together. Twelve seats sit empty. The table has voted once - to remove. It has never voted to add.

OneXah DAO is the kind of member the empty seats were reserved for: already building here, already validating here, already governed by the people who use the chain. We are asking to formalize what is already true - that our community's future and Xahau's future are the same future - and to take up the responsibilities that come with it.

We welcome due diligence. Every claim in this document is either verifiable on-chain today or will be accompanied by chain-verifiable evidence in the formal submission package (see the [data room](docs/data-room.md)).

*"We're early, deliberately."* - and we intend to still be at this table decades from now.

---

## Repository contents

- **[docs/on-chain-vote-guide.md](docs/on-chain-vote-guide.md)** - exact voting mechanics for sitting L1 members, per `govern.c`
- **[docs/data-room.md](docs/data-room.md)** - verified facts with sources, the current L1 table state, and the open data-prep checklist before formal submission
- **[docs/security-review.md](docs/security-review.md)** - security verification method, what has actually been checked on-chain, open items, and the independence caveat
