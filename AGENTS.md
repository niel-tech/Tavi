# Instructions for implementation agents

1. Read README, all docs chapters and dev/v1 before coding. Planning is not implementation.
2. Follow task order. Start with Windows feasibility; do not fake native desktops or successful launches. Maintain a compiling vertical slice after each task.
3. C#/.NET 10 LTS, WinUI 3, stable compatible Windows App SDK. Pin exact resolved versions, document sources and dependency licenses. No preview dependencies without explicit approval.
4. Separate domain, application, native adapters and UI. Native calls behind typed interfaces. Use async cancellable IO, DispatcherQueue, deterministic disposal and safe handles.
5. Tavi runs unelevated. Respect UAC, ACLs, execution policies and network authentication. Never save passwords, pass them via CLI or logs, inject into Explorer, patch native taskbar internals, kill Explorer or silently switch identity. Imported entries never execute automatically.
6. After each task: build, test, update docs and PROGRESS with commands, results, actual Windows build and blockers. Interactive Windows tests cannot be substituted by Linux or headless CI.
7. Preserve native desktops and user processes. Never remove desktops or close apps implicitly. Provide a working fallback if OS integration fails.
8. No real credentials, internal paths, local settings or build outputs in Git. Review diff. Commit logical slices per human instructions; no force pushes.
9. Verify API/dependency behavior from official docs/source; document deviations. Do not drop mandatory requirements silently.
10. Final report: commits, completed and pending tasks, actual tests/compatibility, release artifact and blockers. V1 complete only after mandatory acceptance checks pass.
