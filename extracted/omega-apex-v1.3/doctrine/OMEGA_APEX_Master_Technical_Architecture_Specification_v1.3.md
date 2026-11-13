# OMEGA APEX — MASTER TECHNICAL ARCHITECTURE SPECIFICATION (`v1.3`)
**Document ID:** `OAPX-SPEC-001`  
**Version:** `1.3` (Supersedes `v0.1` in `archive/superseded/`)  
**Status:** Repaired Foundation Specification (Subordinate to `OMEGA_APEX_Supreme_Constitution_v1.1-draft.md`, which remains **`NOT RATIFIED`**)  
**Operational Budget Constraint:** `USD 0.00/month` (Strict Zero-Spend Ceiling; see `OAPX-AMD-001` in `constitution/CONSTITUTIONAL_CONFLICT_AND_AMENDMENT_REGISTER.md`)  
**Governing Autonomy Mode:** `PREPARE_ONLY` (Fail-closed execution boundary enforced by `.bin/omega-policy`)

---

## 1. Six Architectural Planes & Thirteen Subsystems (Section 9 Alignment)

| Plane | Subsystem # & Name | Responsibility in v1.3 | Implementation Artifact in `omega-apex-v1.3/` | Operational Classification |
| :--- | :--- | :--- | :--- | :--- |
| **Plane A: Control** | **1. Supreme Constitutional Kernel** | Instruction precedence, fail-closed `PREPARE_ONLY` policy evaluation, out-of-band approval verification | `constitution/OMEGA_APEX_Supreme_Constitution_v1.1-draft.md`, `.bin/omega-policy` | `IMPLEMENTED_VERIFIED` |
| **Plane A: Control** | **2. Intent Compiler** | Faithfully translates operator requests into structured Mission and Ticket contracts | `.bin/omega-mission`, `.bin/omega-ticket`, `@deepseek-ai/dsh-plan-mode` | `IMPLEMENTED_VERIFIED` |
| **Plane A: Control** | **3. Mission Kernel** | Authoritative mission/ticket state machine, typed verification checks, bounded retries, checkpoint recovery | `.bin/omega-ticket`, `.bin/omega-mission`, `operations/MISSIONS/`, `operations/TICKETS/` | `IMPLEMENTED_VERIFIED` |
| **Plane A: Control** | **12. Human Command Interface** | Operator interaction, explicit approval boundaries, draft vs. verified status presentation | `AGENTS.md`, DSH-Go Web UI (`127.0.0.1:3080`, `defaultPreset: read-only`) | `IMPLEMENTED_VERIFIED` |
| **Plane B: Cognition** | **4. Cognitive Runtime** | Bounded problem-solving cycle, delegation boundary enforcement, disagreement preservation | `.bin/omega-mission` (`register_delegation`, `record_model_disagreement`) | `IMPLEMENTED_VERIFIED` |
| **Plane B: Cognition** | **6. Context Compiler** | Structure-aware ToC prefix-trie retrieval (`0.00%` structural hallucination), archive exclusion | `.bin/omega-stair`, `memory/omega_toc_trie.json` | `IMPLEMENTED_VERIFIED` |
| **Plane C: Knowledge** | **8. Knowledge & Evidence Fabric** | 9-category truth taxonomy, anti-repetition law, independent verifier check, CaMeL quarantine | `.bin/omega-memory`, `memory/omega_memory.db`, `contracts/MEMORY_AND_EVIDENCE_CONTRACT.md` | `IMPLEMENTED_VERIFIED` |
| **Plane D: Capability & Resources** | **5. Intelligence Fabric** | Candidate model registry (`Token Harbor`, `our-free-model`, `google-antigravity`), qualification states | `config/provider_integrations.json`, `config/cordis.patch.yml` | `IMPLEMENTED_VERIFIED` (`Token Harbor` `BLOCKED` pending key) |
| **Plane D: Capability & Resources** | **7. Capability Gateway** | Pre-execution action classification, path-boundary enforcement, zero `shell=True` execution | `.bin/omega-policy`, `.bin/omega-ticket` (`TypedCheckSpec`) | `IMPLEMENTED_VERIFIED` |
| **Plane D: Capability & Resources** | **10. Resource Intelligence** | `$0.00` budget ceiling enforcement, provider vs. local usage separation, route circuit breaker | `.bin/omega-resource`, `operations/RESOURCE_LEDGER.json` | `IMPLEMENTED_VERIFIED` |
| **Plane E: Assurance** | **9. Assurance & Evaluation** | 21-category unit/adversarial test suite, dynamic metric calculation, 9-gate static/runtime verifier | `tests/run_foundation_tests.py`, `.bin/omega-eval`, `.bin/spr-verify` | `IMPLEMENTED_VERIFIED` |
| **Plane E: Assurance** | **11. Reliability & Observability** | Append-only policy decision journal, test receipts, idempotent crash reconciliation | `receipts/events/POLICY_DECISION_JOURNAL.jsonl`, `.bin/omega-ticket reconcile` | `IMPLEMENTED_VERIFIED` |
| **Plane F: Evolution** | **13. Evolution Laboratory** | Proposal-only evaluation gate (`auto_applied_to_production: False`), regression blocking | `.bin/omega-rsi`, `proposals/SEPARATE_DEPLOYMENT_AND_MIGRATION_PROPOSAL.md` | `IMPLEMENTED_VERIFIED` |

