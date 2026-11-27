# 05 — Launching, UNC, user identities and window tracking

Build typed LaunchPlan from kind and requested mode. Use absolute paths, retain UNC and Unicode, reject relative/device paths, explicit argument list and validated cwd. Never concatenate arbitrary user input into cmd.exe or PowerShell -Command. Native command-line encoder tested for spaces, quotes, trailing backslashes, empty args and Unicode. Explicit executable path. Shell association route distinct from direct process launch.

| Item | Normal | Elevated | Alternate identity/network only |
|---|---|---|---|
| Local/UNC EXE | ProcessStartInfo / ShellExecuteEx | ShellExecuteEx runas with UAC | CreateProcessWithLogonW or verified supported broker |
| Folder/file/URL/RDP | ShellExecuteEx open | only verified explicit executable | unavailable for association/Explorer; offer explicit supported EXE |
| .lnk | shell open | resolved verified EXE | inspect resolved target/args/cwd; reject unsupported |
| .ps1 | trusted local PowerShell host -File | UAC on host, confirmation | same trusted local host with alternate identity |
| Group | toggle popup | not applicable | not applicable |

Allow http/https URLs only; inspect .url/.lnk and display target. Do not bypass Windows execution policies or MOTW. Run Tavi as standard user; UAC per launch. Never claim combined elevated+alternate identity; unsupported V1. Shell associations and Explorer may reuse current-user instance; do not label them as switched user. No fake success if unsupported.

## UNC and credentials

No UI-thread network call; bounded async path probes/icon reads. A probe under caller identity cannot reject an alternate-user launch because target identity may have access. Use UNC not mapped drive when alternate session; default cwd chosen explicitly from valid local/target path per mode. Verify both normal and alternate user UNC execution. Distinguish missing path, access denied, cancel, 740 (elevation required), 1219 (SMB credential conflict), unavailable Secondary Logon, invalid credentials, policy denial and timeout. Never silently disconnect existing shares.

Use CredUIPromptForWindowsCredentialsW or verified Windows credential UI without save; support DOMAIN\\user/UPN, ephemeral native buffers; cancel distinguished, clear buffers and dispose handles. Username hint optional, password never stored, passed in CLI, logged, exported or cached. CreateProcessWithLogonW LOGON_WITH_PROFILE for full alternate identity; LOGON_NETCREDENTIALS_ONLY for network credentials only (local token remains caller; credentials validated only at remote use). A returned PID is process creation, not proof of successful network auth. Verify actual identity via test target. Direct UNC executable access may depend on caller/target token and Windows launch API behavior: S01 tests accessible only to alternate user. If direct route fails, evaluate trusted local Tavi launch helper launched under target credentials, then start UNC executable from that process; helper accepts only typed executable path/args/cwd, no passwords, reports child PID/errors through authenticated local IPC with restrictive ACL and correlation, no arbitrary command shell. Do not copy remote EXE or weaken ACLs to make it work. If no safe tested route, explicit unsupported/blocker. Secondary Logon and interactive desktop permissions are prerequisites, never broaden ACLs automatically. No RunAs password-saving option. Auto-start only normal mode.

## Windows and launch lifecycle

Enumerate top-level windows, filter invisible/cloaked/tool/owned/system/Tavi windows using documented APIs; subscribe WinEvent where suitable with coalescing. Track process PID plus start time, verified lineage and desktop GUID. PID reuse, access denied, singleton reuse, Explorer tabs and elevated apps treated as expected limitations. Match only positive evidence. New window on active desktop, move only matched window where allowed; bounded timeout and unverified status. No arbitrary app termination or foreground forcing. Reuse only on active target desktop and if policy permits, never another user's window. Capture/restore monitor-aware window placement, clamp to work area, preserve normal/maximized state; restore only explicitly configured or positively matched. Return structured result with user-friendly message/native error, redacted diagnostics; distinguish launch succeeded vs window placement not verified.

References:
https://learn.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-createprocesswithlogonw
https://learn.microsoft.com/en-us/windows/win32/api/wincred/nf-wincred-creduipromptforwindowscredentialsw
https://learn.microsoft.com/en-us/windows/win32/api/shellapi/nf-shellapi-shellexecuteexw
