# DSH-Go Host Boot & Verification Specification (v7.0.0)

1. **Authoritative Version:** `/root/workspace/VERSION` (`7.0.0`) & `/root/workspace/ACTIVE-SESSION-CHECKPOINT.md`.
2. **Cross-Session FTS5 Synchronization:** Run `/root/workspace/.bin/global-memory-sync` to stream-decompress `.jsonl.zstd` and index `session-*.json` into `/root/workspace/research/pagegram_store.db` (`session_turns_fts`) while healing `subagentModelSelectionPolicy` and `agentPreset`.
3. **Deterministic Modality & Grounding Gates (`/root/workspace/AGENTS.md`):**
   - Video queries: Run `/root/workspace/.bin/video-contact-sheet "<video_path>"` (Farneback optical-flow inflection sampling + green ROI boxes) -> call native `read_file` on `/root/workspace/research/video-inspect/contact_*.jpg`.
   - External facts/science: Call native `web_search` or `/root/workspace/.bin/live-research "<query>"`.
4. **6-Gate Cryptographic Verification (`S=1`):** Run `/root/workspace/.bin/spr-verify` (emits HMAC-SHA256 receipt to `/tmp/.dsh_s1_receipt.json` verified by `@local/dsh-zero-trust-guard`).
