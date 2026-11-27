# Tavi original icon collection

32 original vector glyphs designed for Tavi's compact floating dock. Each has a stable ID, category, English/German name and 24x24 stroke geometry. The checked-in SVGs are editable source files; catalog.json duplicates their geometry for a typed WinUI renderer. No external icon library or font is required. Use Outline (theme-aware stroke) or Soft (same glyph on a subtle tinted rounded tile); users can also choose native application icons. See [customization specification](../../docs/08-customization.md).

| Category | Icons |
|---|---|
| General | [Application](tavi-outline/application.svg), [Calendar](tavi-outline/calendar.svg), [Clock](tavi-outline/clock.svg), [Search](tavi-outline/search.svg), [Laboratory](tavi-outline/flask.svg), [Chart](tavi-outline/chart.svg), [Tools](tavi-outline/tools.svg), [Settings](tavi-outline/settings.svg), [Power](tavi-outline/power.svg) |
| Files | [Folder](tavi-outline/folder.svg), [Network folder](tavi-outline/network-folder.svg), [Collection](tavi-outline/group.svg), [Document](tavi-outline/document.svg), [Spreadsheet](tavi-outline/spreadsheet.svg), [Archive](tavi-outline/archive.svg), [Link](tavi-outline/link.svg) |
| Development | [Terminal](tavi-outline/terminal.svg), [Code](tavi-outline/code.svg), [Database](tavi-outline/database.svg), [Server](tavi-outline/server.svg), [Network](tavi-outline/network.svg), [Cloud](tavi-outline/cloud.svg), [Source control](tavi-outline/branch.svg) |
| Workspace | [Desktop](tavi-outline/desktop.svg), [Workspaces](tavi-outline/workspaces.svg), [Remote desktop](tavi-outline/remote.svg) |
| Communication | [Web](tavi-outline/globe.svg), [Mail](tavi-outline/mail.svg), [Chat](tavi-outline/chat.svg) |
| Security | [Lock](tavi-outline/lock.svg), [Shield](tavi-outline/shield.svg), [Key](tavi-outline/key.svg) |

These are initial design sources, not evidence of WinUI integration or visual testing. The executing agent must validate geometry and catalog consistency, render at supported sizes and themes, and refine any visual defects while retaining stable IDs. Do not add unreviewed third-party artwork.
