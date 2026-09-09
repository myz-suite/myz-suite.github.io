# Guide

Send commands via the `plt` CLI to the local relay; the extension executes them in the real browser.

## Command cheatsheet

| Group | Commands |
|---|---|
| Status | `plt status` · `plt ping` |
| Navigation | `plt goto <url>` · `plt back` · `plt forward` · `plt reload` |
| Interaction | `plt click <css>` · `plt click-text <text>` · `plt fill <css> <value>` · `plt type <css> <text>` · `plt press <key>` · `plt hover <css>` · `plt select <css> --value <v>` |
| View | `plt scroll <up\|down\|top\|bottom\|amount>` · `plt screenshot --path out.png` |
| Extract | `plt extract [--limit N]` · `plt page-info` |
| Network | `plt fetch <url> [--method POST] [--header "k: v"]…` · `plt search <query> [--engine google\|duckduckgo] [--page N]` |
| Tabs | `plt tabs` · `plt tab <id>` · `plt tab-new <url>` · `plt tab-close [id]` |
| Session/ops | `plt session list\|new\|use\|close\|mode` · `plt logs [--follow]` · `plt approve <id>` · `plt deny <id>` |

Global flags: `--server <url>`, `--json`, `--timeout <ms>`, `--session <id>`.

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
plt extract --limit 3000
plt scroll down && plt extract --limit 3000

# Authenticated API from the page
plt goto https://github.com
plt fetch https://api.github.com/user --header "Accept: application/json"
```

## Human-in-the-loop

```bash
plt session mode <id> --mode ask    # ask mode for this session (default auto)
plt click-text "Delete"             # write op parks until approved
# Approve: popup approval queue (✔/✖), or
#         plt approve <requestId> / plt deny <requestId>
```

- Read-only commands (extract/tabs/page-info…) never park.
- Deny or timeout (60s) means the op is not executed (fail-closed).
- Restore with `plt session mode <id> --mode auto`.

## Server config (env)

| Variable | Default | Meaning |
|---|---|---|
| `PARKINGLOT_PORT` | 8787 | listen port |
| `PARKINGLOT_BIND` | 127.0.0.1 | loopback only (do not set 0.0.0.0) |
| `PARKINGLOT_TOKEN` | auto (`~/.parkinglot/token`) | pairing token |
| `PARKINGLOT_ALLOWED_HOSTS` | none | optional domain allowlist |
| `PARKINGLOT_DISABLED_COMMANDS` | `eval` | disabled commands |
| `PARKINGLOT_ENABLE_EVAL` | 0 | explicitly enable eval |

## Security notes

- The server binds `127.0.0.1` and pairing needs the token — treat the token as a secret.
- The extension needs `<all_urls>` to execute commands on any page; use it only on machines you trust.
- `eval` is disabled by default; `search`/`fetch` and automation of third-party sites are subject to their terms and risk controls (see [FAQ](/en/parkinglot/faq) and [Privacy Policy](/en/privacy)).
