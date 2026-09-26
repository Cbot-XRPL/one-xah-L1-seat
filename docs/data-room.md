# Data Room - Verified Facts, Sources, and Pre-Submission Checklist

This file is the data-prep backbone for the proposal. §1-§3 are verified facts with sources. §4 is the open checklist of numbers and artifacts to gather **before** the formal submission goes to sitting members.

---

## 1. Xahau governance - verified spec facts

Verified against the governance hook source and live ledger state (via `account_namespace` on the genesis account, July 2026).

| Fact | Value | Source |
|---|---|---|
| Governance account | `rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh` (genesis) | govern.c |
| L1 seats | 20 (`SEAT_COUNT 20`) | govern.c |
| Filled seats / `MC` | 8 | live hook state |
| Vacant seats | S7, S9-S19 (12 seats) | live hook state |
| Seat-change threshold | 80% of filled seats, floor, min 2 → currently **6 of 8** | govern.c lines ~372-393 |
| Hook / reward-param threshold | 100% of filled seats | govern.c |
| L2 → L1 raise threshold | 51% of L2 members | govern.c |
| Vote transport | `ttINVOKE` (99) with HookParameters `T`/`V` (+`L` on L2) | govern.c header spec |
| Seat topic encoding | `'S'` (0x53) + raw seat byte (S9 = `5309`) | govern.c |
| Vote persistence | indefinite, no expiry; threshold-crossing vote executes in-line | govern.c |
| Reward rate `RR` | 0.00333333… /month ≈ 4% p.a. (unchanged since genesis) | live state; XahauGenesis.h |
| Reward delay `RD` | 2,600,000 s ≈ 30.09 days | live state; XahauGenesis.h |
| L1 member reward | 1/20th of each user's claimed Balance Adjustment per claim | reward.c; whitepaper |
| Member reward gate | seat account must be validator-master-key-derived AND in UNLReport active list | reward.c lines ~265-267 |
| Precedent | S7 removed by 7-of-9 vote (only seat change ever); no member ever added | live hook state |

**Primary sources:**
- https://github.com/Xahau/xahaud/blob/dev/hook/genesis/govern.c
- https://github.com/Xahau/xahaud/blob/dev/hook/genesis/reward.c
- https://github.com/Xahau/xahaud/blob/dev/src/xrpld/app/tx/detail/XahauGenesis.h
- https://xahau.network/docs/features/governance-game
- https://xahau.network/Xahau-Whitepaper.pdf
- Secondary: https://xaman.app/blog/decoding-xahau-the-governance-game , https://gatehub.net/blog/the-genesis-of-xahau-an-overview-of-key-governance-and-mechanisms/
- Explorers: https://xahau.xrplwin.com/validators/governance , https://xahauexplorer.com/en/governance

**Caveat:** some secondary summaries garble the thresholds. Cite `govern.c` (seats 80%, hooks/rewards 100%, L2 raise 51%) - the source is unambiguous.

## 2. OneXah - verified facts (from the `100-2` repo)

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
1. Escape-hatch recovery primitive (`ai/library/escape-hatch.md`) - 22/22 testnet E2E, live on 5 accounts.
2. Xahau Cron mechanics research (`ai/library/ba-cron.md`) - `lsfTshCollect` + `hsfCOLLECT` + Cron pseudo-tx requirement set, documented from scratch.
3. Oden's Eye security registry + raven guards (freeze-only, fail-open, DAO-governed), live on 6 products.
4. Standalone DAO-free AMM/lending/perps suite with live mainnet reference deployments.
5. Fully published raw wire format (`llms.txt`) - keyless, anti-lock-in, AI-agent-friendly.

## 2.5 Cbot Labs infrastructure and Xahau Vault - verified facts

Sources are the operator's own repos on this box: `Xahau-Hub` (cluster provisioning), `cbot-labs` (the public site), `xahau-vault` (marketplace stack).

### Public node cluster (`Xahau-Hub`, `cbotlabs.xyz`)

