# OMEGA APEX v1.3 — SEPARATE DEPLOYMENT & MIGRATION PROPOSAL (`PREPARE_ONLY`)
**Status:** Proposal Only — Requires Explicit Human Execution Outside the Agent Loop  
**Target Environment:** `/root/.dsh` on DSH-Go `0.2.2-rc.1` (Ubuntu `24.04.5` `aarch64` PRoot)

## 1. Verification in Isolated Workspace (Read-Only, Zero Host Impact)
Unpack `OMEGA_APEX_v1.3_FOUNDATION_REPAIRED.zip` into a clean directory and run the test suite and 9-gate verifier directly via Python 3:
```bash
unzip -o OMEGA_APEX_v1.3_FOUNDATION_REPAIRED.zip
cd omega-apex-v1.3
python3 ./tests/run_foundation_tests.py
python3 ./.bin/spr-verify
```
Expected result: `36/36` tests passed across all `21/21` categories, and `terminal_gate_S: 1` (`9/9 PASS`).

## 2. Optional Host Configuration Migration (Manual Operator Action Only)
*Target:* `/root/.dsh/cordis.patch.yml`  
*Expected Effect:* Switches `defaultPreset` from `danger-full-access` (`approval: never`) to `read-only` (`approval: ask`), sets `maxActiveSubagents: 3`, disables `modelDiscovery` on `tool-subagent`, and configures `mimo-v2.6-flash-free` and `deepseek-v4.1-flash-free` in the subagent allowlist.

### Step 2A — Create Persistent Backups Outside `/tmp`
```bash
mkdir -p /root/.dsh/backups
cp /root/.dsh/cordis.patch.yml /root/.dsh/backups/cordis.patch.yml.pre-v1.3
if [ -f /tmp/web-profile-package.json.pre-agy ]; then
  cp /tmp/web-profile-package.json.pre-agy /root/.dsh/backups/web-profile-package.json.pre-agy
fi
```

### Step 2B — Apply Validated `config/cordis.patch.yml`
```bash
python3 -c "import yaml; yaml.safe_load(open('config/cordis.patch.yml'))" && cp config/cordis.patch.yml /root/.dsh/cordis.patch.yml
```

### Step 2C — Optional Token Harbor (`mimo-v2.6-flash:free`, `deepseek-v4.1-flash:free`) Activation
Once you have your own free Token Harbor key (`thk_...`) from [tokenharbor.ai](https://tokenharbor.ai/), store it in your local environment or `/root/.dsh/.credentials.yaml` (`chmod 600`) and add the `token-harbor` provider block (`baseUrl: "https://tokenharbor.ai/v1"`) under `llm-pi-ai` in `/root/.dsh/cordis.patch.yml`.

### Step 2D — Rollback Plan
```bash
cp /root/.dsh/backups/cordis.patch.yml.pre-v1.3 /root/.dsh/cordis.patch.yml
```
