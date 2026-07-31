# On-Chain Vote Guide — Seating OneXah DAO at the L1 Table

A step-by-step guide for sitting L1 members, per the governance hook installed on the Xahau genesis account. Everything here is sourced from the hook source itself:
**govern.c** — https://github.com/Xahau/xahaud/blob/dev/hook/genesis/govern.c

## The mechanism in one paragraph

The L1 table is 20 seats (`SEAT_COUNT 20`) of hook state on the genesis account `rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh`. Sitting members vote by sending **Invoke transactions** (`ttINVOKE`, TransactionType 99) to the genesis account carrying HookParameters that name a **topic** and a **vote value**. Votes persist in hook state indefinitely — there is no voting period and no expiry. When the number of identical votes on a seat topic reaches **80% of currently filled seats** (integer-truncated, minimum 2), the change executes immediately, inside the same transaction that cast the threshold-crossing vote.

With **8 seats currently filled**, the threshold is `floor(8 × 0.8)` = **6 votes**.

## Current table state (verified on-ledger, July 2026)

| Seat | Holder |
|---|---|
| S0 | XRPL-Labs — `rD74dUPRFNfgnY2NzrxxYRXN4BrfGSN6Mv` |
| S1 | Titanium / Alloy Networks — `rN7XCq12KBvBLKad3wWsVUwmb3dNx1fx3e` |
| S2 | Evernode — `ra7MQw7YoMjUw6thxmSGE6jpAEY3LTHxev` |
| S3 | Digital Governance — `rfMB6RCNdWSB6TJXYwCEU5HvDC2eArJp8h` |
| S4 | GateHub — `r4FF5jjJMS2XqWDyTYStWrgARsj3FjaJ2J` |
| S5 | L2 Table – Projects — `rwyypATD1dQxDbdQjMvrqnsHr2cQw5rjMh` |
| S6 | L2 Table – Community/Dev — `r4FRPZbLnyuVeGiSi1Ap6uaaPvPXYZh1XN` |
| S7 | **Vacant** (Auditors & Enterprise table removed by seat vote — the table's only seat change to date) |
| S8 | L2 Table – Exchanges — `rHsh4MNWJKXN2YGtSf95aEzFYzMqwGiBve` |
| S9–S19 | **Vacant** |

Member count `MC` = 8. Live state is browsable at https://xahau.xrplwin.com/validators/governance and https://xahauexplorer.com/en/governance.

## The vote transaction

Each direct (L1) member submits, from their seat account:

```jsonc
{
  "TransactionType": "Invoke",
  "Account": "<your seat r-address>",
  "Destination": "rHb9CJAWyB4rj91VRWn96DkukG4bwdtyTh",
  "NetworkID": 21337,
  "HookParameters": [
    {
      "HookParameter": {
        "HookParameterName": "54",          // 'T' — topic
        "HookParameterValue": "5309"        // 'S' (0x53) + raw seat byte 0x09 = seat S9
      }
    },
    {
      "HookParameter": {
        "HookParameterName": "56",          // 'V' — vote value
        "HookParameterValue": "<ONEXAH_SEAT_ACCOUNTID_20_BYTES_HEX>"
      }
    }
  ]
}
```

Notes, per `govern.c`:

- **The seat number is a raw byte, not ASCII.** Seat S9 is `0x09` → topic `5309`. (Seat S19 would be `5313`.)
- **`V` is the 20-byte AccountID** (hex) of the candidate account — *not* the r-address string. OneXah's candidate AccountID will be published in the formal submission package.
- **Votes are sticky.** Your vote stays in state until you change it. Re-voting with different data decrements your old tally and increments the new one. Re-submitting an identical vote is a no-op.
- **The 6th identical vote seats the member instantly** — the hook writes the seat↔account mapping, increments `MC`, and OneXah DAO is a member from that ledger forward. No further action needed.
- If the candidate already held another seat it would be moved, not duplicated; and a removed member's outstanding votes are garbage-collected automatically.

### For L2-table seats (S5, S6, S8)

Members of an L2 table vote inside their own table with an additional layer parameter `L` (name `4C`) = `01`, marking it a vote about an L1 topic. When **51%** of the L2 table's members cast the identical vote, the L2 table account automatically emits the corresponding Invoke to the genesis account, counting as that seat's one L1 vote.

## Thresholds reference (from govern.c)

| Action | Threshold |
|---|---|
| Seat change (`S0`–`S19`) | **80%** of filled seats (currently 6 of 8) |
| Hook change (`H0`–`H9`) | 100% of filled seats |
| Reward rate / delay (`RR`/`RD`) | 100% of filled seats |
| L2 table raising an L1 vote | 51% of that table's members |

## Precedent

The mechanism has executed exactly once: seat S7 (Auditors & Enterprise) was removed when 7 of the then-9 members (floor(9 × 0.8) = 7) cast the all-zero delete vote — visible in genesis hook state today. Seating OneXah DAO would be the **first addition** in the table's history, exercising the mechanism precisely as specified at genesis.

## Reward eligibility of the new seat

Per **reward.c** (https://github.com/Xahau/xahaud/blob/dev/hook/genesis/reward.c), each L1 seat earns 1/20th of every user's claimed Balance Adjustment — but only while the seat account (derived from a validator master key) appears in the active-validator list of the on-ledger UNLReport. OneXah's proposed seat account will be derived from Cbot's validator master key, so the seat's rewards are earned by live, verifiable validation — and automatically withheld if we ever fail to perform. The table gives up nothing on trust: the protocol itself enforces our end of the bargain.
