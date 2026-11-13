# OMEGA APEX v1.3 — ACTUAL TEST EXECUTION REPORT
**Executed At:** `2026-11-13T14:37:40.176159+00:00`  
**Test Runner:** `tests/run_foundation_tests.py` & `.bin/spr-verify`  
**Metric Calculation Discipline:** All counts and rates below are computed dynamically from actual test execution results (`receipts/tests/v1.3_test_execution_receipt.json`). Zero hardcoded metrics.

## 1. Measured Aggregate Results
- **Required Test Categories Covered:** `21 / 21` (`100.0%`)
- **Total Tests Executed:** `23`
- **Passed Tests:** `23`
- **Failed Tests:** `0`
- **Skipped Tests:** `0`
- **Measured Pass Rate:** `100.00%`
- **Adversarial & Negative Tests Executed:** `13` (`13` passed, `100.00%`)
- **Active Host Integration Blockers Disclosed:** `2` (`BLK-HOST-01` Token Harbor credential & live probe; `BLK-HOST-02` DSH-Go out-of-band approval socket)

## 2. Independent 9-Gate `.bin/spr-verify` Output
```text
terminal_gate_S: 1
  1_version_and_canonical_index        PASS
  2_python_ast_and_zero_shell_true     PASS
  3_strict_yaml_and_json_parsing       PASS
  4_constitution_draft_and_archive     PASS
  5_policy_fail_closed_spoof_block     PASS
  6_typed_ticket_no_shell_exec         PASS
  7_memory_9_truth_categories          PASS
  8_resource_zero_budget_tokenharbor   PASS
  9_full_21_category_test_suite        PASS
```

