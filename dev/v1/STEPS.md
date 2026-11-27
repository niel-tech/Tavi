# Ordered coding tasks

## S01 — Feasibility and contracts

On interactive Windows 11 x64, inventory OS build, SDKs, available MSBuild, choose compatible stable Windows App SDK and desktop adapter after checking license/source. Create small WinUI app plus TestTarget. Prove native enumeration/current/create/rename/switch/change notifications, visibility across desktops, permitted window query/move. Prove shaped rounded centered HWND, anchored popup, DPI conversion, native taskbar visible/auto-hidden modes including native reveal; optional reservation separate. Prove normal/UNC/UAC/otherUser/netOnly launch including alternate-only UNC ACL and real TestTarget identity. Investigate safe helper only if necessary (docs/05). Record exact results, native failure codes and fallback choices in docs/compatibility.md. Exit: successful evidence or explicitly blocked; no pretending. Resolve API decisions before production integration.

## S02 — Solution, domain and persistence

Create proposed solution/projects, pinned toolchain, DI, resource files, analyzers, .gitignore, scripts and Windows CI skeleton. Implement enums ItemKind, LaunchMode, DockMode, ReusePolicy, capability/error results, Workspace, DockSettings, Pin/Group, StartupPolicy; typed ports from architecture. Pure validation and ordered tree operations. JSON schema/example, atomic store, backup/import/export with review state. Unit tests for IDs/cycles/order, path types and unsafe schemes, roundtrip/backup/corrupt/version/import. Minimal WinUI Settings and tray recovery; run build/test. Exit: clean compile, unit tests pass, new config roundtrip.

## S03 — Native desktops

Implement verified adapter behind interface, STA/native lifetime and notifications, capability checks, fallback. Workspace editor CRUD/bind/create/rebind, removal confirmation, active desktop state updates, globals for unbound. Fake adapter unit tests for stale GUID, event storms, external switches, unavailable service. Actual Windows tests D01/D02. Exit: dock state changes from real external switch without app restart.

## S04 — Floating dock and display modes

Implement actual bounded WinUI capsule window, content measurement, rounded geometry, DPI, centering/gaps, max width, scroll/overflow, hover and theme, no taskbar button for dock if tested. Workspace selector, global/local separation, Add/settings, native icon placeholder. Both display modes from docs/04, native auto-hide guidance, safe fallback, fullscreen and taskbar recreation. Optional work-area reservation gated by proof, no full-width visible bar or click-blocking outside capsule. Unit-test geometry using varied monitor origins/scaling; manual U01–U03. Exit: real floating dock in both modes, native controls accessible, recovery works.

## S05 — Groups and editing

Implement anchored Flyout/Popup above clicked group with dynamic grid, breadcrumb/back, mixed entry types, hover/keyboard/scroll/overflow, focus restore. Settings tree + detail form and validation. Drag/drop Explorer paths and shortcuts; async icon resolver with cancellation/cache, never UI thread UNC IO. Reorder and recursive copy/move with new IDs on copy. Per-entry mode controls capability-aware. Test tree invariants and G01/G02; capture sanitized UI screenshots. Exit: create mixed group and launch selection through S06 wiring (until then show explicit not implemented, not fake success).

## S06 — Launcher and identity

Implement type validation, command line quoting and process launch; normal local/UNC EXE and shell associations; .lnk/.url inspection, PS1 safe host, RDP. UAC runas, ephemeral credential prompt, full otherUser/network-only API; verified local helper if needed. Explicit unsupported mode for Explorer associations, no credentials persistence. Asynchronous UNC, per-entry result/error mapping and redacted diagnostics. Tests for quotes/paths/mode matrices, cancellation and identity semantics; manual L01–L04. Exit: actual TestTarget verifies args/cwd/token and target UNC access, no secrets in exported data.

## S07 — Window tracking and workspace startup

Enumerate eligible windows and subscribe changes; correlate PID/start time and verified lineage; desktop association, running dots and unpinned windows in primary mode, chooser, activate/minimize, placement capture/restore. Bounded startup coordinator with explicit user action and one-time optional normal auto-start; switch-away cancels pending, no forced focus. Structured per-entry results. Fake scheduler tests cancellation/reuse/timeouts; real W01/W02. Exit: launch selected workspace apps and folders, observe matched windows on correct desktop, honest unknown states for unsupported apps.

## S08 — Polish, release and handoff

Complete all acceptance IDs in docs/07, recovery, single-instance/exit disposal, high contrast and language resources, diagnostics review, clean Windows smoke, publish script and zip. Add compatibility docs, screenshots and user guide; ensure no real credentials/paths. Verify CI result and clean checkout restore/build/test/publish. Set version 1.0.0 only if gates pass, else preview version and explicit blockers. Report commits, exact commands/exit codes, manual OS matrix, archive location/hash. Do not push additional changes outside human-authorized branch or make a release tag without authorization.

## Definition of done

Every task: tests and evidence, docs kept accurate, PROGRESS updated, build result and known limitations. Never silently defer mandatory features. No architecture shortcut that removes floating design, mixed groups, native desktop binding or required identity routes.
