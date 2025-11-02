# ZenZone — System Guardian Pro

A pure‑Python, single‑loop system utility that monitors system health, detects anomalies, predicts trends, performs safe prioritized cleanup, and reports results — all with zero external dependencies.

Highlights
- Single `while` loop orchestrates everything (constraint friendly)
- < 500 lines (currently 498) and pure Python only
- Safe demo mode and one‑shot CLI for quick verification

Quick Start
- Local interactive: `python system_guardian_pro.py`
- Safe demo (auto‑stop, no deletions): `./run_demo.sh` or `DEMO=1 python system_guardian_pro.py`
- One‑shot CLI (no loop):
  - `python system_guardian_pro.py status | report | alerts | optimize | cleanup [--yes]`

Codespaces
- Open in GitHub Codespaces → Terminal → `./run_demo.sh`
- Do: run one‑shot commands for quick checks
- Don’t: elevate privileges or add external packages — not required

Features
- Monitoring: CPU/memory/disk, health score, trend analysis
- Cleanup: target discovery with age/size/type/location priority and safety checks
- Optimization: cache cleanup and garbage‑collection tuning
- Reporting: detailed text reports saved as `guardian_report_YYYYMMDD_HHMMSS.txt`

Interactive Commands
- `status` — show CPU/memory/disk and health
- `report` — full ML/anomaly/trend report
- `cleanup` — scan targets; confirm to delete (disabled in demo)
- `config` — view configuration
- `alerts` — threshold, anomaly, and predictive alerts
- `optimize` — apply optimizations and update score
- `quit` — exit and save a report

Configuration
- Uses `guardian_config.json` if present; otherwise sensible defaults
- Key settings: monitor interval, thresholds, temp directories, max file age, auto‑cleanup

Data Sources & Accuracy
- Disk usage and filesystem scanning: real, via `shutil.disk_usage` and `pathlib` walks
- CPU usage: heuristic from computation timing (pure Python)
- Memory usage: heuristic from Python object counts + GC
- Processes: simulated and clearly labeled “SIMULATED PROCESSES”
- Anomalies/trends: real statistics (mean/std dev, 2‑sigma, simple slope)

Safety
- Demo mode (`DEMO=1`): safe — no deletions, faster cycles, auto‑stop (30 by default; set `DEMO_CYCLES`)
- Full mode: deletions require explicit confirmation or `cleanup --yes`
- Multi‑step safety checks avoid system files and large binaries

Architecture
- One `while` loop handles monitoring, thresholds, cleanup windows, optimizations, user I/O, and periodic reporting
- Lightweight, dependency‑free design suitable for constrained environments

Constraint Compliance
- Lines: 498/500
- Loops: single main loop
- Dependencies: standard library only

Troubleshooting
- If `./run_demo.sh` isn’t executable: `bash run_demo.sh` or `chmod +x run_demo.sh`
- Windows line endings: `dos2unix run_demo.sh` (if needed)
- Suppress live status flicker by using one‑shot CLI commands
