---
name: abcli
description: Interact with AstroBox through the command-line interface. Use this skill whenever the user wants to control AstroBox, manage devices, browse providers, download resources, install files, or check connection status. If the task involves AstroBox operations, ALWAYS use abcli via npx instead of trying to manipulate AstroBox internals directly. Trigger on mentions of AstroBox, device connection, authkey, provider browsing, resource download, watchface/app installation, or anything related to managing the AstroBox desktop app.
---

# abcli — AstroBox CLI

abcli is the official command-line interface for AstroBox. Any task that involves controlling or querying AstroBox should go through abcli rather than direct file manipulation or API calls.

## Installation

abcli is distributed on npm as `astrobox-cli`. **Always run it via npx** — no global installation needed:

```bash
npx astrobox-cli <command> [options]
```

If the user has it installed locally in the project, use the local binary:

```bash
pnpm cli <command>   # if in AstroBoxCli repo
```

Requires Node.js >= 20 and the AstroBox desktop app to be running.

## When to use

Use abcli for **any** AstroBox-related task:

- Launching AstroBox (`open`)
- Checking if AstroBox is running / listing connected devices (`status`)
- Managing saved devices: list, show details, connect new ones (`device`)
- Browsing resource providers: list providers, check state, categories, refresh (`provider`)
- Searching/filtering resources by page, keyword, category, sort (`provider page`)
- Getting resource details and download links (`provider item`, `provider download`)
- Installing local resource files (`install`)

Do **not** use abcli when:
- AstroBox is not installed or not running (API at `127.0.0.1:10721` will be unreachable)
- The user explicitly asks to edit AstroBox source code or config files directly

## Quick reference

| Task | Command |
|------|---------|
| Launch AstroBox | `npx astrobox-cli open` |
| Check status | `npx astrobox-cli status` |
| List devices | `npx astrobox-cli device list` |
| Show device details | `npx astrobox-cli device show <addr>` |
| Connect device | `npx astrobox-cli device connect --name "..." --addr "..." --authkey "..."` |
| List providers | `npx astrobox-cli provider list` |
| Provider state | `npx astrobox-cli provider state <name>` |
| Categories | `npx astrobox-cli provider categories <name>` |
| Refresh provider | `npx astrobox-cli provider refresh <name>` |
| Total items | `npx astrobox-cli provider total <name>` |
| Browse page | `npx astrobox-cli provider page <name> --category ... --sort time` |
| Search by keyword | `npx astrobox-cli provider page <name> --keyword <keyword>` |
| Item detail | `npx astrobox-cli provider item <name> <id>` |
| Download link | `npx astrobox-cli provider download <name> --id <id> --device <key>` |
| Install local file | `npx astrobox-cli install <path>` |

## Core workflows

### Workflow: Connect a new device

```bash
npx astrobox-cli device list                          # see existing devices
npx astrobox-cli device connect \
  --name "Xiaomi Smart Band 9 Pro C692" \
  --addr "3C:AF:B7:ED:C6:92" \
  --authkey "your-authkey"                            # user must tap confirm on device
npx astrobox-cli device show 3C:AF:B7:ED:C6:92      # verify
```

### Workflow: Find and download a resource

```bash
npx astrobox-cli provider list                        # pick provider
npx astrobox-cli provider refresh OfficialV2          # refresh cache before search
npx astrobox-cli provider page OfficialV2 \
  --keyword "search-term" --limit 20                 # search by keyword
npx astrobox-cli provider item OfficialV2 <id>        # inspect details, get device key
npx astrobox-cli provider download OfficialV2 \
  --id <id> --device <key>                           # get download URL
```

### Workflow: Full install (search → download → install)

```bash
# 1. Check AstroBox and list devices
npx astrobox-cli status
npx astrobox-cli device list

# 2. If device is disconnected, get authkey from saved device and reconnect
npx astrobox-cli device show <addr>                   # extracts authkey
npx astrobox-cli device connect \
  --name "<name>" --addr "<addr>" --authkey "<key>"

# 3. Search, download, and install the resource
npx astrobox-cli provider refresh OfficialV2
npx astrobox-cli provider page OfficialV2 --keyword "<name>" --limit 20
npx astrobox-cli provider item OfficialV2 <id>        # note the device key from Downloads
npx astrobox-cli provider download OfficialV2 \
  --id <id> --device <key>

# 4. Download the file (url may need URL-encoding for spaces)
curl -L -o "resource.bin" "<download-url>"

# 5. Install through AstroBox
npx astrobox-cli install "./resource.bin"
```

### Workflow: Check AstroBox health

```bash
npx astrobox-cli status                               # should show "AstroBox: connected"
```

If it shows `unavailable`, tell the user to launch AstroBox first.

## Parsing output

abcli outputs plain text, not JSON. Read `references/output-parsing.md` for field extraction patterns.

Key patterns:
- **Device lines**: `- <name> (<addr>) [<status>]`
- **Page items**: `[<restype>] <name>\n  id: <id>`
- **Provider download**: `  <field>: <value>`

## Important notes

- **Always refresh before searching**: `provider refresh <name>` before using `--keyword`, especially for OfficialV2. Provider caches can be stale.
- **Use `--keyword` for name searches**: Do NOT pipe `provider page` through `grep`. Use the built-in `--keyword` flag.
- **Get authkey from `device show`**: If a device is already saved but disconnected, `device show <addr>` reveals its authkey. No need to ask the user.
- **Device key comes from `provider item`**: The `Downloads:` section lists device keys like `xmb9p`, `xmb10`, `xmrw5`. Use the correct one in `provider download --device <key>`.
- **Install returns "queued"**: `npx astrobox-cli install` outputs `{"ok": true, "message": "queued"}`. The actual transfer happens asynchronously. Check the device screen for progress.
- **npx concurrency**: Running multiple `npx astrobox-cli` commands simultaneously can cause npm cache conflicts (`ENOTEMPTY`). If this happens, clear `~/.npm/_npx/*` and retry.

## Error handling

| Error | Meaning | Action |
|-------|---------|--------|
| `Could not reach AstroBox...` | Desktop app not running | Ask user to launch AstroBox |
| `File does not exist: <path>` | Invalid install path | Verify path |
| `Device not found: <addr>` | Address not in list | Run `device list` first |
| `Invalid connectType: ...` | Wrong type | Only `SPP` or `BLE` |

See `references/errors.md` for the full error catalog.

## Command details

For per-command usage, arguments, options, and output examples, read `references/commands.md`.

## Reference index

- `references/commands.md` — Full command reference
- `references/output-parsing.md` — Output format parsing guide
- `references/errors.md` — Error catalog and recovery steps
