# Data Room — Verified Facts, Sources, and Pre-Submission Checklist

This file is the data-prep backbone for the proposal. §1–§3 are verified facts with sources. §4 is the open checklist of numbers and artifacts to gather **before** the formal submission goes to sitting members.

---

## 1. Xahau governance — verified spec facts

Verified against the governance hook source and live ledger state (via `account_namespace` on the genesis account, July 2026).

| Fact | Value | Source |
|---|---|---|
| Governance account | `rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh` (genesis) | govern.c |
| L1 seats | 20 (`SEAT_COUNT 20`) | govern.c |
| Filled seats / `MC` | 8 | live hook state |
| Vacant seats | S7, S9–S19 (12 seats) | live hook state |
| Seat-change threshold | 80% of filled seats, floor, min 2 → currently **6 of 8** | govern.c lines ~372–393 |
| Hook / reward-param threshold | 100% of filled seats | govern.c |
| L2 → L1 raise threshold | 51% of L2 members | govern.c |
| Vote transport | `ttINVOKE` (99) with HookParameters `T`/`V` (+`L` on L2) | govern.c header spec |
| Seat topic encoding | `'S'` (0x53) + raw seat byte (S9 = `5309`) | govern.c |
| Vote persistence | indefinite, no expiry; threshold-crossing vote executes in-line | govern.c |
| Reward rate `RR` | 0.00333333… /month ≈ 4% p.a. (unchanged since genesis) | live state; XahauGenesis.h |
| Reward delay `RD` | 2,600,000 s ≈ 30.09 days | live state; XahauGenesis.h |
| L1 member reward | 1/20th of each user's claimed Balance Adjustment per claim | reward.c; whitepaper |
| Member reward gate | seat account must be validator-master-key-derived AND in UNLReport active list | reward.c lines ~265–267 |
| Precedent | S7 removed by 7-of-9 vote (only seat change ever); no member ever added | live hook state |

**Primary sources:**
- https://github.com/Xahau/xahaud/blob/dev/hook/genesis/govern.c
- https://github.com/Xahau/xahaud/blob/dev/hook/genesis/reward.c
- https://github.com/Xahau/xahaud/blob/dev/src/xrpld/app/tx/detail/XahauGenesis.h
- https://xahau.network/docs/features/governance-game
- https://xahau.network/Xahau-Whitepaper.pdf
- Secondary: https://xaman.app/blog/decoding-xahau-the-governance-game , https://gatehub.net/blog/the-genesis-of-xahau-an-overview-of-key-governance-and-mechanisms/
- Explorers: https://xahau.xrplwin.com/validators/governance , https://xahauexplorer.com/en/governance

**Caveat:** some secondary summaries garble the thresholds. Cite `govern.c` (seats 80%, hooks/rewards 100%, L2 raise 51%) — the source is unambiguous.

## 2. OneXah — verified facts (from the `100-2` repo)

Key sources inside `c:\Users\codyr\Desktop\Code\100-2`: `README.md`, `llms.txt`, `ai/BRAIN.md`, `ai/changelog.md`, `ai/library/hook-registry.md` (authoritative hook↔hash↔deployment lock), `ai/library/protocol-x-plan.md`, `frontend/src/BlogPage.jsx`, `frontend/src/DocsPage.jsx`.

### Protocol scale
- 42,329 lines of hand-written C across 43 hook source files; 34 active. 226 operational scripts. 1,334 commits Feb 16 → Jul 10, 2026.
- 10 hooks live on the DAO account `rxxxx9gmp1DSJ8bE4Gya48VtRdPPz7mHF` (10/10 slots full).
- Product accounts: AMM XAH/EVR `rAMMznwkgL1BB6o4eYWufMAdy6t1LPgnf`, AMM XAH/XXX `rLPXFdgvriFHXt7WYybqJSu49Ff5DRzq1u`, Lending XAH `rLoAxwmnrSnTtH58TJYi12coKUWePcENLU`, Lending EVR `rLoANdfWMtXnv2xYKsTDDkrEDyH71bMUfw`, Perps `rPErPbJuVJMTBGH2V4p6dbKnfmasU52KTY`, LPX staking `rxstbCa8R8DNGf5znxYkWwPYzjXUeGiRo`, Oden's Eye `rodENWCDYuas4sXkbBs3QeYsGLXzqrSps`, XAH/RVN `rRLPRi86xXjq8QmuvcpUfN6dg3etmCNHT`.
- All product master keys disabled → 2-of-3 multisigs; roadmap to full blackhole (escape-hatch is the prerequisite, live on all 5 products since 2026-06-11).

### Value / traffic datapoints (as recorded in-repo)
- TVL 2026-07-08: $213k base + $38k staked XXX = **$251k**; up from ~$20k (2026-06-06) and $131k→$145k (2026-06-12).
- DAO treasury ~244,480 → 246,980 XAH after PID 10 (2,500 XAH community tipping fund).
- XAH/XXX pool ~1.3M XAH referenced in BA-cron analysis; AMM auto-claimed +4,108 XAH in one cron tick (2026-06-20).
- ~29k XAH/yr Balance Adjustment yield across DAO + perps + lend-XAH.
- 24h EVR-pool volume cited at ~250K XAH order of magnitude (`dev-checklist.json:4648`).
- XAH↔XRP cross-chain swap proven both directions on mainnet 2026-06-13.

