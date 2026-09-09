# Installation

ParkingLot has two parts: **parkinglot-server** (the relay) and **parkinglot-extension** (the Chrome extension). Install the server, install the extension, then pair them.

## Prerequisites

- **Node.js ≥ 20** (for the server)
- **Chrome / Chromium ≥ 120** (for the extension)

## 1. Install & run the server (npm global)

```bash
npm install -g @parkinglot/server
```

Run the relay (foreground; Ctrl-C to stop):

```bash
plt serve
```

The startup log prints the listen address and **pair token** (default `http://127.0.0.1:8787`; the token persists in `~/.parkinglot/token`, override with `plt serve --token <custom>`):

```
parkinglot-server listening on http://127.0.0.1:8787
pair token: e59fd1316be7aa2fb839fd016fbe1b0b589ce08ee6af2db3
```

> Alternatively run from source: `git clone https://github.com/myz-suite/parkinglot && pnpm install && pnpm build`, then `pnpm --filter @parkinglot/server start`.

## 2. Install the extension (Chrome Web Store)

Open the store page in Chrome and install:

<p><a class="markdown" href="https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj">🔗 ParkingLot — Chrome Web Store</a></p>

Pin the extension to the toolbar after installing.

## 3. Pair (once)

1. Open the extension popup.
2. Enter **Server URL** `http://127.0.0.1:8787` and the **pair token** printed by `plt serve`.
3. Click **Save & Connect** — the button becomes **Connected ✓**.

Pairing is stored locally; the extension auto-reconnects after Chrome restarts.

## 4. Verify

```bash
plt status
# extension: connected ✅
```

## (Optional) Agent users: install the parkinglot skill

To let an AI agent drive the browser through this stack, install the companion skill:

```bash
npx skills add myz-suite/parkinglot --skill parkinglot
```

The skill provides the command reference, the session/tab/navId continuity model and standard workflows (see the [guide](/en/parkinglot/guide)).
