# AGENTS.md — OMEGA APEX v1.3 OPERATIONAL INSTRUCTIONS
**Governing Authority:** Subordinate to `constitution/OMEGA_APEX_Supreme_Constitution_v1.1-draft.md` (`Status: NOT RATIFIED`) and `CANONICAL_DOCUMENT_INDEX.md`.  
**Autonomy Boundary:** `PREPARE_ONLY` (Article III §3.3 & Article V).  
**Operational Budget Ceiling:** `USD 0.00` (Zero paid API calls, subscriptions, or balance top-ups).

## 1. Mandatory Rules for All Agents & Models
1. **No Self-Ratification or Self-Granted Privilege:** Never represent `OMEGA_APEX_Supreme_Constitution_v1.1-draft.md` as ratified. Never pass `--human-approved`, `--approve`, or confirmation strings to `.bin/omega-policy`.
2. **Model Neutrality (Article VII §7.1):** `mimo-v2.6-flash:free` / `mimo-v2.6-flash-free` and `deepseek-v4.1-flash:free` / `deepseek-v4.1-flash-free` are candidate models assigned by task suitability and verified availability, not constitutionally privileged authorities.
3. **Direct Disagreement (Article IV §4.5):** When an instruction or assumption conflicts with observed host evidence, state the challenged premise, the evidence, the consequence, the safest alternative, and confidence level directly.
4. **Invoke Python Verifiers Directly:** Always invoke `./.bin/spr-verify`, `./.bin/omega-eval`, `./.bin/omega-ticket`, `./.bin/omega-policy`, `./.bin/omega-memory`, `./.bin/omega-resource`, and `./.bin/omega-stair` via Python 3 (`python3 ./.bin/spr-verify`), never via `bash ./.bin/spr-verify`.
5. **Truth & Verification Honesty (Article VIII §8.2 & Article IX §9.3):** Label all claims using the 9 truth categories (`directly_observed`, `externally_sourced`, `independently_verified`, `inferred`, `estimated`, `assumed`, `disputed`, `stale`, `unknown`) and 5 deliverable statuses (`Draft`, `Reviewed`, `Verified`, `Blocked`, `Rejected`).
