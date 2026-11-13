# OMEGA APEX v1.3 — CANONICAL DOCUMENT HIERARCHY & INDEX
**Document ID:** `OAPX-IDX-001`  
**Version:** `1.3.0`  
**Status:** Approved Project Index  
**Date:** `2026-11-13`

## 1. Governing Authority Precedence Rules (Article IV §4.3 & Article XV §15.1)
1. **Supreme Constitutional Draft (`OAPX-CON-001`, `v1.1-draft`):** Highest governing design reference within OMEGA APEX (`constitution/OMEGA_APEX_Supreme_Constitution_v1.1-draft.md`). **Explicit Status: `NOT RATIFIED` (`draft`).** No agent, script, or subsystem may represent this draft as ratified until the human operator explicitly ratifies a specific version.
2. **Operational Directive Constraints (`$0.00` Budget & `PREPARE_ONLY`):** Active current human mission instructions (Article IV §4.3 Level 2). Where current operational constraints (`$0.00` budget ceiling) are stricter than the unratified draft text (`USD 10/month` in Article III §3.5), the stricter `$0.00` operational constraint governs runtime execution while formal Amendment Proposal `OAPX-AMD-001` awaits operator review.
3. **Parent Conceptual Doctrine (`OAPX-VIS-001`, `v0.1`):** `doctrine/OMEGA_APEX_Vision_and_Foundational_Doctrine_v0.1.md`.
4. **Master Technical Architecture Specification (`OAPX-SPEC-001`, `v1.3`):** `doctrine/OMEGA_APEX_Master_Technical_Architecture_Specification_v1.3.md`. Subordinate to the Constitution; translates articles into concrete schemas, deterministic validators, and host boundaries.
5. **Runtime Agent & Subsystem Contracts (`AGENTS.md`, `contracts/*`, `config/*`):** Subordinate implementation files.
6. **Archived Historical Documents (`archive/superseded/*`):** Retained strictly for audit traceability (`Article XV §15.3`). Excluded from active policy and STAIR retrieval indices.

## 2. Canonical Document Registry

| Document ID | File Path | Version | Status | Authority & Parent Document | Applicable Subsystem | Relationship to Other Governing Documents |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `OAPX-CON-001` | `constitution/OMEGA_APEX_Supreme_Constitution_v1.1-draft.md` | `1.1-draft` (internal header notes `1.0-draft` — see `OAPX-AMD-002`) | **`draft` (`NOT RATIFIED`)** | Human Operator (Sole Constitutional Approver); Parent: `OAPX-VIS-001` | Subsystem 1: Supreme Constitutional Kernel (All Subsystems 1–13 subordinate) | Outranks all technical specs, agent instructions, and model outputs within OMEGA. |
| `OAPX-REG-001` | `constitution/CONSTITUTIONAL_CONFLICT_AND_AMENDMENT_REGISTER.md` | `1.3.0` | **`proposed`** | Subordinate to `OAPX-CON-001` (Article XV §15.2 procedure) | Subsystem 1: Supreme Constitutional Kernel | Records version metadata discrepancies and formal Amendment Proposals (`OAPX-AMD-001`, `OAPX-AMD-002`) without silently altering `OAPX-CON-001`. |
| `OAPX-VIS-001` | `doctrine/OMEGA_APEX_Vision_and_Foundational_Doctrine_v0.1.md` | `0.1` | **`approved` (Foundational Conceptual Doctrine)** | Human Operator | All 6 Planes & Subsystems 1–13 | Parent conceptual doctrine for `OAPX-CON-001` and `OAPX-SPEC-001`. |
| `OAPX-SPEC-001` | `doctrine/OMEGA_APEX_Master_Technical_Architecture_Specification_v1.3.md` | `1.3` | **`proposed` (Repaired Architecture Spec)** | Subordinate to `OAPX-CON-001` & `OAPX-VIS-001` | All 13 Subsystems | Supersedes `archive/superseded/OMEGA_APEX_Master_Technical_Architecture_Specification_v0.1.md`. |
| `OAPX-AGT-001` | `AGENTS.md` | `1.3.0` | **`proposed`** | Subordinate to `OAPX-CON-001` & `OAPX-SPEC-001` | Subsystems 2, 4, 5, 12 (Cognitive Runtime & Interface) | Replaces legacy `v7.0`/`v8.0` `AGENTS.md` and `os-core/AGENTS.md`. |
| `OAPX-CFG-001` | `config/cordis.patch.yml` | `1.3.0` | **`proposed` (Prepare-Only Proposal)** | Subordinate to `OAPX-CON-001` Article V & `OAPX-SPEC-001` | Subsystems 5, 7, 10 (Intelligence, Capability Gateway, Resource Intelligence) | Repaired valid YAML patch sequence for DSH-Go `0.2.2-rc.1`; not applied to live `/root/.dsh` without human action. |
| `OAPX-CFG-002` | `config/provider_integrations.json` | `1.3.0` | **`proposed`** | Subordinate to `OAPX-SPEC-001` §9 & Article X | Subsystem 5 & 10 (Intelligence Fabric & Resource Governance) | Defines verified vs. blocked routes (`Token Harbor`, `our-free-model`, `google-antigravity`, `agy`) under the `$0.00` budget ceiling. |
| `OAPX-ARC-001` | `archive/superseded/ARCHIVE_MANIFEST.json` | `1.3.0` | **`superseded` (Archive Index)** | Historical Reference Only (`Article XV §15.3`) | None (Inactive) | Catalogues superseded `v1.0-draft`, `v0.1`, `v1.2`, `v7.0`, and `v8.0` documents so they cannot compete with `OAPX-CON-001`. |
