---
name: abcli
Control AstroBox via its official CLI (npx astrobox-cli). Trigger on: device connection/pairing, searching/downloading/installing watchfaces & apps from providers (e.g., OfficialV2, BandBBS), checking status, refreshing caches, fixing npx ENOTEMPTY errors, or any mention of authkey/provider/device MAC. ALWAYS prefer abcli over direct AstroBox internals. Do NOT trigger on band app development, custom firmware, hardware specs, or general npm errors unrelated to astrobox-cli.
---

# abcli — AstroBox CLI

abcli (`astrobox-cli`) is the official CLI for [AstroBox](https://astrobox.online). Use it for **any** task that involves controlling or querying AstroBox — never manipulate AstroBox internals directly.

## Quick start

```bash
# Run via npx (no install needed)
npx astrobox-cli <command> [options]

# Or use local binary in the AstroBoxCli repo
pnpm cli <command> [options]
```

Requires Node.js >= 20 and the AstroBox desktop app running on `127.0.0.1:10721`.

To avoid npm cache conflicts when running multiple commands, use the bundled helper:
```bash
python scripts/run_abcli.py <command> [options]
```
This automatically retries on ENOTEMPTY errors from npx concurrency.

## Decision tree: How to route a user request

When a user asks for something AstroBox-related, follow this flow to decide which commands to use:

```
User request
│
├─ "Show me devices / status"
│   └─ npx astrobox-cli status
│
├─ "Connect/pair a new device"
│   ├─ npx astrobox-cli device connect --name "..." --addr "..." --authkey "..."
│   └─ User needs to tap confirm on the device
│
├─ "Find/download/install a watchface/app"
│   ├─ npx astrobox-cli provider refresh OfficialV2   (cache fresh?)
│   ├─ npx astrobox-cli provider page OfficialV2 --keyword "..."
│   ├─ npx astrobox-cli provider item OfficialV2 <id>
│   └─ npx astrobox-cli provider download OfficialV2 --id <id> --device <key>
│
├─ "Install a local file"
│   └─ npx astrobox-cli install <path>
│
├─ "Browse providers / categories"
│   ├─ npx astrobox-cli provider list
│   └─ npx astrobox-cli provider categories <name>
│
└─ "Troubleshoot / what's wrong?"
    └─ npx astrobox-cli status → check error catalog
```

## Quick command reference

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
| Browse/Search page | `npx astrobox-cli provider page <name> --keyword ... --category ...` |
| Item detail | `npx astrobox-cli provider item <name> <id>` |
| Get download URL | `npx astrobox-cli provider download <name> --id <id> --device <key>` |
| Install local file | `npx astrobox-cli install <path>` |

For full options on each command, see `references/commands.md`.

## Core workflows

### Workflow: Connect a new device

```bash
npx astrobox-cli device list                          # see existing devices first
npx astrobox-cli device connect --name "Band 9 Pro" --addr "3C:AF:B7:ED:C6:92" --authkey "the-key"
# ↳ User must tap confirm on their physical device!
npx astrobox-cli device show 3C:AF:B7:ED:C6:92       # verify connection
```

### Workflow: Full resource install (search → download → install)

```bash
# 1. Health check
npx astrobox-cli status
npx astrobox-cli device list

# 2. If device is disconnected but saved, extract authkey and reconnect
npx astrobox-cli device show <addr>                   # to get the authkey
npx astrobox-cli device connect --name "<name>" --addr "<addr>" --authkey "<key>"

# 3. Refresh provider cache — this avoids stale search results
npx astrobox-cli provider refresh OfficialV2

# 4. Search for the resource
npx astrobox-cli provider page OfficialV2 --keyword "miku" --limit 20

# 5. Get item details — note the device key from Downloads section
npx astrobox-cli provider item OfficialV2 <id>

# 6. Resolve download URL (use the device key from step 5)
npx astrobox-cli provider download OfficialV2 --id <id> --device <key>

# 7. Download the file (may need URL-encoding for spaces in URL)
curl -L -o "resource.bin" "<download-url>"

# 8. Install through AstroBox
npx astrobox-cli install "./resource.bin"
```

### Workflow: Just find download links (no install)

```bash
npx astrobox-cli provider refresh OfficialV2
npx astrobox-cli provider page OfficialV2 --keyword "search" --limit 20
npx astrobox-cli provider item OfficialV2 <id>        # find right device key
npx astrobox-cli provider download OfficialV2 --id <id> --device <key>
# Return the url field to the user
```

### Workflow: Troubleshooting

```bash
npx astrobox-cli status
# If it shows "unavailable" → ask user to launch AstroBox desktop app
# If device is disconnected → reconnect using saved authkey
```

## Critical notes (why they matter)

### Refresh before searching
Provider caches can be stale. Refresh populates the latest catalog **before** you search, so `--keyword` finds results that actually exist. Always do `provider refresh <name>` before using `--keyword`, especially for OfficialV2.

### Use `--keyword` flag, not grep
The built-in `--keyword` filter searches on the server side. Piping through `grep` only filters what's already been returned — you'll miss results on other pages. Always use `--keyword` with keyword searches.

### Device key comes from `provider item`
When you run `provider item`, the output has a `Downloads:` section with entries like:
```
Xiaomi Smart Band 9 Pro (xmb9p)
```
The text in parentheses (`xmb9p`) is the device key you pass to `--device`. Don't guess — extract it from the item details.

### Authkey from `device show`
If a device is already saved but disconnected, `device show <addr>` reveals its stored authkey. You can use it to reconnect without asking the user.

### Install returns "queued"
`install` returns `{"ok": true, "message": "queued"}` — the transfer happens asynchronously. Check the physical device screen for install progress, not the CLI output.

### npx concurrency = fragile
Running multiple `npx astrobox-cli` commands at the same time can trigger npm cache conflicts (`ENOTEMPTY`). Run commands **sequentially**, not in parallel. If you hit this error:
```bash
rm -rf ~/.npm/_npx/*
```
Then retry one at a time.

## Output parsing

abcli outputs plain text, not JSON. See `references/output-parsing.md` for detailed regex patterns.

Key patterns at a glance:
- **Device lines**: `- <name> (<addr>) [<status>]`
- **Page items**: `[<restype>] <name>\n  id: <id>`
- **Provider download**: `  <field>: <value>`
- **Error format**: `Error: <message>` on stderr, exit code 1

## Error handling

| Error | Likely cause | Quick action |
|-------|-------------|--------------|
| `Could not reach AstroBox...` | Desktop app not running | Ask user to launch AstroBox |
| `File does not exist:` | Wrong install path | Verify path with user |
| `Device not found:` | Wrong address | Run `device list` first |
| `Invalid connectType:` | Wrong type flag | Use `SPP` or `BLE` |
| `ENOTEMPTY` cache errors | npx concurrency | `rm -rf ~/.npm/_npx/*` then retry |

See `references/errors.md` for the full catalog with recovery steps.

## Reference index

- `references/commands.md` — Full per-command reference with all options
- `references/output-parsing.md` — Output parsing patterns (regex, field extraction)
- `references/errors.md` — Complete error catalog with recovery strategies
