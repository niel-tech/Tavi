# Tavi

**Your desktop. Your workspace.**

Tavi is a native Windows 11 workspace manager. V1 is currently a specification, not an implemented application.

## V1 features

- A freestanding macOS-inspired dock: horizontally centered, rounded, content-sized, floating above the bottom screen edge, with a visible gap around it.
- Two dock modes: supplementary (above visible Windows taskbar) and primary (near the bottom screen edge while Windows taskbar is set to auto-hide). Windows shell remains available.
- Native virtual desktops, named workspaces, global pins and per-desktop pins. Automatically update the dock on desktop changes.
- Clicking a group opens a grid of mixed programs, folders, UNC paths, files and shortcuts immediately above its dock icon.
- Drag-and-drop, nesting, reorder, search and accessible keyboard navigation.
- User-inserted vertical separators anywhere within the global or workspace pin sequence; separate configuration per virtual desktop.
- Always-visible Settings button at the far right: manage native desktops, their individual docks, global pins, appearance, icon selection and startup.
- Original Tavi icon collection with native, Outline and Soft visual options; choose an icon per pin, group or workspace.
- Opt-in Tavi autostart at Windows sign-in, independent of workspace application startup.
- Local/UNC application launch, UAC elevation, alternate Windows user, network-only credentials where supported.
- Workspace startup, window tracking, running indicators, optional window placement restoration.
- Local JSON, secret-free import/export, portable self-contained x64 release.

## Documentation

| Chapter | Content |
|---|---|
| [01 Product](docs/01-product.md) | Scope and user journeys |
| [02 Architecture](docs/02-architecture.md) | Solution and service contracts |
| [03 Native desktops](docs/03-desktops.md) | Integration, events, compatibility |
| [04 Floating dock](docs/04-dock.md) | Visual design, placement, groups |
| [05 Launching](docs/05-launch.md) | UNC, identity, UAC, windows |
| [06 Persistence](docs/06-persistence.md) | Schema, import and security |
| [07 Verification](docs/07-verification.md) | Tests, CI, build and publishing |
| [08 Customization](docs/08-customization.md) | Separators, Settings, Windows autostart and selectable icons |

Original vector icon sources and stable catalog: [assets/icons](assets/icons/README.md).

## Implement V1

Read [AGENTS.md](AGENTS.md) and [dev/v1/README.md](dev/v1/README.md). Follow the ordered steps. Pass [START-PROMPT.md](dev/v1/START-PROMPT.md) to an executing coding agent and maintain [PROGRESS.md](dev/v1/PROGRESS.md).

C# / .NET 10 LTS / WinUI 3 / stable Windows App SDK, Windows 11 x64. Verify and pin the actual compatible SDK versions. This public repository must never contain credentials or private configuration.
