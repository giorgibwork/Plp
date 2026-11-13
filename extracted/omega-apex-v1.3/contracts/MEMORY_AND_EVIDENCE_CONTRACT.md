# MEMORY, PROVENANCE & EVIDENCE CONTRACT (`v1.3`)
**Executable Engine:** `.bin/omega-memory` (`memory/omega_memory.db`)  
**Governing Articles:** `OMEGA_APEX_Supreme_Constitution_v1.1-draft.md`, Articles VII (§7.4–7.5), VIII (§8.1–8.5), IX (§9.1–9.4)

## 1. Nine Mandatory Truth Categories (Article VIII §8.2)
Every knowledge record stored in `omega_memory.db` must carry one of these nine categories:
1. `directly_observed`: Inspected directly by a deterministic read-only tool in the current environment.
2. `externally_sourced`: Retrieved from an identified primary external document or URL (`source_ref`).
3. `independently_verified`: Checked by a deterministic test or an independent verifier (`verifier_actor != author_actor`) with a recorded `evidence_ref`.
4. `inferred`: Derived logically from observed facts but not directly observed.
5. `estimated`: Approximate quantitative figure (such as unverified token or quota estimates).
6. `assumed`: Working assumption stated explicitly for planning.
7. `disputed`: Contradicted by another model, source, or observation (or quarantined for injection).
8. `stale`: Past its `stale_after` freshness timestamp; requires revalidation before use.
9. `unknown`: Unresolved fact or unverified host capability.

## 2. Anti-Repetition & Anti-Self-Verification Invariants
- **Repetition Never Upgrades Truth (Article VIII §8.3):** Re-storing an `assumed`, `inferred`, `estimated`, or `unknown` record increments `repetition_count` but is mechanically blocked from upgrading `truth_category` to `directly_observed` or `independently_verified` without an independent `verifier_actor` and `evidence_ref`.
- **Author Cannot Self-Verify (Article VII §7.4):** `.bin/omega-memory` returns `REJECTED_SELF_VERIFICATION` if `verifier_actor == author_actor` when requesting `independently_verified`.
