# MyZ Annotator & MyZ Danmaku Viewer Privacy Policy

**Effective date:** 2026-09-17

MyZ Annotator helps you highlight, annotate, and capture screenshots in your browser, and manage everything locally. MyZ Danmaku Viewer fetches timestamped YouTube comments and renders an on-device floating danmaku layer. ParkingLot is a browser-automation bridge whose extension connects only to a relay you run yourself on `127.0.0.1`, letting an AI agent (or you) drive real browser actions by command. This policy explains what data these extensions access, how it is used, and the choices you have.

## Data We Store Locally

- Highlighted text, associated notes, tags, colors, and capture metadata
- Extension settings (color palette, view preferences, encrypted sync configuration, YouTube caption style)
- Generated screenshots when you choose to download them (images are saved directly to your device and never leave the browser)
- Encrypted sync storage connection details (e.g. Endpoint, Bucket, Access Key) are kept in browser-local storage only
- For MyZ Danmaku Viewer: parsed comment details (author, timestamp, like count, text) kept locally so the danmaku overlay can work offline

All of the above is kept in browser-local storage that is scoped to your profile. We do not transmit, back up, or otherwise share this information with any external service. The MyZ Annotator / MyZ Danmaku Viewer project and maintainers never receive copies of your highlights, danmaku caches, or settings.

If you enable encrypted sync:

- You supply your own third-party S3-compatible storage (for example AWS S3, Cloudflare R2, or other compatible providers).
- Only ciphertext and minimal metadata are stored remotely; the sync secret is derived from the password you enter, we do not store that password, and the secret stays on your device and is never uploaded.
- Any outages, billing disputes, or compliance issues with the storage provider must be resolved between you and that provider; we are not responsible.

### Notes Specific to MyZ Danmaku Viewer

- The extension uses YouTube’s private interfaces to read public comments for the current video so it can detect timestamps. Requests are sent directly from your browser; we do not proxy, inspect, or store responses.
- Parsed danmaku results and related metadata remain inside your browser for offline reuse. They are not uploaded or synced anywhere.
- We do not collect your viewing history or account information. Danmaku parsing runs entirely on your device.
- Calling YouTube’s private interface relies on an unofficial channel. Google may rate-limit or block accounts or IPs that issue these requests frequently. If that happens, you are responsible for any access restrictions or playback issues that arise. We cannot compensate or mediate with Google.

## Promotional Content

To support the ongoing development of this suite, extensions in the MyZ suite may display promotional content related to this software, without affecting core functionality (for example, recommending another MyZ extension or asking you to rate this one). Specifically:

- **MyZ Danmaku Viewer** may show one clickable promotional message in the danmaku layer the first time you play a given video. It is shown only once per video, and never again for videos that are already cached or have already shown it.
- Such content relates only to this software suite. It contains **no third-party advertising** and involves no upload, sharing, or analysis of your data.
- You can turn promotional content off in the extension settings, or remove it by uninstalling the extension. We do not collect or report any personal information when you interact with promotional content.

## End-to-End Encrypted Sync (E2EE)

All synced data is end-to-end encrypted (E2EE) and never exposes plaintext to the storage platform. If you forget the password, new clients cannot decrypt old data and you must re-encrypt and re-sync. The encryption sync implementation is publicly auditable at <https://github.com/myz-suite/sync/>.

## ParkingLot (agent browser bridge)

ParkingLot pairs a Chrome extension (executor) with a `parkinglot-server` relay that you run locally. It is designed local-first; every page action is executed by the extension inside your own browser session:

- **Network**: the extension's WebSocket connects only to your relay (default `ws://127.0.0.1:8787`) after token pairing. We operate no remote service that receives, forwards, or stores commands or page data.
- **Where data lives**: the pairing token and server URL are kept in the extension's local storage; a JSONL command ledger is written by the relay into your local state dir (default `~/.parkinglot/`), with passwords, tokens and request bodies redacted.
- **Scope**: commands drive the browser to pages you specify (including sites you are logged into). The extension adds no tracking and sends no telemetry.
- **Optional capability**: `eval` (arbitrary in-page JS) is disabled by default and requires an explicit opt-in on your own server. Using `search`, `fetch`, or automating logged-in sites means accepting those sites' terms and risk controls.
- **Your call**: automating third-party sites may trigger their risk controls (CAPTCHA, rate limits, bans). What you automate, where, and how often is your decision and your responsibility.

## Permissions Explained

- `activeTab` and `tabs`: MyZ Annotator reads the current selection and captures screenshots; MyZ Danmaku Viewer identifies which YouTube video is playing.
- `<all_urls>` content script: MyZ Annotator uses this to render the toolbar and highlights; MyZ Danmaku Viewer runs only on YouTube pages to display the danmaku overlay.
- YouTube page access: Lets MyZ Danmaku read public comments for the active video so it can produce danmaku locally.
- `storage`: Required to keep your highlights, danmaku caches, and settings on-device.
- `scripting`: Used by MyZ Danmaku to add the overlay UI and styles on the page.
- ParkingLot permissions: `tabs` (list/switch tabs), `scripting` (inject the page command executor), `webNavigation` (track navigation for the navId continuity), `storage` (local server URL + pairing token), `alarms` (service-worker keep-alive), plus `host_permissions <all_urls>` to run commands on whichever page you point it at.

## No Remote Code Execution

All logic ships with the extension package. The extension never loads or executes code from remote sources.

## Your Choices

- Remove highlights, notes, or screenshots at any time via the dashboard UI.
- Disable optional network features such as encrypted sync whenever you want.
- Turn promotional content off in the extension settings at any time.
- Uninstall the extension to delete all stored data automatically.

## Changes to This Policy

If we modify how the extension handles data, we will update this document and bump the effective date. We recommend checking the repository release notes for any privacy-related updates.

## Contact

Questions or concerns? Open an issue on the [project repository](https://github.com/myz-suite/myz-support/issues).

## No Data Collection by Maintainers

MyZ Annotator is a client-side extension. The maintainers operate no backend that receives, aggregates, or analyzes user data. All network requests triggered by the extension go directly from your browser to services that you configure or access (for example, your S3-compatible object storage, or YouTube). By using these optional network features, you acknowledge that you understand the associated privacy implications and accept any risks and costs.