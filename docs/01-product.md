# 01 Product scope

Tavi adds a personal dock to Windows 11; it is not a new shell or independent security session. User can choose between a supplementary dock above the native taskbar or a primary dock floating near the bottom edge when the native taskbar is set to auto-hide. See chapter 04. Default design: compact, centered, never a visible full-width rectangle.

## Workspaces

First launch: usable global dock with Add, workspace selector and Settings. Enumerate native desktops. Explicitly create or bind named workspaces, rename, reorder, switch and edit pins. Removing a workspace does not remove a Windows desktop. Separate confirmation for native removal; warn Windows may move windows. External Task View or Ctrl+Win+arrows refreshes pins automatically. Unbound desktop shows global pins and Bind. Never switch desktops without user intent.

Global pins always visible; workspace pins only for current bound desktop. Within either sequence users can add, drag, reorder and remove real vertical separator entries. Global items precede workspace items in V1; a fixed boundary divider is optional, not a substitute for custom separators. Drag items to reorder or add; copy/move between workspaces and groups. Stable IDs. Item types: EXE local/UNC, local/UNC/mapped folder, file, .lnk/.url, HTTP(S), PS1, RDP and group. Each editable name, icon, path, arguments and working directory where appropriate, launch mode, optional username hint. Show shell icons or selectable Tavi icons (Outline or Soft); choose stable icon ID and optional palette color for each pin, group or workspace. See docs/08-customization.md. UNC access never blocks UI.

Groups are virtual collections, not physical directories. Click icon to toggle compact grid above button. Mixed folders, executables, shortcuts and files; nested groups with breadcrumbs. Click leaf launches only that item and closes flyout; opening group never launches everything. Search, scroll, keyboard, drag/drop and edit. Right click offers valid Open, Run as administrator, Run as another user, Network credentials only, Edit, Copy/Move, Remove. Unsupported modes explicitly unavailable.

## Central Settings and Windows startup

The gear at the far right of every dock is permanent and outside scroll/overflow. Clicking it opens the actual configuration window with sections for Workspaces, Dock, Global pins, Icons and Startup. Workspaces create/rename/reorder/bind/switch native virtual desktops and edit each desktop's own ordered dock with live preview. Unbound desktops still show the gear. Settings also reachable from tray and a second app launch. Appearance inherits global defaults with optional per-workspace overrides.

A separate opt-in Start Tavi with Windows switch registers the portable app at sign-in under the current Windows user, without elevation. Initial default off. It starts the dock silently, not Settings, and does not grant permission to start alternate-identity apps. Per-workspace normal-mode first-activation startup remains a separate opt-in. Imported configurations cannot enable either startup behavior automatically.

## Workspace launch

Explicit Start workspace: activate target desktop, launch opted-in entries sequentially by default, show per-item progress, allow cancellation of pending entries. Optional auto-start once per app session on first activation, off by default, normal mode only. Never start imported items automatically. If user switches away, cancel pending launches; don't switch back. Reuse existing windows only when positively matched on current desktop and policy permits. For ordinary verified EXE windows, restore saved placement; Explorer/shared/elevated/cross-user windows are best effort, clearly report unverified placement. Explorer opens folder; separate tab/window behavior only if demonstrated. Never claim separate Explorer identity.

## V1 scope

Mandatory: functioning native desktops and desktop-dependent dock, floating UI and both display modes on verified builds, mixed group flyout, edit/reorder, arbitrary vertical separators, rightmost Settings configuration, selectable bundled icon pack, opt-in Windows sign-in startup, local and UNC launch and tested identity modes, startup and tracking, persistence, import/export, accessibility, safe recovery and self-contained x64 publish. Primary mode offers current-desktop running windows plus pins, workspace switcher and settings; native Start/system tray remain native.

Deferred: replacing Explorer, per-desktop native taskbar pins, arbitrary Explorer impersonation, password vault, remote sync, ARM64, independent bars per monitor, full system tray replica. No paid dependency or cloud service.
