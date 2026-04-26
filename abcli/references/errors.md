# abcli Error Catalog

Common errors, what they mean, and how to recover.

---

## `Could not reach AstroBox at http://127.0.0.1:10721. Is AstroBox running?`

**Meaning:** The AstroBox desktop application is not running, or its local API server is not accessible.

**Recovery:**
1. Ask the user to launch AstroBox.
2. Wait a few seconds for the API to start.
3. Retry the command.

---

## `File does not exist: <path>`

**Meaning:** The file path provided to `install` does not exist.

**Recovery:**
1. Verify the file path with the user.
2. Check if the path is relative to the correct working directory.
3. Retry with the correct path.

---

## `Device not found: <addr>`

**Meaning:** The MAC address passed to `device show` is not in the saved device list.

**Recovery:**
1. Run `npx astrobox-cli device list` to see all saved devices.
2. Check if the address format matches (case-insensitive, but colons matter).
3. If the device is new, use `device connect` instead.

---

## `Invalid connectType: <value>. Must be "SPP" or "BLE".`

**Meaning:** The `--connectType` flag received an unsupported value.

**Recovery:**
- Use `--connectType SPP` (default) or `--connectType BLE`.

---

## `Failed to connect: <message>`

**Meaning:** The `device connect` request was rejected by AstroBox.

**Recovery:**
1. Check that the name, addr, and authkey are correct.
2. Verify AstroBox is running and no other device connection is in progress.
3. Ask the user to check if their device is in pairing mode.

---

## Request failed with <status> <statusText>

**Meaning:** The AstroBox API returned a non-2xx HTTP status.

**Recovery:**
1. Read the response body in the error message for details.
2. Check if the provider name, item ID, or parameters are valid.
3. For `provider download`, verify the `--device` key is correct.

---

## `ENOENT` or `command not found`

**Meaning:** `npx` or `astrobox-cli` is not available.

**Recovery:**
1. Verify Node.js >= 20 is installed: `node --version`
2. Check npm is available: `npm --version`
3. Try installing the CLI: `npm install -g astrobox-cli`
4. Or use `npx astrobox-cli` which downloads on demand.

---

## `ENOTEMPTY` or npm cache rename errors

**Meaning:** Multiple `npx astrobox-cli` processes ran concurrently, causing npm's npx cache directory to conflict.

**Recovery:**
1. Clear the npx cache: `rm -rf ~/.npm/_npx/*`
2. Retry the command.
3. Avoid running multiple `npx astrobox-cli` commands in parallel when possible.

---

## `Install error: 没有已连接的设备，请先连接设备`

**Meaning:** The install was queued but there is no connected device to receive the file.

**Recovery:**
1. Check device status: `npx astrobox-cli status`
2. If saved devices are disconnected, reconnect one:
   ```bash
   npx astrobox-cli device show <addr>
   npx astrobox-cli device connect --name "<name>" --addr "<addr>" --authkey "<key>"
   ```
3. The user must tap confirm on their physical device.
4. Retry the install.

---

## General troubleshooting checklist

1. **Is AstroBox running?** → `npx astrobox-cli status`
2. **Is Node.js >= 20?** → `node --version`
3. **Is the port available?** → Check if `127.0.0.1:10721` is accessible
4. **Are parameters valid?** → Cross-check with `provider list`, `device list`, etc.
