# V1 — Execution plan

Goal: ship a working native Windows 11 workspace manager, version 1.0.0, not just a mockup. Read AGENTS.md and docs in order. Follow STEPS.md sequentially; each task has an exit gate. Maintain PROGRESS.md; don't mark a task complete without evidence. Review git status and keep commits scoped. The planning commit on main does not authorize unsafe native modifications.

Execution order: S01 feasibility, S02 foundation/persistence, S03 desktop management, S04 floating dock/modes, S05 editor and groups, S06 launcher identities, S07 window/workspace orchestration, S08 integration/release. Customization (docs/08-customization.md) is mandatory V1 scope across S02–S05 and S08; the checked-in vector assets must be integrated, not merely documented. The first spike may use throwaway code under spikes/; promote only proven parts. On unavailable Windows host, implement/test platform-neutral tasks but record S01 and native gates blocked; do not claim native support. Complete mandatory gates before final release.

Start agent with START-PROMPT.md.