| Fact | Value | Source |
|---|---|---|
| Public endpoints | `https://cluster.cbotlabs.xyz` (RPC, POST-only), `wss://ws-cluster.cbotlabs.xyz` (WS), `https://cbotlabs.xyz/api/cluster` (status JSON) | `Xahau-Hub/README.md`; `cbot-labs/cluster.html` |
| Phase | Phase 1 - two nodes live; node 3 in `inventory.yml`, `enabled: false`, pending 384 GB RAM + 4 TB NVMe | `inventory.yml`, `docs/PHASE-2.md` |
| Nodes | `xah-node-1` deep (700 GiB DB, `ledger_history` 3.5M target), `xah-node-2` api (300 GiB, 500k) | `inventory.yml` |
| Host | R740 / `pve2`, 2x Xeon Gold 6154 (36C/72T), 128 GB now / 384 GB planned, PERC H740P RAID 10, 256 GiB pool reserve kept unprovisioned | `Xahau-Hub/README.md` |
| Validator isolation | The UNL validator (CT 200 on a **different** host) is a hard-coded forbidden target in `lib/guard.sh`; 35 guard assertions fail the build if a guard stops refusing | `inventory.yml` `cluster.host.forbidden`, `make guards` |
| Path | Cloudflare Tunnel → nginx rate limiter → `xah-node-2`; no port forward, WAN IP never published | `Xahau-Hub/README.md`, `proxy/npm-notes.md` |
| Rate limit | 15 req/s + burst 30 per client, 8 WS connections. Load-verified: 178 req/s in → 43 served, 157 x 429 | `ops/install-ratelimit.sh`, README |
| Hardening verified end to end 2026-09-13 | `server_info`, `fee`, `ledger`, `ledger_current`, `ledger_closed`, `account_info`, `account_tx`, `ping` all `success` over the public name; WS upgrades to 101 and pushes `ledgerClosed`; `can_delete` / `stop` → **403**; admin port refuses network connections | `Xahau-Hub/README.md` |
| Nature of the nodes | Stock `xahaud`, **non-validating**. Trust is the published Xahau UNL, not the operator | `cbot-labs/cluster.html` |
| Stated availability | Best effort, **no SLA**, published as such on the page | `cbot-labs/cluster.html` |
| Observed live state (2026-09-25) | 2/2 nodes online, validated ledger 26,078,107, deep node history window 657,308 ledgers / api node 104,088, 12 peers, build `2026.6.21-release+3350` | cluster page screenshot |

**Open item:** upload bandwidth for a public WS endpoint on the home connection is still **UNMEASURED** and is flagged in `Xahau-Hub/README.md` as the open question before promoting the endpoint widely. Do not promise capacity in the submission; describe it as best-effort and growing.

### Price oracle (`roratatoAYHjnDY5Fhc3uCvDy2Y3oeQQf`, https://onexah.io/oracle)

XLS-47d `PriceOracle` objects on Xahau mainnet. Publisher: `server/lib/price-oracle-publisher.js` in the One Xahau repo; page `OraclePage.jsx`; API `https://onexah.io/api/public/v1/oracle` (keyless, returns the live values, the publisher workers and the recent post hashes).

| Fact | Value | Source |
|---|---|---|
| Oracle account | `roratatoAYHjnDY5Fhc3uCvDy2Y3oeQQf` | live API |
| Doc 1 (`currency`) | `XAH/USD`, `XRP/USD`, `EVR/USD`, `XXX/USD`, `RVN/USD` in one atomic `OracleSet` per tick | changelog 2026-08-01 |
| Doc 1 sourcing | XAH + XRP = two-source average (CoinGecko + Bitrue); EVR/XXX/RVN priced off AMM reserves x the XAH anchor via plain RPC reads | changelog 2026-08-01 |
| Doc 2 (`earth`) | `CO2/PPM` (NOAA Mauna Loa), `SST/DGC` + `GAT/DGC` (ClimateReanalyzer), `ICE/MKM` (NSIDC), `KPX/IDX` (SWPC Kp), `EQK/MAG` (USGS largest M4.5+ in 24 h) - keyless agency sources | changelog 2026-08-02 |
| Publishers | worker A `rUXUHA1HALSrj9R7fNrsELHQRP3MZDXxLT` (Cbot Labs) and worker B `rJ9AtQqQcJTBdhQChTbP97rS7ceUEXkFmK` (Evernode container, also the decentralized-host mirror of onexah.io). B only publishes once A's document passes its stale gate - A healthy carries both docs, A down and B carries both. | live API; changelog 2026-08-02 |
| Freshness | ledger-enforced: `LastUpdateTime` within +/-300 s of close time and monotonic. Publisher-side: XAH anchor failure skips the whole tick; each pair carries a bounded last-good fill because an `OracleSet` omitting a pair **deletes** it | xls47 playbook; changelog 2026-08-01 |
| Readable by any hook | object index `SHA512Half(0x0052 \|\| owner AccountID \|\| OracleDocumentID)`; `slot_set` takes the 32-byte index, so a foreign oracle is readable with no permission | `ai/library/xls47-price-oracle-playbook.md` |
| Reserve | doc 1 (5 pairs) 1 owner reserve, doc 2 (6 pairs) 2 owner reserves | XLS-47 spec |