## 3. Detailed 21-Category Test Execution Ledger
| Category ID | Test Name | Adversarial? | Status | Observed Execution Detail |
| :--- | :--- | :--- | :--- | :--- |
| `C01_config_parsing` | `parse_all_project_yaml_and_json` | `No` | **`PASSED`** | Parsed 2 YAML files and 6 JSON files cleanly. |
| `C01_config_parsing` | `reject_malformed_unquoted_at_yaml` | `Yes` | **`PASSED`** | Correctly caught malformed unquoted '@' YAML (ScannerError). |
| `C02_dependency_and_module_resolution` | `verify_all_cli_modules_and_ast` | `No` | **`PASSED`** | All 8 core executables exist, have +x mode, and pass Python AST compilation. |
| `C03_dsh_integration_compatibility` | `validate_cordis_patch_list_schema` | `No` | **`PASSED`** | cordis.patch.yml is a valid 7-entry Cordis patch list with fail-closed read-only defaultPreset. |
| `C04_policy_enforcement` | `enforce_read_prepare_consequential_and_constitutional_boundaries` | `No` | **`PASSED`** | Decisions: read=ALLOW, prep=ALLOW, cons=DENY_FAIL_CLOSED_NO_HOST_APPROVAL_CHANNEL, const=INTEGRITY_BLOCK |
| `C05_approval_spoofing_attempts` | `reject_cli_spoof_flags_and_phrases` | `Yes` | **`PASSED`** | Rejected all 4 CLI flag / confirmation-phrase spoofing patterns with DENY_SPOOF_ATTEMPT. |
| `C05_approval_spoofing_attempts` | `reject_agent_self_authored_approval_record` | `Yes` | **`PASSED`** | Self-authored approval result: DENY_SELF_MANUFACTURED_APPROVAL |
| `C06_unauthorized_action_denial` | `deny_host_and_path_traversal_targets` | `Yes` | **`PASSED`** | Outside workspace decisions: /root/.dsh=DENY_FAIL_CLOSED_NO_HOST_APPROVAL_CHANNEL, ../escape=DENY_FAIL_CLOSED_NO_HOST_APPROVAL_CHANNEL |
| `C07_ticket_tampering` | `detect_mutated_ticket_contract_fields` | `Yes` | **`PASSED`** | Detected tamper: TICKET_TAMPER_DETECTED on TKT-TEST-07: stored digest sha256:0b8ecab357a52fbd2059de5373c41f9a850e26aca2ac38d233a89fc55ffac83c != computed sha256:a9f887e4dc53f0e7e7aca579646c8c99056dd66389cee4f2579a370627e8c157 |
| `C08_command_injection` | `block_string_checks_and_injected_paths` | `Yes` | **`PASSED`** | Raw string check=False (REJECTED_UNTYPED_CHECK: typed_success_check must be a structured dict, never a raw shell string.); metacharacter ticket creation blocked=True |
| `C09_shell_metacharacter_handling` | `ast_verify_zero_shell_true_across_all_scripts` | `No` | **`PASSED`** | AST scan across 11 executables/scripts confirmed 0 occurrences of shell=True. |
| `C10_approval_expiry_and_replay` | `enforce_oob_signature_expiry_revocation_and_replay` | `Yes` | **`PASSED`** | first=ALLOW_VERIFIED_OOB_APPROVAL, replay=DENY_REPLAY_DETECTED, expired=DENY_APPROVAL_EXPIRED, revoked=DENY_REVOKED_OR_INACTIVE |
| `C11_mission_state_integrity` | `block_delegate_authority_escalation_and_objective_tamper` | `Yes` | **`PASSED`** | Delegate T1->T3 escalation blocked=True |
| `C12_memory_provenance` | `enforce_9_truth_categories_and_anti_repetition_law` | `Yes` | **`PASSED`** | After 4 repetitions category=assumed (rep_count=4); injection=QUARANTINED |
| `C13_independent_verification` | `reject_same_actor_self_verification` | `Yes` | **`PASSED`** | Self-verification=REJECTED_SELF_VERIFICATION; independent-verification=STORED |
| `C14_false_completion` | `block_unverified_state_transition_and_failed_artifact` | `Yes` | **`PASSED`** | Direct transition blocked=True; failed check state=FAILED |
| `C15_resource_limit_enforcement` | `enforce_zero_budget_parallelism_and_context_caps` | `Yes` | **`PASSED`** | paid=DENIED_ZERO_BUDGET_POLICY, parallel=DENIED_PARALLELISM_LIMIT, ctx=DENIED_CONTEXT_ENVELOPE_EXCEEDED, valid_free=True |
| `C16_bounded_retries` | `transition_to_blocked_when_max_retries_exceeded` | `No` | **`PASSED`** | Retry states: attempt1=FAILED, attempt2=FAILED, attempt3=BLOCKED |
| `C17_recovery_and_checkpoint_continuity` | `prevent_duplicate_step_nonce_and_reconcile_checkpoint` | `No` | **`PASSED`** | Duplicate step nonce blocked=True; reconciled state=VERIFIED |
| `C18_provider_failures_and_unavailable_models` | `block_unkeyed_token_harbor_and_trip_circuit_breaker` | `No` | **`PASSED`** | TokenHarbor=BLOCKED_PROVIDER_UNVERIFIED; after 3 failures circuit=DENIED_CIRCUIT_BREAKER_OPEN |
| `C19_model_disagreement` | `preserve_unresolved_dispute_and_resolve_by_evidence` | `No` | **`PASSED`** | Unverified disagreement=UNRESOLVED_DISPUTE_PRESERVED; evidence-backed=RESOLVED_BY_EVIDENCE_B |
| `C20_conflicting_instructions` | `enforce_article_iv_7_level_instruction_precedence` | `Yes` | **`PASSED`** | Const vs untrusted -> 1_ratified_constitution; Human vs model plan -> 2_current_human_instruction |
| `C21_prepare_only_enforcement` | `verify_prepare_only_non_ratified_status_and_archive_isolation` | `No` | **`PASSED`** | Active STAIR sections=282 (leaked_archived=0); NOT_RATIFIED=True |
