# Terms of Service

**Effective date:** 2026-01-12

These Terms of Service govern how you may use the MyZ Annotator, MyZ Danmaku Viewer and ParkingLot browser extensions. Installing or using either extension means you accept these terms.

## Eligibility
You must have the legal capacity to enter into a binding agreement in your jurisdiction. If you use the extension on behalf of an organization, you confirm that you are authorized to bind that organization to these terms.

## License and Acceptable Use
You receive a limited, non-exclusive, revocable license to install and use the extensions for personal or internal business purposes. Do not reverse engineer the extensions (unless permitted by law), remove notices, or use them to violate any law or third-party rights.

## Local-Only Data Handling
All highlights, danmaku caches, settings, and credentials remain inside your browser storage. The maintainers operate **no remote service** to receive, store, or process your data. If you enable encrypted sync, you provide your own third-party S3-compatible storage; only ciphertext and minimal metadata are stored remotely. The sync secret is derived from the password you enter, and we do not store that password.

## Optional Features
- **Encrypted Sync (S3-compatible):** You may configure your own storage (e.g., AWS S3, Cloudflare R2, or other S3-compatible services) and set a local sync secret. Requests are sent directly from your browser to your configured storage.
- **MyZ Danmaku Viewer:** Uses YouTube’s private interfaces from your browser to fetch public comments and generate danmaku locally. You must comply with YouTube/Google policies.

These features are entirely optional and under your control. You are responsible for the consequences of enabling them and for complying with third-party terms and policies. In particular:

- Do not send sensitive or private data to third-party servers unless you fully understand and accept their data-handling practices.
- We do not provide any remote service and are not responsible for any loss, leakage, charges, disputes, or liabilities caused by your use of third-party servers.
- The storage provider used for encrypted sync is chosen by you. Any outages, data loss, billing disputes, or compliance issues must be resolved between you and the storage provider; we are not responsible.

## End-to-End Encrypted Sync
All synced data is end-to-end encrypted (E2EE) and never exposes plaintext to the storage platform. If you forget the sync password, new clients cannot decrypt old data and you must re-encrypt and re-sync. The encryption sync implementation is publicly auditable at <https://github.com/myz-suite/sync/>.

## ParkingLot Terms

**ParkingLot** automates actions inside your own browser session:

- **Local operation**: you must build and run the companion `parkinglot-server` relay yourself and are responsible for protecting its pairing token and local state directory. We provide no remote or hosted service.
- **Scope of authorization**: only commands you (or an AI agent you explicitly authorized) issue via `plt`/HTTP are executed. The extension never visits sites on its own; pages are driven by commands.
- **Third-party risk is yours**: automating third-party sites (logged-in accounts, search engines, APIs) may trigger their risk controls, breach their terms, or lead to account restrictions. You decide what, how and how often to automate and bear the consequences.
- **Do not leak secrets**: avoid passing passwords or tokens in plaintext in commands; although the command ledger redacts sensitive fields, do not put keys in query parameters.
- **Out-of-scope operations**: `eval` (arbitrary JS) is disabled by default; enable it on your local server only after your own assessment.

## Third-Party Content and Services
You are solely responsible for ensuring that annotating or reusing content complies with all applicable laws, website terms, and third-party rights.

## No Warranties & Limitation of Liability
The extensions are provided "as is" without any warranty. Use them at your own risk. To the fullest extent permitted by law, the maintainers and contributors are not liable for any indirect or consequential damages arising from your use or inability to use the extensions or optional features. For MyZ Danmaku Viewer specifically, Google may change or restrict access to these private interfaces at any time. If that results in account limitations, playback failures, or other issues, you bear the responsibility.

## Indemnity
You agree to indemnify and hold harmless the maintainers and contributors against claims or losses stemming from your use of the extension or violation of these terms.

## Termination and Changes
We may modify or discontinue the extension without notice. You may stop using it at any time by uninstalling the extension. We may update these terms occasionally; the effective date will change accordingly. Continued use means you accept the updates.

## Contact
Questions? Open an issue on the [project repository](https://github.com/myz-suite/myz-support/issues).