**Claim discipline:** the repo supports "one of the first XLS-47d price oracles on Xahau mainnet" and every technical detail above. It does **not** yet support "the only one" - that needs the check in §4.3b. The perps hook's AMM-reserve "oracle" is a different thing (an internal price read, not a published feed); do not conflate them.

### Public hook releases (`cbot-labs-hooks`)

Repo: https://github.com/Cbot-XRPL/cbot-labs-hooks (public). Each release ships hook source + compiled `.wasm` + a one-command Node installer with a dry-run mode that verifies the binary hash before submitting; the installer signs with the operator's own local `SEED` and transmits no key.

| Release | Path | What it does | Status |
|---|---|---|---|
| **ba-cron** | `basic/ba-cron/` | `AccountSet SetFlag 11` (`lsfTshCollect`) + `SetHook` (`hsfCOLLECT`) + `CronSet` (~30 d, `RepeatCount 256`, self-re-arming) → emits `ClaimReward` on each tick; the `GenesisMint` credits one ledger later. `HookOn` covers only `Cron(92)`, `SetHook(22)`, `Invoke(99)` - Payment and OfferCreate bits are off. Writes no hook state. | Live on mainnet |
| **uritoken-broker** | `basic/uritoken-broker/` | Buyer `Payment` with `NFTID` + `BUY` → `URITokenBuy` → `Remit` to buyer → net fee `Payment`; refunds a failed buy. Mirror of https://github.com/Cbot-XRPL/xahau-uritoken-broker (v3.0.0, hook hash `9D39BF3D`). | Live on mainnet |
| **amm-v2** | `defi/pools/amm-v2/` | Constant-product XAH ⇄ IOU pool; LP shares as an IOU, bps swap fee, optional DAO fee escrow, DEX offer mirroring. Hook hash `E000F5F04A0A1CABCAF6ECDA617E8E743BAF1C9F57EE0A7B8FF066CF95DED5C7`, 56,628 B. The exact build on `rAMMznwkgL1BB6o4eYWufMAdy6t1LPgnf`, `rLPXFdgvriFHXt7WYybqJSu49Ff5DRzq1u`, `rRLPRi86xXjq8QmuvcpUfN6dg3etmCNHT`. | Live on mainnet |

**Audit status, exactly as the repo states it:** `basic/` hooks are **not audited**; **amm-v2 has been through an external audit with the tracker private and fixes in source**. That is a stronger statement than anything in §2 and it is still **not** an "independently audited protocol" claim - it covers one hook, and the report is not published. Permitted phrasing: "the AMM hook has been through an external audit (tracker private, fixes in source)". Not permitted: "our hooks are externally audited", "audited protocol".

### Xahau Vault (`xahau-vault`, `xahauvault.com`)

