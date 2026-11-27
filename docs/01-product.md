# 01 Product scope

Tavi adds a personal dock to Windows 11; it is not a new shell or independent security session. User can choose between a supplementary dock above the native taskbar or a primary dock floating near the bottom edge when the native taskbar is set to auto-hide. See chapter 04. Default design: compact, centered, never a visible full-width rectangle.

## Workspaces

First launch: usable global dock with Add, workspace selector and Settings. Enumerate native desktops. Explicitly create or bind named workspaces, rename, reorder, switch and edit pins. Removing a workspace does not remove a Windows desktop. Separate confirmation for native removal; warn Windows may move windows. External Task View or Ctrl+Win+arrows refreshes pins automatically. Unbound desktop shows global pins and Bind. Never switch desktops without user intent.

Global pins always visible; workspace pins only for current bound desktop. Drag items to reorder or add; copy/move between workspaces and groups. Stable IDs. Item types: EXE local/UNC, local/UNC/mapped folder, file, .lnk/.url, HTTP(S), PS1, RDP and group. Each editable name, icon, path, arguments and working directory where appropriate, launch mode, optional username hint. Show shell icons or fallback. UNC access never blocks UI.

Groups are virtual collections, not physical directories. Click icon to toggle compact grid above button. Mixed folders, executables, shortcuts and files; nested groups with breadcrumbs. Click leaf launches only that item and closes flyout; opening group never launches everything. Search, scroll, keyboard, drag/drop and edit. Right click offers valid Open, Run as administrator, Run as another user, Network credentials only, Edit, Copy/Move, Remove. Unsupported modes explicitly unavailable.

## Workspace launch

Explicit Start workspace: activate target desktop, launch opted-in entries sequentially by default, show per-item progress, allow cancellation of pending entries. Optional auto-start once per app session on first activation, off by default, normal mode only. Never start imported items automatically. If user switches away, cancel pending launches; don't switch back. Reuse existing windows only when positively matched on current desktop and policy permits. For ordinary verified EXE windows, restore saved placement; Explorer/shared/elevated/cross-user windows are best effort, clearly report unverified placement. Explorer opens folder; separate tab/window behavior only if demonstrated. Never claim separate Explorer identity.

## V1 scope

Mandatory: functioning native desktops and desktop-dependent dock, floating UI and both display modes on verified builds, mixed group flyout, edit/reorder, local and UNC launch and tested identity modes, startup and tracking, persistence, import/export, accessibility, safe recovery and self-contained x64 publish. Primary mode offers current-desktop running windows plus pins, workspace switcher and settings; native Start/system tray remain native.

Deferred: replacing Explorer, per-desktop native taskbar pins, arbitrary Explorer impersonation, password vault, remote sync, ARM64, independent bars per monitor, full system tray replica. No paid dependency or cloud service.
