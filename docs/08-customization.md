# 08 — Dock customization, Settings, startup and icon system

Mandatory V1 requirements. Extends chapters 01–07 and the S01–S08 execution plan.

## 1. User-defined vertical separators

- Add Separator from the dock context menu at the requested insertion point and from Settings > Workspaces > selected desktop > Dock layout / Global pins.
- Persist separators as ordered DockEntry records with GUID, kind=separator, optional paddingDip (4–12, default 6). They are not links, applications, groups or physical folders. No target, icon, credentials, running state or auto-start.
- Appearance: 1 DIP vertical stroke, 28 DIP tall, theme-aware contrast, centered in dock cell; no visual button tile, hover activation or focus in normal mode. Edit mode shows a draggable handle and accessible label "Separator"; keyboard Move left/right, Remove. Multiple separators allowed and exact order survives reload, workspace switch and portable export/import.
- Global sequence always precedes current workspace sequence in V1. Users can insert separators at any position in either sequence, including edges, and optionally enable a separate automatic global boundary (off by default). Running-window boundary independent. No separators inside group flyout in V1. Reorder and copy/move across permitted dock lists; copy assigns new GUID. Never silently remove consecutive separators.
- Include separator width in content sizing and overflow. Never show a clickable separator in the overflow menu. Preserve stored order regardless of compact display. Fixed Settings remains available with all lists empty or overflowing.

## 2. Fixed Settings entry and configuration

Every dock, including unbound/fallback global dock and both positioning modes, has a permanent gear at the far right. Not a configurable pin: cannot hide, remove, reorder or overflow it. Workspace selector at left; pin/running region between; overflow immediately before gear. Gear opens/activates one ordinary WinUI Settings window; do not launch duplicate windows. Tray and second app launch remain recovery routes.

Suggested Settings NavigationView:
- Workspaces: list native desktops and bindings, create/rename/reorder workspace, create/switch/bind/rebind native desktop, optional confirmed native deletion. Show active desktop and orphan/unbound state. Native ordering only if adapter supports it; otherwise workspace ordering only, clearly labeled. Select a workspace without switching the OS desktop. Preview and edit that workspace's ordered dock (including separators and groups), choose workspace icon, startup policy and appearance overrides. Save/Cancel; switch editing selection with unsaved changes prompts. Global settings changes redraw current dock after save. Native actions such as create/switch are explicit immediate actions, not falsely presented as reversible by Cancel.
- Global pins: same ordered editor for items on every desktop, separators, add/move/copy/edit/delete, preview.
- Appearance: mode, bottom gap, icon size, theme, icon style, optional automatic boundary, optional proven reservation. Per-workspace overrides for icon size, bottom gap, icon style, theme, boundary and accent; inherit/reset independently. Keep primary/supplementary mode and monitor selection global in V1 to avoid native taskbar geometry changes on every switch. Use existing geometry limits and accessibility settings.
- Icons: browse complete Tavi pack with search/category, live preview on light/dark and native/Outline/Soft choices. Contextual picker opens from a pin/group/workspace editor.
- Startup: Start Tavi with Windows, status/repair, separate explanation and links to workspace first-activation settings. Also show OS startup management link.
- About/Diagnostics: version, compatibility, native fallback and redacted diagnostics.

Settings changes must persist atomically; previews never execute items. No hidden settings switch that alters OS behavior without explicit action. Use English/German resources and accessible controls.

## 3. Windows sign-in startup

This is distinct from optional workspace application startup. Default disabled, toggle explicitly in Settings, no admin elevation. For unpackaged portable V1 implement IStartupRegistrationService with an owned shortcut in current user's Environment.SpecialFolder.Startup. Use documented IShellLink/IPersistFile (or verified equivalent). Name Tavi.lnk; absolute installed Tavi.exe target, correct working directory, --autostart argument. Do not target a network executable, script shell, or elevated process. Only edit/remove a verified Tavi-owned shortcut; if a conflicting unrelated file exists, report and ask user to resolve it. Atomic create/replace where feasible. No HKLM, task scheduler, services, StartupApproved registry modifications or bypass of OS startup policies. Detect missing/moved executable path and offer explicit Repair; do not automatically change registration when moving/importing config or re-enabling externally disabled apps.

