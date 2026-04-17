# abcli Command Reference

Complete reference for every abcli command. All examples use `npx astrobox-cli`.

---

## `open`

Launch AstroBox via the `astrobox://` protocol URL.

```bash
npx astrobox-cli open
npx astrobox-cli open --url astrobox://workspace
```

**Options:**
- `--url <url>` — Custom protocol URL (default: `astrobox://`)

**Output:**
```
Opened astrobox://
```

---

## `status`

Query AstroBox connection status and list connected devices.

```bash
npx astrobox-cli status
```

**Output format:**
```
AstroBox: <connected|unavailable>
Devices: <count>
- <name> (<addr>) [<connected|disconnected>]
```

**Example:**
```
AstroBox: connected
Devices: 2
- Xiaomi Smart Band 9 Pro C692 (3C:AF:B7:ED:C6:92) [connected]
- Galaxy S23 (A1:B2:C3:D4:E5:F6) [disconnected]
```

---

## `install`

Install a local resource file through AstroBox.

```bash
npx astrobox-cli install ./app.rpk
npx astrobox-cli install /absolute/path/to/file.bin
```

**Arguments:**
- `<path>` — Path to local file, resolved from current working directory

**Output:** JSON response indicating the install has been queued.

```json
{
  "ok": true,
  "message": "queued"
}
```

The actual file transfer happens asynchronously. Check the physical device screen for progress indicators.

---

## `device list`

List all saved devices and their connection status.

```bash
npx astrobox-cli device list
```

**Output format:**
```
Devices: <count>
- <name> (<addr>) [<status>]
```

---

## `device show`

Show full details for a device by MAC address.

```bash
npx astrobox-cli device show 3C:AF:B7:ED:C6:92
```

**Arguments:**
- `<addr>` — Device MAC address

**Output format:**
```
Name:     <name>
Address:  <addr>
AuthKey:  <authkey>
Status:   <connected|disconnected>
SAR Ver:  <sarVersion>
TX Win:   <txWinOverrunAllowance>
Type:     <connectType>
```

---

## `device connect`

Add and connect a new device. The user must tap confirm on their physical device.

```bash
npx astrobox-cli device connect \
  --name "Xiaomi Smart Band 9 Pro C692" \
  --addr "3C:AF:B7:ED:C6:92" \
  --authkey "your-authkey"
```

**Required options:**
- `--name <name>` — Device name
- `--addr <addr>` — Device MAC address
- `--authkey <authkey>` — Device auth key

**Optional options:**
- `--sarVersion <version>` — SAR version (default: `2`)
- `--txWinOverrunAllowance <allowance>` — TX window overrun allowance
- `--connectType <type>` — Connection type: `SPP` or `BLE` (default: `SPP`)

**Output:**
```
Connecting...
Connected to <name> (<addr>)
```

**Note:** The success message means the request was accepted by AstroBox. The user still needs to tap confirm on their device to complete the Bluetooth pairing.

---

## `provider list`

List all available resource providers.

```bash
npx astrobox-cli provider list
```

**Output:** One provider name per line.
```
OfficialV2
BandBBS
MiFitness
```

---

## `provider state`

Get the current state of a provider.

```bash
npx astrobox-cli provider state OfficialV2
```

**Arguments:**
- `<name>` — Provider name

**Output:** Single word state.
```
Ready
```

Possible states: `Ready`, `Updating`, `Failed(...)`

---

## `provider categories`

Get the category list for a provider.

```bash
npx astrobox-cli provider categories OfficialV2
```

**Arguments:**
- `<name>` — Provider name

**Output:** One category per line.
```
watchface
quick_app
Xiaomi Smart Band 10
REDMI Watch 5
```

---

## `provider refresh`

Refresh a provider's cache.

```bash
npx astrobox-cli provider refresh OfficialV2
npx astrobox-cli provider refresh OfficialV2 --cfg "config-string"
```

**Arguments:**
- `<name>` — Provider name

**Options:**
- `--cfg <cfg>` — Provider configuration string (default: empty string)

**Output:**
```
Refreshing...
Provider OfficialV2 refreshed
```

---

## `provider total`

Get total item count for a provider.

```bash
npx astrobox-cli provider total OfficialV2
```

**Arguments:**
- `<name>` — Provider name

**Output:** Plain number.
```
1234
```

---

## `provider page`

Get paginated content from a provider.

```bash
npx astrobox-cli provider page OfficialV2
npx astrobox-cli provider page OfficialV2 --page 1 --limit 10 --category watchface --sort time
npx astrobox-cli provider page OfficialV2 --keyword "miku" --sort name
```

**Arguments:**
- `<name>` — Provider name

**Options:**
- `--page <page>` — Page number (default: `1`)
- `--limit <limit>` — Items per page (default: `20`)
- `--keyword <keyword>` — Search keyword (preferred over piping through grep)
- `--category <category>` — Comma-separated category filter
- `--sort <sort>` — Sort order: `time`, `name`, or `random` (default: `time`)

**Output format:**
```
Page <page> · <count> items

[<restype>] <name>
  id: <id>
[<restype>] <name>
  id: <id>
```

---

## `provider item`

Get detailed information about a specific resource item.

```bash
npx astrobox-cli provider item OfficialV2 979808740400
```

**Arguments:**
- `<name>` — Provider name
- `<id>` — Resource ID

**Output format:**
```
[<restype>] <name>
  <description>
  author: <author>

Links:
  [<icon>] <title>: <url>

Downloads:
  <display_name> (<key>)
    version: <version>
    file: <file_name>
```

---

## `provider download`

Resolve the download link for a resource item.

```bash
npx astrobox-cli provider download OfficialV2 \
  --id 979885362176 \
  --device xmb9p \
  --downloadKey xmb9p
```

**Arguments:**
- `<name>` — Provider name

**Options:**
- `--id <id>` — Resource ID (required)
- `--downloadKey <key>` — Download entry key
- `--device <device>` — Device key (required for some OfficialV2 items)
- `--trial` — Trial download flag (default: false)

**Output format:**
```
<display_name>
  version: <version>
  file:    <file_name>
  url:     <download_url>
```
