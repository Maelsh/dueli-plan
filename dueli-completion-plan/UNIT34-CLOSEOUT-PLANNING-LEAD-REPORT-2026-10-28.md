# UNIT34 — Closeout and Planning Lead Handoff
**Date:** 2026-10-28  
**Code PR:** [Maelsh/dueli-opus#146](https://github.com/Maelsh/dueli-opus/pull/146)  
**Approved code HEAD:** `cf93f9b1a1d12d8c6aaf280679cd40658d909909`  
**Actual merge SHA:** `a6c1802ba66e2f175d6642693e0afd3f8eff9685`  
**Plan baseline at execution:** `dc5bc1efd7d94dfa1c19604b7277b8104cdb93ad`

## Final status
UNIT34 / R4-DB-MEASURE-1 is **CODE MERGED** after two independent REMOTE APPROVE reports and direct GitHub verification of exact PR head/base and successful pre-merge checks. PR #146 is closed/merged. Pre-merge Quality Gate run [40622691772](https://github.com/Maelsh/dueli-opus/actions/runs/40622691772) succeeded; Deploy workflow [40622691784](https://github.com/Maelsh/dueli-opus/actions/runs/40622691784) succeeded as a workflow but production deployment was **SKIPPED** and Preview only. The merged SHA's post-merge workflow evidence is not yet available in the connector at the time of this report; therefore do not label UNIT34 deployed or production verified until exact-SHA post-merge Quality/Deploy evidence is confirmed.

PR #110 remains OPEN/HOLD and untouched. UNIT35 and UNIT35.1 have not started; keep them blocked until UNIT34 is closed in the canonical path after post-merge gates and documentation.

## UNIT34 measurement figures (local synthetic Vitest / SQLite shim)
These are the numeric counts reported by the implementation's local statement counter, **not Cloudflare D1 billing metrics**.

| Journey / measurement | Reported local figure | Meaning / limitation |
|---|---:|---|
| Home rail T0 session creation | 13 SQL statements | Local synthetic run |
| Home rail continuation page | 5 SQL statements | Local synthetic run |
| Explore T0 | 13 SQL statements | Local synthetic run |
| Explore continuation | 5 SQL statements | Local synthetic run |
| Guest suggested rail cold path | 13 SQL statements | Local synthetic run |
| Guest suggested rail cache hit path | 8 SQL statements | Module/test path only; cache is not wired into session T0 |
| searchCompetitions | 6 SQL statements | Local synthetic run |
| searchUsers | 9 SQL statements | Local synthetic run |
| H7 loadCompetitions | 1 SQL statement | Synthetic test path |
| H7 profiles | 3 SQL statements | Synthetic test path |
| H7 viewerCtx | 0 statements | Guest fixture follows an empty path; not a general production claim |
| SSE poll / sse_event_log | Measured by harness; numeric value not present in committed summary table | Re-run/report numeric sample if required for comparable baseline |
| GET /api/notifications | Measured by harness; numeric value not present in committed summary table | Same limitation |
| chunk_index timeline + seek/timeLookup | Measured by harness; numeric value not present in committed summary table | Same limitation |
| UserSignalsModel.loadUsers | Measured by harness; numeric value not present in committed summary table | Same limitation |
| Competitions EXPLAIN QUERY PLAN | Sample measured; index path: `idx_competitions_status_started` | Query plan text, not a row count |

**Actual Cloudflare D1 `rowsRead` / `rowsWritten`: unavailable for all journeys in UNIT34.** No production experiments were run. SQLite `rowsReadApprox` / `rowsWrittenApprox` are approximations from the local shim only and must never be reported as D1 analytics/billing values. The committed report states that cold/warm and T0/continuation counts are machine/run-dependent; figures above should be treated as the reported local sample, not a stable performance guarantee.

## Accepted engineering decisions
- Ordered-ID cache was removed from `CategoryRailProvider.buildOrderedIds`; it remains uncached to preserve each new session's fresh T0 snapshot. Do not reattach `PublicSurfaceCache` to T0/session freezing.
- `PublicSurfaceCache` remains an isolated in-isolate utility with six key dimensions (`surface`, `category`, `subcategory`, `status`, `lang`, `policy_version`) and 15-second default TTL. It is not currently imported by production read paths. Any future production attachment must define explicit invalidation and be reviewed separately.
- Bounded Home rail retry: max 2 attempts with 350 ms × attempt backoff; final failure remains visible/retryable.
- Logging: request ID validation/generation, structured 5xx logging, redaction and generic user-facing errors.
- Local validation from reports: 76/76 focused tests; TypeScript and build passed. REMOTE additionally reports full suite 2170 passed / 1 skipped and Linux quality-gate-poll 8/8; pre-merge CI Quality Gate is green.

## Non-blocking follow-ups / planning disposition
1. **P3 — duplicate structured error logs:** same 500 can produce both controller/unhandled and HTTP_5XX records. Correlation remains possible via requestId; optional future log deduplication.
2. **P3 — legacy raw `console.error` paths:** older controller logs remain unstructured; pre-existing and outside this PR. Consider only in a scoped logging-hardening task.
3. **P3 — redact allowlist:** keyword-based redaction may not suppress every internal error label (REMOTE specifically noted `D1_ERROR` can appear in a detail field); verify against the current spec and, if needed, tighten in a dedicated security-hardening task. No secrets/PII leak was demonstrated by REMOTE.
4. **P3 — docs:** make explicit the owner/technical-lead approval gate before UNIT40 for the numeric budget/table, and distinguish playlist from timeline/seek journey naming. Documentation-only follow-up.
5. **Production analytics:** obtain real D1 rowsRead/rowsWritten via approved staged traffic / Cloudflare analytics later; must not use uncontrolled production experiments.
6. **Production cache integration:** only on safe public read paths with explicit invalidation; not T0 session IDs.
7. **Windows `jq` polling tests:** reported local environment issue; Linux CI is authoritative for current gate. Do not reopen UNIT34 absent new evidence.

These are follow-ups, not reasons to reopen the accepted code or delay the current merge. They must not be promoted into new top-level UNITs without a planning decision.

## Scope protections
- No H7 weights/policy change, schema migration, finance, ads, or MySQL migration.
- PR #110 remains OPEN/HOLD.
- Do not start UNIT35 / UNIT35.1 until post-merge checks are confirmed and the canonical plan marks UNIT34 closed.