### DAO governance (executed on-chain history)
- Passage rule: stake-weighted `yes > no` AND ≥1 council YES; 100 XXX proposal bond; vote XXX + bonds burned/retained (deflationary).
- Executed proposals: PID 6 (ADDPROD), PID 7 (emission product), PID 10 (**treasury spend**, 2,500 XAH), PID 11 (ELP staked emission), PID 12 (**perps pair added by vote**), PID 13 (**council member "gadet" elected**, `rsmYqAFi4hQtTY6k6S3KPJZh7axhUwxT31`, 18,057 XXX staked).
- Council on-chain: `rHmmXMfW4bdxJqQeuUPdQSG8zL8RXabrBe` (dust/admin), `rGYNRDczgiJf5ScSwu4pihozRoMJAb4JV5` (7Rays), `rsmYqAFi4hQtTY6k6S3KPJZh7axhUwxT31` (Gadget). `CCNT` = 3 at tag `0x1E`.
- Tokenomics: 3,000 XXX/epoch initial, 0.06%/epoch decay (~20%/yr), ~5M XXX free-emission ceiling, bond price = live AMM − 5% fee, 7-epoch vesting.

### Validator
- `ai/BRAIN.md:17`: dedicated `XahauNode` box, **separate from application infra**, synced and **proposing**; isolation is an explicit standing rule. Hostname `xahauval.cbotlabs.xyz` routed in `infra/cloudflare-tunnel/hosts.txt`.

### Novel public-good contributions
1. Escape-hatch recovery primitive (`ai/library/escape-hatch.md`) — 22/22 testnet E2E, live on 5 accounts.
2. Xahau Cron mechanics research (`ai/library/ba-cron.md`) — `lsfTshCollect` + `hsfCOLLECT` + Cron pseudo-tx requirement set, documented from scratch.
3. Oden's Eye security registry + raven guards (freeze-only, fail-open, DAO-governed), live on 6 products.
4. Standalone DAO-free AMM/lending/perps suite with live mainnet reference deployments.
5. Fully published raw wire format (`llms.txt`) — keyless, anti-lock-in, AI-agent-friendly.

## 3. Framing guardrails (keep the proposal honest)

- **Do not claim "majority of Xahau traffic"** until §4.2 produces chain-verified numbers. Current defensible phrasing: "one of the largest sources of diverse, organic transactional traffic."
- **Voter counts:** repo documents council of 3 (+admin) and active stakers, not "100s–1000s of voters." Frame the large voter base as trajectory ("growing toward"), not as present fact, until live counts are pulled.
- Audits in-repo are internal/AI-adversarial; no third-party auditor is named. Say "audited internally with published forensics," not "independently audited," unless Big Green Candle's audit work is documented and attached.

## 4. Pre-submission checklist (data prep still to do)

### 4.1 The seat account (blocking)
- [ ] Decide and publish the **candidate seat account**. To earn rewards it must be the account derived from the **validator's master public key** (reward.c gate). Derive it (`master key → AccountID`), fund it, publish r-address + 20-byte AccountID hex in README and vote guide.
- [ ] Decide internal control of that account (multisig? DAO-directed signing policy?) and document how OneXah DAO governance directs its L1 votes (e.g., a dedicated ptype or published council process).
- [ ] Record the validator public key and its dUNL/UNLReport status; capture a `ledger_entry` of the UNLReport showing the validator active.

### 4.2 Chain-verified traffic metrics (the "momentum" evidence)
- [ ] `account_tx` counts + monthly time series for all product accounts (AMM ×3, lending ×2, perps, DAO, LPX staking, Oden's Eye).
- [ ] Unique interacting accounts (proxy for users) across those accounts.
- [ ] Total hook-emitted transaction counts; Cron tick counts; total fees burned by OneXah-related transactions.
- [ ] OneXah share of total Xahau transaction volume over the last 30/90 days — this is the number that either supports or retires the "majority of traffic" claim.
- [ ] Live DAO stats from `/api/public/v1/dao`: staker count, XXX holder count (richlist), proposal/vote participation counts.

### 4.3 People & security (supporting)
- [ ] Short bios + roles + (optional) r-addresses for the full council: Cbot (Cody), Gadget (Mick), 7Rays (Mike), Big Green Candle (Dane) — Big Green Candle's audit work appears nowhere in the repos, so this must be written fresh.
- [ ] Big Green Candle (Dane): document the audit/security work performed so the security section can cite it.
- [ ] Geographic spread of council/validators ("different continents") — one line each, no doxxing needed.

### 4.4 Submission logistics
- [ ] Contact channels for the 8 sitting members (XRPL-Labs, Titanium, Evernode, Digital Governance, GateHub, Projects L2, Community/Dev L2, Exchanges L2) — note the three L2 tables need internal 51% first, so brief their *members*, not just the table.
- [ ] Choose the target seat (proposal currently says S9; S7 also open — S7 carries the "removed auditors" history, S9 is clean).
- [ ] Publish this repo (or a rendered version) as the public manifesto; consider a one-page PDF executive summary for member outreach.
- [ ] Optional: pre-stage the exact Invoke JSON per member with the final AccountID filled in, so a "yes" costs a member five minutes.
