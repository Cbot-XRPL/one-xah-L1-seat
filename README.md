# Cbot Labs - Proposal for a Seat at the Xahau L1 Governance Table

**Candidate:** **Cbot Labs** - Xahau validator and public infrastructure operator; builder of One Xahau / Protocol X (on-chain DAO), Xahau Vault, the public node cluster, and the open Cbot Labs hook releases
**Seat account:** derived from the Cbot Labs validator master key *(published with the formal submission)*
**Submitted to:** The sitting members of the Xahau L1 Governance Table
**Requested seat:** Any vacant L1 seat (S7, S9-S19) - proposed: **S9**
**Status:** Draft for member review
**Date:** August 2026

---

## Executive summary

Cbot Labs - the Xahau validator and infrastructure operator behind One Xahau / Protocol X, Xahau Vault and the public node cluster - respectfully proposes that it be voted into a vacant seat on the Xahau L1 Governance Table, per the mechanism defined in the genesis governance hook (`govern.c`).

The case rests on two pillars:

1. **Long-term infrastructure contribution.** Cbot (Cody), who runs Cbot Labs and founded One Xahau, is a long-standing Xahau supporter and validator operator, providing hardware and consensus support to the network. The proposed seat account will be derived from an actively validating master key, satisfying the UNLReport eligibility gate the reward hook enforces - we intend to *earn* the seat's rewards the way the whitepaper intends: by validating reliably. Beyond the validator, Cbot Labs runs a **public Xahau node cluster** - free, keyless JSON-RPC and WebSocket endpoints on mainnet, growing node by node ([cbotlabs.xyz/cluster](https://cbotlabs.xyz/cluster)) - and publishes **installable hook releases** the community runs on its own accounts ([cbot-labs-hooks](https://github.com/Cbot-XRPL/cbot-labs-hooks)).

2. **Momentum-driving, user-generated contribution.** OneXah is one of the largest sources of diverse, organic transactional traffic on Xahau today: a live, non-custodial DeFi ecosystem - AMM, lending, perpetuals, staking, cross-chain swap, GameFi hub - where **every protocol is a Xahau Hook** and every user action is a signed Xahau transaction. The protocols are governed by an on-chain DAO with a global council and a growing community of token-holder voters, so behind this seat is a **real constituency of users, LPs and builders** - not a single closed product.

Twelve of the twenty L1 seats are currently vacant. No new member has been added since genesis. Seating us would be the first addition in the table's history - and it would seat exactly what the Governance Game was designed to attract: an operator that validates for Xahau, runs public infrastructure on Xahau, publishes hooks the rest of the chain can install, and builds products whose users govern them on-chain.

---

## 1. Who we are

**One Xahau** (onexah.io, @One_Xahau) began in February 2026 as educational tooling and DEX culture for Xahau, and grew - through 1,300+ commits in five months - into a full-stack DeFi ecosystem built entirely from native Xahau Hooks. The on-chain DAO is **Protocol X** (governance token **XXX**), and the engineering is credited to **Cbot Labs**.

Everything is live on Xahau mainnet today:

| Product | What it is |
|---|---|
| **AMM** | Constant-product pools (XAH/EVR, XAH/XXX, XAH/RVN). Remit-everywhere design: no pre-existing trustline ever required. A per-pool fee switch routes the DAO's cut to the treasury in XAH. |
| **Lending** | Two deliberately oracle-free single-asset money markets (XAH, EVR). "Cross-asset borrowing requires a price oracle, and oracles are attack surface. Each pool is one asset, top to bottom." |
| **Perpetuals** | XAH-margined 1-10× leveraged spot with on-chain TWAP oracle, funding rate, and permissionless liquidation. New markets are created **by DAO vote**, not admin action. |
| **Protocol X DAO** | On-chain fee aggregation, emission, staking (with a staked-XXX yield boost), bonding, an autonomous XXX buyback-and-burn agent, and governance - ten hooks on one account. |
| **Cross-chain swap** | XAH↔XRP, is underpinned and provided by XRPLlabs and Gatehub teleport system, which we utilise and provide to users in a seamless way. |
| **GameFi hub & public API** | Aggregates Xahau play-to-earn projects; keyless CORS-open read API plus a fully documented raw on-chain wire format so anyone can build against our hooks without us. |

A defining design property: **every position is a bearer token.** LP shares, lending deposits, and perps LP are real Xahau IOUs in the user's wallet. "Transfer the token, transfer the redemption right." Hooks compute redemption from the inbound IOU alone - never a sender-keyed lookup - so positions are tradable on the Xahau DEX, usable as collateral, and custodiable in any multisig.

