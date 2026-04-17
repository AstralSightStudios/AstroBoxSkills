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
npx astrobox-cli provider categories OfficialV2       # pick category
npx astrobox-cli provider page OfficialV2 \
  --category watchface --sort time --limit 10         # browse
npx astrobox-cli provider item OfficialV2 <id>        # inspect details
npx astrobox-cli provider download OfficialV2 \
  --id <id> --device xmb9p                           # get download URL
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
