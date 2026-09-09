# Installation

ParkingLot has two parts: **parkinglot-server** (the local relay) and **parkinglot-extension** (the Chrome extension). Install, then pair them.

## Prerequisites

- **Node.js ≥ 20** and **pnpm ≥ 9** (for the server)
- **Chrome / Chromium ≥ 120** (for the extension; uses `chrome.alarms` 0.5-min keep-alive)

## 1. Build & start the server

```bash
git clone https://github.com/myz-suite/parkinglot.git
cd parkinglot
pnpm install
pnpm build

pnpm --filter @parkinglot/server start    # runs in the foreground
```

The startup log prints the listen address and **pair token** (default `http://127.0.0.1:8787`; the token persists in `~/.parkinglot/token` across restarts).

## 2. Load the extension in Chrome

> Chrome 137+ removed the `--load-extension` CLI flag — use developer mode.

1. Open `chrome://extensions`, enable **Developer mode** (top right).
2. Click **Load unpacked** and select `packages/extension/dist`.
3. The **ParkingLot** icon appears in the toolbar.

## 3. Pair (once)

1. Open the extension popup.
2. Enter **Server URL** `http://127.0.0.1:8787` and the server's **pair token**.
3. Click **Save & Connect** — the button becomes **Connected ✓**.

The pairing is stored locally; the extension auto-reconnects after Chrome restarts.

## 4. Verify

```bash
node packages/server/dist/cli.js status
# extension: connected ✅
```

> The CLI binary is **`plt`** (`packages/server/dist/cli.js`). Usage: see the [guide](/en/parkinglot/guide).
