# abcli Output Parsing Guide

abcli outputs plain text, not JSON. Use string matching and regex to extract fields.

---

## `status` output

```
AstroBox: connected
Devices: 2
- Xiaomi Smart Band 9 Pro C692 (3C:AF:B7:ED:C6:92) [connected]
```

**Parse:**
- First line: `AstroBox: (connected|unavailable)`
- Second line: `Devices: (\d+)`
- Device lines: `- (.+) \(([^)]+)\) \[(connected|disconnected)\]`
  - Group 1: device name
  - Group 2: MAC address
  - Group 3: status

---

## `device list` output

```
Devices: 1
- Xiaomi Smart Band 9 Pro C692 (3C:AF:B7:ED:C6:92) [connected]
```

**Parse:** Same pattern as `status` device lines.

---

## `device show` output

```
Name:     Xiaomi Smart Band 9 Pro C692
Address:  3C:AF:B7:ED:C6:92
AuthKey:  abcdef123456...
Status:   connected
SAR Ver:  2
TX Win:   6
Type:     SPP
```

**Parse:** Each line is `Label: value`. Use `^(.+?):\s*(.+)$` per line.

Key mappings:
- `Name` → `name`
- `Address` → `addr`
- `AuthKey` → `authkey`
- `Status` → `status`
- `SAR Ver` → `sarVersion`
- `TX Win` → `txWinOverrunAllowance`
- `Type` → `connectType`

---

## `provider page` output

```
Page 1 · 5 items

[watchface] 「矩」- 橘雪莉
  id: 979805910807
[quick_app] 愤怒的小球
  id: com.Dreamqiu.angryballs
```

**Parse:**
- Header: `Page (\d+) · (\d+) items`
- Items are separated by blank lines.
- Each item starts with `\[(\w+)\] (.+)` → restype, name
- Next line: `  id: (.+)` → id

---

## `provider item` output

```
[watchface] The Commander 体验版
  掌控全局。
  author: hrsthrt74

Links:
  [chats-circle] 交流群: https://...

Downloads:
  Xiaomi Smart Band 9 Pro (xmb9p)
    version: v1.0
    file: 体验版 The Commander for Band9Pro v1.0 by hrsthrt74.bin
```

**Parse:**
- Header: `\[(\w+)\] (.+)` → restype, name
- Description lines: `  (.+)` (before author/links/downloads)
- Author: `  author: (.+)`
- Links section starts with `Links:`. Each link: `  \[(.+?)\] (.+?): (.+)`
- Downloads section starts with `Downloads:`. Each entry:
  - `  (.+) \(([^)]+)\)` → display_name, key
  - `    version: (.+)`
  - `    file: (.+)`

---

## `provider download` output

```
Xiaomi Smart Band 9 Pro
  version: v1.0.0
  file:    resource.bin
  url:     https://raw.githubusercontent.com/...
```

**Parse:**
- First line: display name (raw, no label)
- `  version: (.+)`
- `  file:\s+(.+)`
- `  url:\s+(.+)` → the actual download URL

**Important:** The `url` field is what you need to download the file.

---

## `provider state` output

Single word, no labels:
```
Ready
```

**Parse:** Read entire stdout, trim whitespace.

---

## `provider total` output

Plain number:
```
1234
```

**Parse:** `parseInt(stdout.trim(), 10)`

---

## `provider list` output

One name per line:
```
OfficialV2
BandBBS
```

**Parse:** `stdout.trim().split('\n')`

---

## `provider categories` output

One category per line:
```
watchface
quick_app
```

**Parse:** `stdout.trim().split('\n')`

---

## Error output format

All errors go to stderr and follow this format:
```
Error: <message>
```

Exit code is always `1` on error. Check stderr first before parsing stdout.