Read actual shortcut status (not just settings JSON): absent, registered-valid, invalid/repairable, conflict, denied/error; OS-level enabled/disabled or policy status may be unknown via documented APIs, distinguish it from shortcut existence. Offer Windows Startup Apps settings to manage OS state. Never report a verified startup without actual sign-in evidence. On --autostart start one unelevated dock quietly, no Settings window, no UAC/credential prompts. A second autostart invocation must not activate Settings; ordinary second manual launch does. Wait asynchronously for shell readiness with bounded retries/fallback, remain responsive. User Exit stops current instance; explicit disable removes registration. Respect Windows startup policies, do not self-recreate deleted/disabled registration. Import/export excludes registration, no auto-start from imported items.

Workspace first-activation automation remains opt-in normal mode only, as in chapter 01. It may run after Tavi sign-in startup only after actual desktop binding is resolved and user previously enabled workspace startup. Cancel pending launches on desktop switch/exit; never require alternative credentials unattended.

## 4. Original selectable icon pack

Use assets/icons/tavi-outline/*.svg and assets/icons/catalog.json as V1's bundled original source assets. All icons use 24x24 viewBox, 1.65 unit rounded strokes, no embedded text/fonts/scripts/external resources. Catalog stable kebab-case IDs, categories and English/German labels; don't rename IDs after release. Implement searchable grid (name/category), previews at 24/36/48 DIP and selected check. Native app/file icon remains available and default for executable/file targets; use Tavi folder/group defaults where appropriate.

Styles:
- Native: shell/application icon; fallback generic Tavi glyph when unavailable.
- Outline: original monochrome geometry, current theme foreground, no heavy tile.
- Soft: same original glyph over a subtle rounded tinted square, theme-aware foreground contrast and optional user-selectable palette token (neutral, blue, teal, green, amber, rose, violet). No requirement to draw a new glyph for each style.
- Per-entry/group/workspace IconSpec: source=native or tavi, iconId, optional style (inherits effective dock iconStyle if null), optional color token. For global item appearances, effective current desktop theme/style applies unless explicit per-item override. Settings gear and workspace selector system glyphs remain accessible and recognizable regardless of custom pins.

Implementation: compile/package the catalog and SVG files as app resources, never fetch remotely. Manifest includes path geometry per glyph so WinUI can render PathIcon/Path with bound theme Stroke/Fill rather than relying on unsupported SVG styling. Use 24x24 geometry and uniform scale, StrokeThickness=1.65, round joins/caps, with explicit padding. If PathIcon cannot represent stroke, use Path inside Viewbox with appropriate Stroke properties. Render Native via bounded async icon provider. Cache by icon source/id/style/theme/color/scale and invalidate on theme changes. High contrast overrides tint with system brush; no accessibility information only conveyed by color. Unknown ID falls back safely, no arbitrary SVG import/rendering from untrusted config. User may select any catalog ID for any valid pin/group/workspace, see preview, reset to default; choice persisted and portable. Icon sources are included in release output or compiled resources. No external icon font or paid dependency.

Validate catalog JSON, unique IDs, every referenced SVG exists and matches geometry, no external URI/scripts, every glyph has nonempty bounded geometry. Test WinUI rendering on real Windows, screenshots at light/dark/high contrast, labels and keyboard navigation. Do not call the pack integrated merely because SVG sources exist.

## 5. Acceptance

C01–C04 in chapter 07 are mandatory before V1 release. Record actual Windows startup test and icon render evidence. If a native OS limitation prevents a feature, preserve safe fallback, document it and leave relevant gate blocked. Existing S01–S08 order remains; no new phase required.
