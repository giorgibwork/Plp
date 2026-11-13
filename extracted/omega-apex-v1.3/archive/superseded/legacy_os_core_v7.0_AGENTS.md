# DSH-Go Host Execution Specification (v7.0.0 — Zero-Persona Deterministic State Machine)
# Target Runtime: google-antigravity/antigravity-gemini-3.7-flash (primary) & 3.8-flash (secondary)
# Prefix-Stability Contract: Keep this file byte-static across turns to preserve >95% KV cache hits.

## 1. Deterministic Trigger -> Tool Chain -> Evidence Artifact Rules

| Input Trigger / Task Class | Mandatory Tool Chain (Execute in Exact Sequence) | Required Evidence Artifact Before Synthesis | Prohibited Shortcuts (Automatic S=0 Failure) |
| :--- | :--- | :--- | :--- |
| **A. Any Video / `.mp4` / Gallery / Exercise Identification Query** | 1. Run `/root/workspace/.bin/video-contact-sheet "<video_path>"` (or `--gallery` for multi-video folders) via `bash`.<br>2. Call native `read_file` on the generated `/root/workspace/research/video-inspect/contact_*.jpg` (or `gallery_sheet_*.jpg`). | Visual pixels loaded via native `read_file` + optical-flow telemetry header (`STATIC_POSE`, `GLOBAL_CAMERA_PAN`, or `LOCALIZED_ARTICULATION`) in `last_video_sheet.json`. | - Guessing video contents from filenames (`gym_edit_remade.mp4`, `VID_*.mp4`).<br>- Running `cv2.absdiff` in `bash` without calling `read_file` on saved `.jpg` contact sheets. |
| **B. Any External Fact, Training Protocol, Athlete Method, or Science Claim** | 1. Call native `web_search` tool AND/OR run `/root/workspace/.bin/live-research "<explicit query>"` via `bash`.<br>2. Inspect `/root/workspace/research/last_grounding.json`. | Verified URLs, PMIDs/DOIs, or transcripts in `last_grounding.json` with `sources_count > 0` (`gate_S: 1`). | - Synthesizing athlete logs (e.g. Devon Larratt) or papers from parametric memory when search returns `[]`.<br>- Hardcoding queries or swallowing network errors with `sys.exit(0)`. |
| **C. Any Reference to Another Chat Session or Earlier Turn** | 1. Run `/root/workspace/.bin/global-memory-sync` via `bash`.<br>2. Run `/root/workspace/.bin/chat-grep --latest [session_keyword] 15` (or `chat-grep "<query>"`). | Exact `Turn N`, `seq`, `USER` prompt, and `ASST` response retrieved from `/root/.dsh/sessions/` or SQLite FTS5 (`pagegram_store.db`). | - Guessing what happened in another chat without running `chat-grep`.<br>- Reading only `USER` prompts while ignoring `ASST` responses. |
| **D. Creating or Modifying Any Script, Binary, or Config** | 1. Write complete, functional code.<br>2. Run `/root/workspace/.bin/spr-verify` via `bash`. | `/tmp/.dsh_s1_receipt.json` with `terminal_gate_S: 1` and valid HMAC-SHA256 signature across all 6 gates. | - Writing `<=3` line `print()` stubs, `time.sleep` fake swarms, or `# Pad issues` arrays.<br>- Claiming `S=1` in text when `spr-verify` exited non-zero or was not run. |
| **E. Updating an Existing Domain Blueprint (`08-elite-engines`)** | 1. Read `/root/workspace/08-elite-engines/DOMAIN_MANIFEST.json`.<br>2. Edit the canonical `master_file` in place (e.g., `11-FULLY-OPTIMIZED-HOOK-MASTER-PLAN.md`) and sync to `/sdcard/Download/DSH-Go/`. | Updated canonical file passing `spr-verify`. | - Creating fragmented addendum files (`10-...-ADDENDUM.md`) or resurrecting archived 5-set drafts from `08-elite-engines/archive/`. |

## 2. Fail-Closed Output Rules
1. **Language & Format:** English only. Zero theatrical roleplay, zero sycophantic validation, and zero unverified claims. Every technical response must cite exact file paths, line numbers, or retrieved URLs.
2. **Fail-Closed Reporting (`S=0`):** When a tool fails, returns `[]`, or lacks visual confirmation, output `Gate=S=0 (BLOCKED: <exact tool output>)`. Never fabricate data to satisfy a user prompt.

## 3. Environment & Path Reference
- **Workspace:** `/root/workspace` | **Deliverables:** `/sdcard/Download/DSH-Go/`
- **Core CLI Tools (`/root/workspace/.bin`):** `video-contact-sheet`, `live-research`, `global-memory-sync`, `chat-grep`, `spr-verify`, `auto-checkpoint`, `hcp-invariant-checker`, `kinetic-preproc`, `pagegram-mem`, `pagegram-guard`, `os-daemon`.
- **Canonical Domain Manifest:** `/root/workspace/08-elite-engines/DOMAIN_MANIFEST.json`.
