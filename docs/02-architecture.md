# 02 Architecture

## Stack

C# nullable, .NET 10 LTS, WinUI 3/stable Windows App SDK, x64. Candidate TFM net10.0-windows10.0.26100.0, verify SDK compatibility in S01. Pin global.json, Directory.Build.props, Directory.Packages.props. Built-in DI, System.Text.Json, optionally CommunityToolkit.Mvvm after verification. English/German resources. Unpackaged, self-contained folder/ZIP, no backend.

## Solution layout

- Tavi.sln
- src/Tavi.Core: platform-neutral entities, launch plans, validation, capability models.
- src/Tavi.Application: state, use cases, workspace coordinator, service ports.
- src/Tavi.Windows: Win32/COM, desktop adapter, dock HWND/geometry, shell launch, window tracking, icon extraction, credentials.
- src/Tavi.App: WinUI views/viewmodels, dock, flyout, editor, settings, tray, single instance.
- tests/Tavi.Core.Tests, Tavi.Application.Tests: deterministic tests with fakes.
- tests/Tavi.Windows.Tests: adapter tests; interactive opt-in.
- tests/Tavi.TestTarget: small GUI showing PID, identity, arguments, cwd, window info.
- scripts/build.ps1, test.ps1, publish.ps1; .github/workflows/ci.yml.

Core independent; Application -> Core; Windows implements Application ports; App composes DI. UI never directly calls native APIs.

## Typed service contracts

- IVirtualDesktopService: capability snapshot, enumerate/current, create/rename/switch/remove, active/list events, query window desktop, try move/pin.
- IDockHost: display mode, monitor, size, placement, optional work area reservation, status and recovery.
- ILaunchService: validate/build plan, launch, typed result (started/activated/cancelled/denied/unsupported/failed/unverified), nullable PID/native error.
- ICredentialPrompt: ephemeral credential lease; cancellation; zero memory on disposal.
- IWindowTracker: eligible window snapshot, change events, launch correlation, activate, placement capture/restore.
- IConfigurationStore: load/save/backup/import preview/export.
- IIconProvider: native icon extraction, validated bundled Tavi icon catalog, theme-aware Outline/Soft rendering, bounded cancellable cache, generic fallback.
- IStartupRegistrationService: read actual registration state, enable/disable/repair explicit per-user startup shortcut; report OS-policy uncertainty without bypass.
- IDockLayoutService: pure ordered global/workspace entries including non-launchable separators, appearance inheritance, fixed workspace/settings controls and overflow layout.
- IWorkspaceCoordinator: bind/switch/start/cancel and immutable state/status.

Separate active native desktop from workspace selection. Serialize transitions; do not hold locks over IO/shell/UI. Coalesce native callbacks and marshal updates to UI. Do not persist HWND/PID. Single instance per interactive session; second launch activates Settings. Closing Settings leaves dock running. Tray and explicit Exit always available. Structured redacted logs, bounded background work, no constant busy polling.

## Customization contracts

Use discriminated DockEntry (PinEntry or SeparatorEntry) with stable IDs; groups contain launchable pins/groups only. Never route separators through ILaunchService or IWindowTracker. Add DockAppearance and nullable WorkspaceAppearanceOverride, IconSpec (source Native or Tavi, stable iconId, style Outline/Soft, optional palette token), and StartupRegistrationStatus. Keep machine-local sign-in registration outside portable workspace exports. Settings is a separate Window; selecting the gear opens Workspaces for the active binding, preserving uncommitted changes through explicit Save/Cancel. See docs/08-customization.md.