- Marketplace + wallet + crawler stack for Xahau NFTs: metadata resolution, local media cache, admin crawl jobs, creator profiles, launchpad, Studio and Contract Engine creation lanes, XRPL↔Xahau bridge flow.
- Self-hosted: Express API + built Vite frontend + crawler worker + bridge worker under pm2 on the operator's own VM; Prisma/Postgres DB-first with a JSON fallback path. `docs/deployment/local-dev-to-vm.md`.
- **Hooks written in-house** (`src/hooks/*`, each with preserved known-good source + wasm and recorded hashes):
  - *Ephemeral broker* - buy-now clearing: buyer `Payment` with `NFTID`+`BUY` → `URITokenBuy` → `Remit` → net fee out. Known-good snapshot 2026-03-29, source hash `E54D0932…FEFD0A4`, wasm `46CD2C4B…FE3C9D493`. `docs/hooks/ephemeral-broker-hook.md`.
  - *NFT swap hook* - two-sided bundle swap, 1-4 tokens a side (v5; mainnet runs v4.1 one-for-one). Open or counterparty-named listings, un-ready / change / kick / reclaim paths, fee up-flow. Settlement is **atomic in one ledger**. `docs/hooks/nft-swap-hook.md`.
  - *NFT auction hook* - timed bundle auctions, min bid + increment, buy-now, anti-snipe extension, anyone-can-close, credit-and-withdraw for refunds the ledger rejects. Built 2026-09-25, HookHash `93D1165F…F84B6AD`, **testnet 69/69**. Hook only - not on mainnet. `docs/hooks/nft-auction-hook.md`.
  - *NFT contract + fee routes* - mint/remit with callback-confirmed mint state and up to 4 net-of-cost fee-route wallets. Snapshot 2026-04-01, source `37006C5C…181FE7A5`, wasm `4A0275FE…2B519E24`. `docs/hooks/xahau-nft-contract-fee-routes.md`.
- Mainnet settlement audit (2026-09-25): two swaps 109 s apart at ledgers 26,074,464 / 26,074,496; per-swap XAH movement is exactly the 0.2 XAH URIToken owner reserve per token; the hook nets ~-0.0004 XAH (its own tx fees) and **takes no reserve**; fee sweep to the up-flow account matched the documented KEEP. `ai/current-state.md`.
- Open/read API and an MCP connector let a holder's own Claude or ChatGPT read their wallet and draft trades; **the AI can never sign** - every trade tool stops at a Xaman payload.

**Framing guardrails for this section:** the auction hook is **testnet-only** - do not describe it as live. Node 3 is **planned**, not running. The cluster is **non-validating** and **no-SLA**; say "free, keyless, best-effort, growing," never "production RPC for the ecosystem." Vault mainnet claims are limited to the broker, the swap hook (v4.1) and the contract hooks.

## 3. Framing guardrails (keep the proposal honest)

- **Who holds the seat:** Cbot Labs, as validator and infrastructure operator. Do **not** write the proposal as though the DAO holds the seat or directs its rewards - it does not, and a member who reads the DAO's on-chain rules will see that no such mechanism exists. The honest framing is in README §2.5: the operator runs and funds the infrastructure **and the community systems on top of it** (One Xahau, the marketplace, the faucet, the open APIs, support) and is the gate on what the seat earns; much of that spend flows back out into the ecosystem (SetHook fees on live-hook fixes, test runs, new protocols, tips, releases), and One Xahau benefits along with everyone else - but as a consequence of how the operator spends, not as an entitlement. Protocol X keeps its own treasury and its own vote. The precedent to lean on is how the table already works - seat rewards sustain the member's infrastructure - stated generally, without naming another member.
- **Do not over-promise decentralization.** "Community-governed" is true of the Protocol X products (treasury, proposals, council co-sign, product multisigs). It is not true of the validator, the cluster, the Vault deployment, or the seat account - those are operator-run, and saying otherwise is the kind of claim due diligence dismantles.

- **Do not claim "majority of Xahau traffic"** until §4.2 produces chain-verified numbers. Current defensible phrasing: "one of the largest sources of diverse, organic transactional traffic."
- **Voter counts:** repo documents council of 3 (+admin) and active stakers, not "100s-1000s of voters." Frame the large voter base as trajectory ("growing toward"), not as present fact, until live counts are pulled.
- Audits in-repo are internal/AI-adversarial; no third-party auditor is named. Say "audited internally with published forensics," **never "independently audited."**
- **Kairo Vault Technologies' security work (Dane Brown, council seat) does not unlock an independence claim** - he holds a council seat, so the work is insider work, however reproducible. Documenting it (now done, see [security-review.md](security-review.md)) lets the proposal describe a **published, reproducible verification method** with byte-exact source-to-deployment results; it does **not** let it say "independently audited" or "third-party audited." An independence claim requires commissioning a reviewer with no council seat and no governance stake. See [security-review.md §0](security-review.md#0-independence--read-this-before-citing-anything-below) for the exact permitted phrasings - an overstated independence claim discovered during member due diligence would discount the whole submission.

