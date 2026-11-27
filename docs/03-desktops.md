# 03 Native virtual desktops

Use documented IVirtualDesktopManager for window desktop queries and permitted moves. It lacks complete enumeration/create/rename/switch/event APIs. Evaluate maintained compatible adapter (candidate https://github.com/Grabacr07/VirtualDesktop); inspect source/license and test actual Windows builds before pinning. Internal COM is version-sensitive: keep behind IVirtualDesktopService, capability checks and safe failure. No guessing GUID/vtable offsets.

S01 spike must demonstrate enumerate/current, user-requested create/rename/switch/remove, external Task View notifications, persistent dock visibility on all native desktops and window association. Record exact OS build and versions. Test Explorer restart, sleep/resume, shell disconnection, logoff. Use STA when required; dispose subscriptions. If notification unavailable, bounded low-frequency polling only with validated adapter. If incompatible, global dock still functions, disable native controls and explain; do not simulate support. Completion requires real Windows verification.

Bind workspace ID to native desktop GUID locally. Reconcile on startup/list change; never infer by index/name. Missing GUID becomes orphaned binding with rebind/create. Export bindings removed by default. Desktop changes update visible pins/running list atomically, close old group flyout, cancel pending launches. Never move arbitrary windows or force focus.

Launch after target desktop becomes active. Track exact PID/start time, verified process lineage and eligible top-level HWND. Only move positively matched windows with appropriate permission; shared/elevated/cross-user apps may resist. Timeout and report unverified placement, never guess from window title alone. Prefer new window instead of reusing another desktop's instance. Native desktops do not isolate data, tokens or network credentials.

Reference: https://learn.microsoft.com/en-us/windows/win32/api/shobjidl_core/nn-shobjidl_core-ivirtualdesktopmanager
