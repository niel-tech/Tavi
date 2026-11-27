# 06 — Local configuration

Store per-user %LOCALAPPDATA%\\Tavi\\settings.json. SchemaVersion 1, UTF-8, stable GUIDs, deterministic order. Atomic temp file + flush + replace within same directory; retain last known good backup. Validate before replacing; corrupt primary prompts recovery from backup or safe empty config without destructive overwrite. Single-instance writer. No HWND/PID, secrets, tokens or passwords. Redact usernames and private paths from exportable diagnostic bundles.

Illustrative JSON (IDs shown as actual GUIDs):
~~~json
{
  "schemaVersion": 1,
  "dock": {
    "mode": "supplementary",
    "placement": "bottomCenter",
    "reserveSpace": false,
    "iconSizeDip": 36,
    "bottomGapDip": 10,
    "theme": "system"
  },
  "globalPins": [],
  "workspaces": [
    {
      "id": "a563b2d5-7f6b-45b8-889a-11459bec9099",
      "name": "Testing",
      "nativeDesktopId": null,
      "autoStartOnFirstActivation": false,
      "pins": [
        {
          "id": "05769cb3-e550-416b-9a2d-0881c86f8177",
          "kind": "group",
          "name": "Tools",
          "children": [
            {
              "id": "059a8e0b-0f89-4009-bccd-a66827153b04",
              "kind": "executable",
              "name": "Test app",
              "target": "\\\\server\\share\\Test.exe",
              "arguments": [],
              "workingDirectory": null,
              "launchMode": "otherUser",
              "usernameHint": "EXAMPLE\\tester",
              "autoStart": false,
              "reusePolicy": "newInstance"
            }
          ]
        }
      ]
    }
  ]
}
~~~

Leaf optional icon reference (safe local/default), placement (monitor, logical bounds, show state), autoStart and reuse. Groups have children only; no implicit execution or startup flag. Validate enum values, unique IDs, depth <= 8, total entries <= 2000, file <= 4 MiB, bounded strings/args, kind/mode combinations, no cycles. Reject unknown schema versions with recovery instruction; migrate explicitly in later versions. Pin order global then workspace, separator, running windows. Move preserves IDs; copy recursively regenerates IDs.

Export machine-portable JSON strips desktop GUID bindings by default, no credentials; explicitly review username hints and local paths before export. Import preview validates all entries, shows conflicts and unsupported targets; choose merge (new IDs) or replace with backup, confirm. Imported executable/scripts/shortcuts disabled until reviewed; auto-start cleared, no automatic network probing or launching. Bind desktops explicitly after import. Add JSON schema and synthetic example during S02; use tests roundtripping Unicode/UNC, corruption, interrupted write, conflict, import and backup. Keep data local; no analytics/cloud.