## 4. Pre-submission checklist (data prep still to do)

### 4.1 The seat account (blocking)
- [ ] Decide and publish the **candidate seat account**. To earn rewards it must be the account derived from the **validator's master public key** (reward.c gate). Derive it (`master key → AccountID`), fund it, publish r-address + 20-byte AccountID hex in README and vote guide.
- [ ] Decide internal control of that account (multisig? published signing policy?) and document how community input **informs** its L1 votes - a consultation and publication process, not a claim that the DAO controls the seat (see §3 guardrails and README §2.5).
- [ ] Record the validator public key and its dUNL/UNLReport status; capture a `ledger_entry` of the UNLReport showing the validator active.

### 4.2 Chain-verified traffic metrics (the "momentum" evidence)
- [ ] `account_tx` counts + monthly time series for all product accounts (AMM ×3, lending ×2, perps, DAO, LPX staking, Oden's Eye).
- [ ] Unique interacting accounts (proxy for users) across those accounts.
- [ ] Total hook-emitted transaction counts; Cron tick counts; total fees burned by OneXah-related transactions.
- [ ] OneXah share of total Xahau transaction volume over the last 30/90 days - this is the number that either supports or retires the "majority of traffic" claim.
- [ ] Live DAO stats from `/api/public/v1/dao`: staker count, XXX holder count (richlist), proposal/vote participation counts.

### 4.3 People & security (supporting)
- [ ] Short bios + roles + (optional) r-addresses for the full council: Cbot (Cody), gadget78 (Mick), 7Rays (Mike), Dane Brown - Kairo Vault Technologies GK (Huge Green Candle).
- [x] Dane Brown (Kairo Vault Technologies GK): audit/security work documented → **[docs/security-review.md](security-review.md)**; current live builds in **[docs/live-hooks.md](live-hooks.md)**.
- [ ] Decide whether the fleet-sweep provenance notes are disclosed in the proposal or held for member due diligence on request - project's call; security-review.md states they exist and are available on request.
- [ ] Geographic spread of council/validators ("different continents") - one line each, no doxxing needed.

### 4.3b Infrastructure evidence (cluster + Vault)
- [ ] Measure and record **upload bandwidth** on the cluster's public path - the one open question in `Xahau-Hub/README.md` before the endpoint is promoted to members.
- [ ] Capture an uptime/availability window for `cluster.cbotlabs.xyz` (e.g. 30 days of `/api/cluster` polling) so the "public infrastructure" claim carries a number.
- [ ] Record node 3's arrival (RAM + NVMe) if it lands before submission - it turns "two nodes, a third planned" into "three nodes".
- [ ] Pull chain-verified counts for the Vault hook accounts (broker, swap escrow) the same way as §4.2, so the NFT side has its own traffic evidence.
- [ ] Decide whether the auction hook ships to mainnet before submission; if not, keep it described as testnet-proven.
- [ ] Before claiming "the only" XAH/USD oracle: scan mainnet for other `PriceOracle` (0x0080) objects and record what you find. Until then the proposal says "one of the first", which the repo supports.
- [ ] Capture a week of oracle uptime (post cadence + how often worker B had to take over) - it is the cleanest evidence that the Evernode backup is real and not decorative.

### 4.4 Submission logistics
- [ ] Contact channels for the 8 sitting members (XRPL-Labs, Titanium, Evernode, Digital Governance, GateHub, Projects L2, Community/Dev L2, Exchanges L2) - note the three L2 tables need internal 51% first, so brief their *members*, not just the table.
- [ ] Choose the target seat (proposal currently says S9; S7 also open - S7 carries the "removed auditors" history, S9 is clean).
- [ ] Publish this repo (or a rendered version) as the public manifesto; consider a one-page PDF executive summary for member outreach.
- [ ] Optional: pre-stage the exact Invoke JSON per member with the final AccountID filled in, so a "yes" costs a member five minutes.
