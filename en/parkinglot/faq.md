# FAQ

::: warning Not yet stable
ParkingLot is still evolving — the wire protocol and commands **may change in breaking ways**. Use it with caution in production, and review the repository changelog before upgrading.
:::

## EXTENSION_OFFLINE / cannot connect

- Check the toolbar badge: **green** = connected, **red** = disconnected (server not running / dropped), **orange** = not configured or bad token. On red/orange, open the popup and follow its guidance, then click **Retry**.
- Bad token (orange): re-copy the pair token printed by `plt serve`.
- Make sure the server is running (`plt status` against `http://127.0.0.1:8787`).
- Occasional `EXTENSION_OFFLINE`: the extension reconnects automatically after Chrome reclaims its background worker; retry shortly. If it keeps failing, check the badge state above.
- After every `pnpm build` that changes the extension, click the **refresh** button on ParkingLot in `chrome://extensions`.

## "Cannot access a chrome:// URL" / no response

Commands cannot run on Chrome-internal pages (`chrome://`, Web Store…). Open a normal page first, e.g. `plt tab-new https://example.com`.

## TARGET_NOT_FOUND / TARGET_AMBIGUOUS

Run `plt extract` to see the actual page content, then use a more specific CSS selector or text.

## "No tab with id" / SESSION_NOT_FOUND

The session's tab was likely closed. The server then clears the binding and the next command falls back to the **most recently active tab**; you can also `plt session list`, `plt session close <id>`, then `plt goto` again.

## Empty search results / paging

- Anti-bot/consent walls: switch `--engine duckduckgo`, or `plt goto` the site directly.
- Paging: `--page 2` works on google; the duckduckgo html endpoint ignores offsets.

## Automation risk on logged-in sites

The extension acts inside your own logged-in session (e.g. X, banking). Automation may trip third-party risk controls (CAPTCHA, rate limits, bans). Judge your targets and frequency yourself; we run no proxy or remote service, and you bear the consequences.

## Can I install only the extension?

No. The extension is the executor and requires a `parkinglot-server` relay that you run locally.

## Is it on the store?

Yes. The extension is live on Chrome Web Store: <https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj>. Install the server with `npm install -g @parkinglot/server` and run `plt serve` — see [Installation](/en/parkinglot/install).

## More questions?

Open an issue on the [project repository](https://github.com/myz-suite/parkinglot/issues).