### The wider Cbot Labs build

**Cbot Labs** is the engineering group behind One Xahau - and One Xahau is not the only thing it runs on Xahau. Three lines of work, one team, all Xahau-native:

| Line | What it is | Where |
|---|---|---|
| **One Xahau / Protocol X** | The DeFi ecosystem above - AMM, lending, perpetuals, DAO, GameFi - every protocol a native Hook. Built by Cbot Labs, **governed on-chain by its own DAO and treasury**. | [onexah.io](https://onexah.io) |
| **Xahau Vault** | A live NFT marketplace and wallet for Xahau-native collections, running **novel hooks we wrote** rather than a custodial backend: an ephemeral buy-now broker, a two-sided bundle swap hook, a timed bundle auction hook, and a mint/remit contract hook with callback-confirmed fee routes. Self-hosted end to end - crawler, metadata resolver, media cache, bridge worker and public API on our own infrastructure. | [xahauvault.com](https://xahauvault.com) |
| **Xahau public cluster** | Free, keyless JSON-RPC and WebSocket endpoints on Xahau mainnet, plus a deep-history node. Two nodes live, a third already written into the inventory and waiting on hardware. | [cbotlabs.xyz/cluster](https://cbotlabs.xyz/cluster) |
| **Cbot Labs Hooks** | Public hook releases anyone can install on their own account: source, compiled `.wasm`, one-command installer, dry-run and hash verification. Three live on mainnet today, more in the pipeline. | [github.com/Cbot-XRPL/cbot-labs-hooks](https://github.com/Cbot-XRPL/cbot-labs-hooks) |

These are listed together on purpose. The account that would hold the seat is the **Cbot Labs validator** - and the same operator behind that key runs public RPC for the chain, hosts the NFT marketplace, and publishes working hook releases other people install on their own accounts. One Xahau's protocols, by contrast, are not ours to direct: they run on an on-chain DAO with its own treasury and its own vote.

> "Xahau took a different path… small native programs called Hooks that run *inside* the ledger, attached to accounts, validated by every node. No EVM. No mempool. No off-chain executor. Just deterministic WebAssembly that finishes before the transaction commits."
> *(One Xahau, "Why Xahau")*

We built here on purpose. We are Xahau-native, Xahau-only, and Xahau-aligned.

---

## 2. What we bring to the table (literally)

### 2.1 Traffic and usage - the momentum contribution

Every swap, deposit, borrow, repayment, liquidation, perp open/close, stake, claim, vote, proposal, and bond on One Xahau is a signed Xahau mainnet transaction - plus the hook-emitted follow-ups (Remits, GenesisMints, sweeps) and autonomous Cron ticks running on six-plus protocol accounts. This is diverse, recurring, organic transaction flow: DeFi users, LPs, liquidators, gamers, and governance participants, not a single-app monoculture.

Documented footprint (see the [data room](docs/data-room.md) for sources and the live-metrics checklist):

- **TVL grew >10x in five weeks** in mid-2026, from ~$20k in early June to ~$251k (a current figure is attached in the formal submission).
- **DAO treasury ~247,000 XAH**, governed by on-chain vote (treasury spends execute as passed proposals, e.g. PID 10).
- **81 active XXX stakers** with ~180,000 XXX staked into governance and rewards (August 2026).
- **~29,000+ XAH/year** of Balance Adjustment yield claimed autonomously by our hooks - we reverse-engineered and documented Xahau's Cron mechanics to do it, and published the research.
- 24h AMM volume on the EVR pool alone in the ~250k XAH order of magnitude at peak.
- Hundreds of XAH in SetHook fees burned to the network across our upgrade history.

*(Live, chain-verifiable transaction counts for the five product accounts will be attached as an appendix before formal submission - see data room §4.)*

### 2.2 Validator and infrastructure - the long-term contribution

Cbot operates a **proposing Xahau validator** on dedicated, isolated hardware (separate box from all application infrastructure), alongside self-hosted node, RPC, and web infrastructure across multiple domains. This is a real independent operator with a multi-year Xahau track record - not a hosted app on rented keys.

**The public cluster.** Alongside the validator - and deliberately isolated from it, on separate hardware, with the validator host guarded out of the cluster tooling *in code* rather than by convention - Cbot Labs runs a public Xahau node cluster: one deep-history node and one API node live today, a third already provisioned in inventory and waiting on RAM and NVMe. It is free and keyless for anyone to use:

| Protocol | Endpoint | Use |
|---|---|---|
| JSON-RPC | `https://cluster.cbotlabs.xyz` | Stateless queries (POST only) |
| WebSocket | `wss://ws-cluster.cbotlabs.xyz` | Subscriptions and streaming |
| Status | `https://cbotlabs.xyz/api/cluster` | Machine-readable live node state |

These are stock `xahaud` nodes that **do not validate** - trust comes from the published Xahau UNL, not from us. Admin methods (`can_delete`, `stop`, `peers`) return 403 and the admin port refuses network connections; rate limiting is applied per client at the edge (15 req/s, burst 30, 8 WS connections - verified under load at 178 req/s in, 157 rejected with 429); the deep node carries a rolling history window several times the API node's. Live per-node ledger, history window, peer count and uptime are published on the cluster page and refresh every 20 seconds. Availability is best-effort with no SLA, stated plainly on the page - this is a public good, not a product. It grows node by node as hardware lands, and the build-out plan is public.

Per the reward hook (`reward.c`), an L1 seat only earns governance rewards while its account, derived from a validator master key, appears in the on-ledger UNLReport's active validator list. **We are proposing a seat that validates.** The seat account will be the account derived from our validator's master key, and we commit to maintaining UNL-grade reliability as a condition we expect the table to hold us to.

### 2.3 Novel public goods contributed to the Xahau ecosystem

These are chain-level contributions any Xahau project can adopt, born from running serious value through Hooks:

1. **The escape-hatch primitive** - solves the "Parity freeze" problem for blackholed hook accounts. A tiny pre-installed hook that, only after a supermajority vote with forced quorum and timelock, can drain stuck value to the DAO - and *never* re-arms a key. "No key is ever re-armed. Recovery = funds exit; admin never re-enters." Live on all five product accounts.
2. **Xahau Cron research** - we documented the exact requirement set for autonomous cron execution (`lsfTshCollect` + `hsfCOLLECT` + the Cron ledger object materialized by pseudo-transaction) after discovering silently non-firing configurations, and proved autonomous Balance Adjustment claims on mainnet (+4,108 XAH in one tick).
3. **Oden's Eye** - a freeze-only, DAO-governed, cross-protocol security registry with fail-open product-side guards, live fleet-wide across the DAO and every product account (v4.9 guard, source-verified). A shared security good for the chain, now extended by RVN/RLP staking that lets holders back individual ravens.
4. **Working hook releases the community can actually install** - **[github.com/Cbot-XRPL/cbot-labs-hooks](https://github.com/Cbot-XRPL/cbot-labs-hooks)**. Not reference snippets: each release is a complete package - hook source, the compiled `.wasm`, a one-command installer with a dry-run mode, a published hook hash, and a README stating exactly what the hook can and cannot do. You sign everything with your own key; nothing is custodial and no key leaves your machine.

   | Release | What it does | Status |
   |---|---|---|
   | **ba-cron** | Installs `lsfTshCollect` + a `hsfCOLLECT` hook + a ~30-day `CronSet` so your account auto-claims its Balance Reward (~4% APY) forever, hands-off. Fires only on `Cron`/`SetHook`/`Invoke` - never on your Payments - and cannot move funds anywhere but your own balance. | Live on mainnet |
   | **uritoken-broker** | Ephemeral URIToken (NFT) broker: one XAH Payment in, the hook buys the listed token, remits it to the buyer, routes the broker fee, auto-refunds a failed buy. No escrow account, no off-chain keeper. | Live on mainnet |
   | **amm-v2** | Constant-product AMM (XAH ⇄ one IOU) with LP shares as an IOU, bps swap fee, optional DAO fee escrow and DEX offer mirroring - the exact build running the three onexah.io pools, hash-verifiable against those live accounts. It has been through an external audit (tracker private, fixes in source). | Live on mainnet |

   Plus the standalone DAO-free lending and perps reference deployments, and the Vault hooks below. **More releases are queued** - this repo is where they get published. We are the group putting working, installable Xahau hook flows in the community's hands, and we intend to keep being that.
5. **A fully open wire format** - our complete raw-transaction format (every HookParameter, hex-documented) is published keyless so builders and AI agents can integrate with the hooks directly, bypassing us entirely. Deliberate anti-lock-in.
6. **NFT hook primitives (Xahau Vault)** - marketplace mechanics implemented as hooks instead of as a custodial backend: an *ephemeral broker* that clears a buy-now in one `URITokenBuy` + `Remit` and forwards the net fee after chain costs; a *peer-to-peer swap hook* that holds each side's bundle only between the two "ready" transactions and settles both Remits **atomically in a single ledger** (mainnet-verified - the only XAH that moves is the 0.2 URIToken owner reserve riding with each token, and the hook takes no reserve of its own); a *timed auction hook* for bundles of up to four tokens with anti-snipe extension, buy-now, and a credit-and-withdraw path for refunds the ledger rejects; and a *mint/remit contract hook* that confirms the mint by callback before routing configured fee shares. Same discipline as the DeFi hooks - hash-locked, testnet battle-tested, preserved known-good baselines.
7. **Public RPC and WebSocket endpoints** - the cluster in §2.2: free, keyless, rate-limited, no SLA, and growing. Infrastructure the ecosystem can point an app at today, seat or no seat.

### 2.4 Security discipline

Every live hook is hash-locked with recorded lineage; every mainnet SetHook is preceded and followed by full-namespace state snapshots ("state byte-identical" is our standard of proof); testnet battle-testing is mandatory before any mainnet change; and when an exploit was found in June 2026, it was contained, forensically documented, and hardened against within days - in public changelogs. "Verify on-chain before claiming 'done' or 'broken' - never trust a stale doc" is a standing engineering rule.

Security is led in-house by **Cbot Labs (Cody)** - the primary audit and hook-engineering work behind the protocol. Every live hook is **verified byte-for-byte source-to-deployment** (repository source rebuilds to the exact live `HookHash`) and carries **`hookz` behavioural proofs and Xahau testnet battle-test proofs** before it ever reaches mainnet. Our guard hooks carry **no fund-moving path**: a guard installed on an account holding user funds cannot move those funds. **Kairo Vault Technologies (Dane Brown)**, our Audit & security council member, structured the verification write-up and reviewed that work on-chain - a security firm’s check; we’re straight that, as a council seat, it isn’t an independent third-party audit. Every byte-level result is re-checkable by anyone with a node. Current live builds: **[docs/live-hooks.md](docs/live-hooks.md)**; method: **[docs/security-review.md](docs/security-review.md)**.

### 2.5 The seat account, and what its rewards fund

Plainly, because members will ask.

**The seat is held by Cbot Labs.** The account is derived from our validator's master key, and Cbot Labs operates it. Cbot Labs also pays for and runs the validator, the public cluster, Xahau Vault, and the web and API infrastructure underneath all of it - the hardware, the storage, the bandwidth and the engineering hours. That is the contribution the seat would sit on.

**The rewards are infrastructure funding.** A seat's share of Balance Adjustment claims goes to the operator that runs the metal, which is how the other members use theirs. XRPL Labs does not run a DeFi protocol out of its seat; it uses what the seat earns to keep its infrastructure up and build the next thing. Ours does the same job: nodes, disks, bandwidth, the third cluster node, and the next hook release. It is not a protocol treasury line, and it is not distributed to token holders.

**One Xahau is not the same thing as the seat.** Protocol X has its own on-chain treasury, its own stake-weighted vote and its own council, and it keeps them. It does not direct the seat's rewards and is not owed them - and equally, Cbot Labs does not own or control the DAO's treasury. Two separate things, honestly labelled: an infrastructure operator with a seat, and a community-governed protocol that the same team builds for.

---

## 3. The DAO - the constituency behind the seat

The seat is operated by Cbot Labs (see §2.5), but it is not a seat with nobody behind it. The protocols the operator builds are governed by their users, and that governance is live with an executed on-chain history:

- **Proposals are open** to any staker meeting the minimum, with a 100 XXX bond (burned/retained - governance is deflationary by design).
- **Passage requires both** a stake-weighted community majority (`yes > no`) **and** at least one council co-signature. "Neither side can act alone… The council can't originate an outcome against the community's will; it can only assent to a direction the community already chose."
- **Real outcomes on-chain already:** treasury spends (PID 10: 2,500 XAH community fund), emission product registration (PID 7, 11), a perps market created by vote (PID 12), and **two council members added by community vote** (Gadget, PID 13; Dane, PID 16).
- **Master keys on all product accounts are disabled** in favor of 2-of-3 multisigs held by separate parties, with blackholing as the stated direction for accounts where it makes sense - so non-custody becomes a property of the ledger rather than a promise.

### Council

A trusted council spanning multiple continents, with role coverage across the full operational surface:

| Member | Role |
|---|---|
| **Cbot (Cody) - Cbot Labs** | Founder; hook & contract development and the protocol’s primary security/audit work - byte-for-byte, `hookz`, and testnet proofs on every live hook; Xahau validator operator |
| **gadget78 (Mick)** | DevOps; active in the Evernode Community, developer of evrPanel, bringing OneXah to decentralized hosting. (Elected to the council by on-chain community vote PID 13).
| **7Rays (Mike)** | Community outreach; on-chain council member |
| **Dane Brown - Kairo Vault Technologies GK** (Huge Green Candle) | Council member, Audit & security - structured the verification write-up and reviewed the work on-chain (a security firm; council seat, not an independent third-party audit) |

As that community grows, the seat's positions on table business will be put to it the same way protocol changes are - proposed openly, debated, voted by stake - and our reasoning published either way. The seat stays operated by the party that runs the infrastructure; the constituency is what informs how it votes. **Seating us puts a working operator at the table, with a live on-chain community behind the products it builds.**

---

## 4. The ask - and the exact mechanism

Per the governance hook installed on the genesis account (`rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh`), a seat change requires identical votes from **80% of sitting members** - with 8 seats currently filled, that is **6 of 8 members**.

We ask each sitting member to cast an Invoke transaction to the genesis account with:

- HookParameter `T` = `0x53` (`'S'`) followed by the raw seat byte - for seat S9: **`5309`**
- HookParameter `V` = our 20-byte seat AccountID *(to be published with the formal submission)*

Votes persist in hook state with no expiry; the vote that crosses the threshold seats the member in the same execution. Full step-by-step mechanics, with citations to `govern.c`, are in **[docs/on-chain-vote-guide.md](docs/on-chain-vote-guide.md)**.

### What we commit to as a member

1. **Validate.** Maintain a reliable, UNL-grade validator whose derived account holds the seat, accepting the reward hook's eligibility gate as our performance bond.
2. **Participate.** Vote on seat, hook, and reward topics actively and transparently, with our positions informed by OneXah DAO governance and our reasoning published.
3. **Build.** Continue shipping Xahau-native protocols, installable public hook releases ([cbot-labs-hooks](https://github.com/Cbot-XRPL/cbot-labs-hooks)), and protocol research (Cron mechanics, escape-hatch, security registry) as open contributions.
4. **Grow the network.** Keep driving diverse transactional demand to Xahau - DeFi, NFTs, GameFi, cross-chain flow - and onboard the next wave of builders through our open APIs, our standalone hook suite, and a public node cluster we keep expanding.
5. **Stay accountable.** Reinvest what the seat earns into the infrastructure it rests on - nodes, bandwidth, the next hook release - and publish our positions and our reasoning where the community that uses the chain can hold us to them.

---

## 5. Why now

The Governance Game was designed for "community, enterprise, infrastructure providers" to steward Xahau together. Twelve seats sit empty. The table has voted once - to remove. It has never voted to add.

Cbot Labs is the kind of member the empty seats were reserved for: already validating here, already serving public endpoints here, already shipping hooks other people install, and building products whose users govern them on-chain. We are asking to formalize what is already true - that our community's future and Xahau's future are the same future - and to take up the responsibilities that come with it.

We welcome due diligence. Every claim in this document is either verifiable on-chain today or will be accompanied by chain-verifiable evidence in the formal submission package (see the [data room](docs/data-room.md)).

*"We're early, deliberately."* - and we intend to still be at this table decades from now.

---

## Repository contents

- **[docs/on-chain-vote-guide.md](docs/on-chain-vote-guide.md)** - exact voting mechanics for sitting L1 members, per `govern.c`
- **[docs/data-room.md](docs/data-room.md)** - verified facts with sources, the current L1 table state, and the open data-prep checklist before formal submission
- **[docs/security-review.md](docs/security-review.md)** - security verification method, what has actually been checked on-chain, open items, and the independence caveat

## Elsewhere

- **[onexah.io](https://onexah.io)** - One Xahau / Protocol X: the DAO-governed DeFi ecosystem
- **[xahauvault.com](https://xahauvault.com)** - Xahau Vault: the NFT marketplace, self-hosted, hook-powered
- **[cbotlabs.xyz/cluster](https://cbotlabs.xyz/cluster)** - the public Xahau node cluster, live status and endpoints
- **[github.com/Cbot-XRPL/cbot-labs-hooks](https://github.com/Cbot-XRPL/cbot-labs-hooks)** - installable Xahau hook releases (ba-cron, URIToken broker, AMM v2 - more coming)
- **[github.com/Cbot-XRPL/Xahau-Hub](https://github.com/Cbot-XRPL/Xahau-Hub)** - the cluster provisioning repo
