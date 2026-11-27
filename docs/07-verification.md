# 07 — Build, verification and release

Use Windows 11 x64 interactive VM/workstation. Verify stable .NET 10 SDK and matching Windows App SDK, Windows SDK, Visual Studio Build Tools/MSBuild with WinUI workloads. Record exact versions and supported Windows builds in docs/compatibility.md. Pin dependencies, lock/restore as appropriate. Do not invent a compatibility matrix. CI on Windows runner: restore, MSBuild solution build (x64), deterministic unit tests, publish smoke check. Native interactive tests opt-in; no auto-login/credential fixture on shared runners. scripts/build.ps1, test.ps1, publish.ps1 fail nonzero on errors and output clear paths. Verify unpackaged self-contained configuration for both .NET and Windows App SDK (WindowsPackageType=None, WindowsAppSDKSelfContained=true and appropriate runtime settings; verify with selected SDK). Publish folder ZIP, no installer required, no auto-elevation or execution policy changes. Run clean Windows VM without development SDKs; check dependencies and note any required Windows system runtime. Do not promise SmartScreen-free unsigned download. Include LICENSE only after explicit owner license selection; dependency notices required regardless.

## Mandatory acceptance matrix (record evidence and exact build)

| ID | Test |
|---|---|
| D01 | Create, rename, bind, switch native desktops. External Task View/Ctrl+Win+arrows refreshes correct local pins; global pins persist. Orphan and removal confirmation safe. |
| D02 | Dock stays visible across desktops, shell restart, resume; no focus steal; unsupported adapter yields honest global fallback. |
| U01 | Default centered freestanding rounded capsule, visible bottom gap, dynamic width, overflow; no full-width visual/input bar; desktop behind edges remains interactive. |
| U02 | Supplementary above native taskbar; primary near bottom with native auto-hide; native reveal/Start/system UI work; fallback when auto-hide off, mode switch, recovery/Exit. |
| U03 | DPI 100/125/150/200, monitor changes, fullscreen, maximized windows, theme/high contrast/reduced motion, optional AppBar reserve tested or explicitly disabled. |
| G01 | Create mixed group incl. UNC folder and EXE, .lnk, URL and nested group; anchored popup above button, click leaf only, Esc/outside/desktop switch closes. |
| G02 | Explorer drag/drop, reorder, move/copy, keyboard/Narrator, overflow; no cycle; offline UNC not blocking. |
| L01 | Local/UNC normal EXE; args, cwd, Unicode; local/UNC folders and files; scripts honor policy; URL validation. |
| L02 | UAC elevation and cancellation, 740 and access denied; Tavi itself standard user. |
| L03 | Full alternate user local + UNC incl. alternate-only ACL, actual identity shown in TestTarget; cancel/invalid credentials; no secret in config/process args/log. |
| L04 | Network-only local identity unchanged, target-share authorization tested; wrong creds, 1219, mapped-drive and offline-share errors safe. |
| W01 | Start workspace, optional once/session normal auto-start, cancel/switch-away stops pending entries; no unintended relaunch/reuse. |
| W02 | Match running window on correct desktop, normal/maximized placement restoration, singleton/elevated/other-user ambiguity reports unverified. |
| P01 | JSON save/reload, Unicode UNC, backup recovery, corrupt schema, portable export/import preview; imports do not execute/probe/start automatically. |
| R01 | CI build/test and clean x64 Windows 11 portable ZIP smoke; single instance, tray recovery, exit cleanup, no leaked AppBar registration. |

Run representative at least two supported Windows 11 build families if accessible; publish only actually validated builds. Any unavailable test is NOT RUN, not pass. Core acceptance blocker: cannot call V1 complete if any mandatory feature fails; optional reserve-space/effects may be disabled with clear limitation and baseline floating dock intact. Capture sanitized screenshots of both dock modes and mixed group; no real paths/credentials. Record automated commands, exit codes, manual test results, limitations, version and release artifact hash.