---

## 2. Fail-Closed Policy & Approval Architecture (Section 5 Specification)

1. **Why CLI Flags Are Rejected:** Any CLI flag (`--human-approved`, `--approve`, `--operator-confirm`) or fixed string (`RATIFY_OR_APPROVE`) can be synthesized by an LLM agent invoking `tool-bash`. `.bin/omega-policy` scans `sys.argv` before argument parsing and returns `DENY_SPOOF_ATTEMPT` (exit code `2`) whenever any such token appears.
2. **Real DSH-Go Execution Boundary Analysis:**
   - Inside DSH-Go `0.2.2-rc.1`, `@deepseek-ai/dsh-permission-presets` controls whether the Web UI prompts the human before invoking `tool-bash` or `tool-fs`. Setting `defaultPreset: read-only` (`sandbox: read-only`, `approval: ask`) in `config/cordis.patch.yml` enforces read-only containment at the host boundary.
   - Because DSH-Go `0.2.2-rc.1` does not expose a cryptographic hardware/UI approval socket to subprocesses inside PRoot, `.bin/omega-policy` **fails closed (`DENY_FAIL_CLOSED_NO_HOST_APPROVAL_CHANNEL`)** on all `OP_CONSEQUENTIAL_EXEC` requests unless an out-of-band operator HMAC key is mounted at `/run/omega_operator_oob.key` (outside the project workspace) and a signed, unexpired, unrevoked, single-use nonce `ApprovalRecord` matches the exact `proposal_digest`.

---

## 3. Constrained Typed Ticket Verification (Section 6 Specification)

`omega-ticket` contains **zero `shell=True` calls**. All ticket acceptance checks must use `TypedCheckSpec`:
- `file_exists`: Verifies target file exists within workspace boundary (rejecting `..` traversal and shell metacharacters `[;|&$\`><\n\r]`).
- `file_sha256`: Verifies exact SHA-256 hex digest of a workspace file.
- `json_valid`: Parses JSON file and verifies presence of `required_keys`.
- `yaml_valid`: Parses YAML file via `yaml.safe_load` and checks top-level type (`list` or `dict`).
- `config_key_equals`: Traverses parsed JSON/YAML data structures in memory to verify exact configuration values.
- `test_result_present`: Reads a structured test receipt JSON and checks `passed_tests >= min_passed` and `failed_tests <= max_failed`.
- `allowlisted_readonly_validator`: Executes only fixed allowlisted scripts (`spr-verify`) via `subprocess.run([sys.executable, fixed_path], shell=False)`.
