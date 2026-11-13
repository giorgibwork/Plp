# CONSTITUTIONAL CONFLICT REGISTER & FORMAL AMENDMENT PROPOSALS (`OAPX-REG-001`)
**Version:** `1.3.0`  
**Governing Procedure:** `OMEGA_APEX_Supreme_Constitution_v1.1-draft.md`, Article XV §15.1–15.4  
**Rule Enforced:** OMEGA APEX MUST NOT silently rewrite, self-amend, or self-ratify constitutional text (`Article II §2.4`). All conflicts and proposed changes are isolated here for explicit operator decision.

---

## 1. Constitutional & Doctrinal Conflict Register

| Conflict ID | Competing Sources | Exact Discrepancy Observed | Resolution Applied in v1.3 Foundation |
| :--- | :--- | :--- | :--- |
| **`CNF-001`** | `OMEGA_APEX_Supreme_Constitution_v1.1-draft.md` line 5 (`Version: 1.0-draft`) vs. filename & lines 369, 410 (`version 1.1-draft`) | The uploaded v1.1-draft file contains `**Version:** 1.0-draft` in its top metadata block while its filename, operator-decisions table (line 369), and footer (line 410) state `1.1-draft`. | Preserved the uploaded file byte-for-byte in `constitution/OMEGA_APEX_Supreme_Constitution_v1.1-draft.md` (no silent edit); logged formal Amendment Proposal `OAPX-AMD-002` below to normalize line 5 upon operator review. |
| **`CNF-002`** | `OMEGA_APEX_Supreme_Constitution_v1.1-draft.md` Article III §3.5 (`no more than USD 10 per month`) vs. v1.3 Repair Directive §1 (`Current operational budget: $0`) | The unratified constitutional draft allows up to USD 10/month when authorized, whereas the current operational directive sets an active operating budget of **$0.00** (zero purchases, subscriptions, or paid fallbacks). | Per Article III §3.5 (*"This is an operating constraint, not an instruction to consume the entire budget"*) and Article IV §4.3, `.bin/omega-resource` enforces `budget_ceiling_usd = 0.00` immediately as an operational constraint, while `OAPX-AMD-001` proposes the formal constitutional text update. |
| **`CNF-003`** | Legacy `ABSOLUTE-MAX-CONSTITUTION.md` (`v8.0.0-OMEGA`) & `os-core/AGENTS.md` (`v7.0.0`) vs. `OMEGA_APEX_Supreme_Constitution_v1.1-draft.md` | Prior package versions left `ABSOLUTE-MAX-CONSTITUTION.md` (which declared itself "Active Law") and `os-core/AGENTS.md` (which instructed running `spr-verify` via `bash` and allowed `T1`/`T2` auto-execution) in the active directory tree. | Moved all legacy `v7.0`, `v8.0`, `v1.0-draft`, and `v1.2` competing files to `archive/superseded/` and marked them `active_authority: false` in `ARCHIVE_MANIFEST.json`. |
| **`CNF-004`** | Model-privilege wording in v1.2 routing docs vs. `OAPX-CON-001` Article VII §7.1–7.2 (*"No model or provider is constitutionally privileged"*) | v1.2 labeled MiMo-V2.6-Flash as "Ultimate Main Orchestrator" as if constitutionally fixed. | Corrected in v1.3: MiMo (`mimo-v2.6-flash:free` / `mimo-v2.6-flash-free`) and DeepSeek (`deepseek-v4.1-flash:free` / `deepseek-v4.1-flash-free`) are **candidate models** assigned to roles only when qualified by availability, health, and task checks (`Article VII §7.1`). |

---

## 2. Formal Constitutional Amendment Proposals (Article XV §15.2 Format)

### Amendment Proposal `OAPX-AMD-001` — Operational Budget Ceiling Alignment ($10/mo → $0.00/mo)
1. **Exact Text to Change (Article III, Section 3.5):**
   - *Current Text (`v1.1-draft`, lines 98–100):*
     > "The initial operating budget is no more than USD 10 per month for AI subscriptions, subject to future explicit human revision. This is an operating constraint, not an instruction to consume the entire budget. OMEGA MUST NOT initiate a purchase, paid activation, top-up, API balance charge or other paid commitment without specific human authorization."
   - *Proposed Text (`v1.2-draft`):*
     > "The initial operating budget is USD 0.00 per month (strictly free-tier and zero-cost routes only), subject to future explicit human revision. No purchases, subscriptions, paid activations, balance top-ups or paid API fallbacks are permitted. OMEGA MUST NOT initiate any paid commitment or enable any metered route without a prior constitutional or mission budget revision explicitly approved by the human operator."
2. **Reason and Intended Benefit:** Aligns Article III §3.5 with the operator's confirmed $0 current operating budget while eliminating any ambiguity about paid fallbacks.
3. **Articles and Components Affected:** Article III §3.5, Article X §10.1–10.4, `config/provider_integrations.json`, and `.bin/omega-resource`.
4. **Compatibility and Regression Implications:** Disables all paid/metered provider routes (`gemini-4-argon` on Vertex/Gemini API, OpenCode Go $10/mo paid tier). Free routes (`our-free-model`, `Token Harbor :free` once keyed, and existing `google-antigravity` / `agy` free consumer allocation) remain unaffected.
5. **Supporting Evidence:** Evaluated in test category `T15_resource_limit_enforcement` in `tests/run_foundation_tests.py`.
6. **Effective Version and Transition Notes:** Proposed for `v1.2-draft`; until ratified, `.bin/omega-resource` enforces `$0.00` as an explicit current mission constraint under Article IV §4.3(2).

### Amendment Proposal `OAPX-AMD-002` — Header Version Metadata Normalization
1. **Exact Text to Change (Preamble Header, line 5):**
   - *Current Text:* `**Version:** 1.0-draft`
   - *Proposed Text:* `**Version:** 1.1-draft`
2. **Reason and Intended Benefit:** Resolves internal discrepancy between line 5 (`1.0-draft`) and lines 369 and 410 (`1.1-draft`) of `OMEGA_APEX_Supreme_Constitution_v1.1-draft.md`.
3. **Articles and Components Affected:** Preamble metadata header only.
4. **Compatibility and Regression Implications:** None; purely documentary consistency.
5. **Supporting Evidence:** Verified by `diff` between `v1.0-draft` and `v1.1-draft`.
6. **Effective Version and Transition Notes:** Takes effect upon operator acceptance.
