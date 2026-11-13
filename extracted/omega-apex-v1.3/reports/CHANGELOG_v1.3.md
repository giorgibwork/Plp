# OMEGA APEX v1.3 — COMPLETE REPAIR CHANGELOG (`CHANGELOG_v1.3.md`)
**Version:** `1.3.0-OMEGA-APEX-FOUNDATION`  
**Date:** `2026-11-13`

## Exact Files Added, Repaired, or Archived

1. **`CANONICAL_DOCUMENT_INDEX.md` (Added):** Establishes one unambiguous governing document hierarchy with `OAPX-CON-001` (`v1.1-draft`, `NOT RATIFIED`) at the top.
2. **`constitution/OMEGA_APEX_Supreme_Constitution_v1.1-draft.md` (Preserved Active Draft):** Preserved byte-for-byte in `NOT RATIFIED` status without silent edits.
3. **`constitution/CONSTITUTIONAL_CONFLICT_AND_AMENDMENT_REGISTER.md` (Added):** Documents conflicts `CNF-001`–`CNF-004` and formal Article XV §15.2 Amendment Proposals `OAPX-AMD-001` ($10/mo → $0/mo budget ceiling) and `OAPX-AMD-002` (header version `1.0-draft` → `1.1-draft`).
4. **`archive/superseded/*` & `ARCHIVE_MANIFEST.json` (Archived):** Moved competing `v1.0-draft`, `v0.1` tech spec, `v1.2` composite spec, `v8.0` `ABSOLUTE-MAX-CONSTITUTION.md`, `ABSOLUTE_MAX_OMEGA_DOCTRINE.md`, and legacy `os-core/` duplicates out of the active tree and excluded them from STAIR indexing.
5. **`config/cordis.patch.yml` & `cordis.patch.yml` (Repaired):** Fixed line 73 YAML `ScannerError` (`@deepseek-ai/...`), restored valid top-level YAML list structure for DSH-Go `0.2.2-rc.1`, and set `defaultPreset: read-only` (`approval: ask`).
6. **`config/provider_integrations.json` (Added):** Documented and validated `Token Harbor` (`https://tokenharbor.ai/v1`, `mimo-v2.6-flash:free`, `deepseek-v4.1-flash:free`, marked `BLOCKED` pending `TOKENHARBOR_API_KEY`), `our-free-model` (`mimo-v2.6-flash-free`, `deepseek-v4.1-flash-free`), `google-antigravity`, and disabled paid routes under the `$0.00` budget.
7. **`.bin/omega-policy` (Rewritten):** Removed CLI spoof flags (`--human-approved`, `--operator-confirm`); implemented fail-closed execution boundary with out-of-band HMAC-SHA256 verification, proposal digest binding, expiration, revocation, and single-use replay nonces.
8. **`.bin/omega-ticket` (Rewritten):** Eliminated all `subprocess.run(..., shell=True)` calls; implemented `TypedCheckSpec`, immutable contract digest check, T0–T3 consistency, bounded retries, expiration, step-nonce deduplication, and idempotent crash reconciliation.
9. **`.bin/omega-mission` (Added):** Implemented full Mission Contracts, delegation scope/ring boundary validation, model disagreement preservation (`Article VII §7.5`), and 7-level instruction precedence resolution (`Article IV §4.3`).
10. **`.bin/omega-memory` (Rewritten):** Implemented all 9 truth categories (`Article VIII §8.2`), anti-repetition rule (`Article VIII §8.3`), independent verifier check (`verifier_actor != author_actor`), freshness TTL, project boundary isolation, and CaMeL injection quarantine.
11. **`.bin/omega-resource` (Added):** Implemented `$0.00` operational budget ceiling, separation of provider allowance vs. measured vs. estimated usage, and route circuit breaking.
12. **`.bin/omega-stair` & `.bin/omega-rsi` (Repaired):** Excluded `archive/superseded/` from STAIR prefix-trie indexing and locked RSI laboratory to proposal-only output (`auto_applied_to_production: False`).
13. **`tests/run_foundation_tests.py`, `.bin/omega-eval` & `.bin/spr-verify` (Rewritten):** Replaced hardcoded metrics and duplicated tests with a 21-category (36-test) unit and adversarial test suite and 9-gate independent verifier.
