# Guide

::: warning Not yet stable
ParkingLot is still evolving — the wire protocol and commands **may change in breaking ways**. Use it with caution in production, and review the repository changelog before upgrading.
:::

Send commands via the `plt` CLI to the local relay; the extension executes them in the real browser.

## Command cheatsheet

| Group | Commands |
|---|---|
| Status | `plt status` · `plt ping` |
| Navigation | `plt goto <url>` · `plt back` · `plt forward` · `plt reload` |
| Interaction | `plt click <css>` · `plt click-text <text>` · `plt fill <css> <value>` · `plt type <css> <text>` · `plt press <key\|combo>` (e.g. `Control+c`) · `plt hover <css>` · `plt select <css> --value <v>` |
| View | `plt scroll <up\|down\|top\|bottom\|amount>` · `plt screenshot [--path out.png] [--selector <css>]` |
| Extract | `plt extract [--selector <css>] [--mode text\|structured] [--article] [--depth N] [--offset N] [--limit N] [--max-chars N]` · `plt page-info` |
| Network | `plt fetch <url> [--method POST] [--header "k: v"]…` · `plt search <query> [--engine google\|duckduckgo] [--page N]` |
| Tabs | `plt tabs` · `plt tab <id>` · `plt tab-new <url>` · `plt tab-close [id]` |
| Session/ops | `plt session list\|new\|use\|close` · `plt logs [--follow]` · `plt events [--tail N]` |

Global flags: `--server <url>`, `--json`, `--timeout <ms>`, `--session <id>`. Run `plt <command> --help` for command-specific options.

Notes:

- `plt screenshot` without `--path` writes `./screenshot-<timestamp>.png` and prints the absolute path.
- `plt extract --article` returns **Markdown** plus YAML frontmatter.
- `plt extract --mode structured --selector …` returns a DOM tree with `total` and echoed `offset`/`limit` for paging.

## Continuity model: session / tab / navId

- **Session** is the logical target: the first `plt goto` auto-creates one and it becomes the default for later commands.
- **tabId** is the physical tab; **navId** increments on every navigation.
- Every response carries a `context {url, title, navId, tabId}` snapshot — **if `context` changed, the page changed** (url/title change = navigated; navId increased = a navigation happened). Read it before trusting stale content.

```bash
plt goto https://example.com    # session=pl-xxx, navId=1
plt extract                     # same session
plt click-text "Learn more"     # real click → page navigates → navId=2, url changed
```

## Common workflows

```bash
# Research
plt search "playwright vs puppeteer"
plt goto https://github.com/…   # pick a result
plt extract --max-chars 3000
plt scroll down && plt extract --max-chars 3000

# Authenticated API from the page
plt goto https://github.com
plt fetch https://api.github.com/user --header "Accept: application/json"
```

## Connection status & events

- The toolbar badge shows the connection state — **green** = connected, **red** = disconnected, **orange** = not configured or bad token; the popup offers guidance and **Retry**.
- Disconnects auto-reconnect; a rejected token stops auto-reconnect until the config is fixed.
- Tab lifecycle events (`tab.created`/`tab.removed`) are cached by the server and shown by `plt events`; other commands append an unread count reminder.
- When a session's tab is closed, the binding is cleared and the next command falls back to the most recently active tab.

## Server config (env)

| Variable | Default | Meaning |
|---|---|---|
| `PARKINGLOT_PORT` | 8787 | listen port |
| `PARKINGLOT_BIND` | 127.0.0.1 | loopback only (do not set 0.0.0.0) |
| `PARKINGLOT_TOKEN` | auto (`~/.parkinglot/token`) | pairing token |
| `PARKINGLOT_ALLOWED_HOSTS` | none | optional domain allowlist |
| `PARKINGLOT_DISABLED_COMMANDS` | `eval` | disabled commands |
| `PARKINGLOT_STATE_DIR` | `~/.parkinglot` | state / ledger / token dir |

## Security notes

- The server binds `127.0.0.1` and pairing needs the token — treat the token as a secret.
- The extension needs `<all_urls>` to execute commands on any page; use it only on machines you trust.
- `eval` is disabled by default; `search`/`fetch` and automation of third-party sites are subject to their terms and risk controls (see [FAQ](/en/parkinglot/faq) and [Privacy Policy](/en/privacy)).
