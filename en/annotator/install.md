# Installation Guide

Choose your browser and install MyZ Annotator from the respective store:

- Chrome Web Store: <https://chromewebstore.google.com/detail/myz-annotator/mhakfcbobhdemicjelhjjpmgibhnnplg>
- Microsoft Edge Add-ons: <https://microsoftedge.microsoft.com/addons/detail/myz-annotator/fepakkoggnancnpcclldodfbpgobkabj>

You can also click “Install on Chrome” or “Install on Edge” on the homepage to jump directly to the correct listing.

## Get started

1. Pin the extension icon to the toolbar so you can open it quickly.
2. Select any text on the page—the floating toolbar appears next to your selection so you can highlight, underline, add wavy lines, or 📸 capture a screenshot.
3. The badge on the toolbar icon shows how many highlights exist on the current page.
4. Open the popup or dashboard to manage highlights: search, filter by tag, import/export, and downgrade entries to plain text when needed.

## Dashboard Settings (feature configuration)

In the Dashboard top navigation, click **Settings** to configure:

### Highlight preferences

- **View mode**: choose the default card or list view for the highlight list.
- **Color palette**: pick the 5-color palette used for annotations; colors can be customized.
- **Default style**: set the default annotation style for new highlights (marker / underline / wavy).
- **Default color**: set the default color for new highlights.

### Appearance

- **Theme**: choose Follow system / Light / Dark.

### Import highlights

- **File import**: supports MyZ JSON, RainDrop CSV, Weava CSV, and Chrome bookmarks HTML files.
- **Conflict strategy**:
  - **Skip duplicates**
  - **Overwrite duplicates**
  - **Keep the latest**

### Encrypted Sync (E2EE)

Encrypted sync uses your own S3-compatible storage; we do not run any online service. Only ciphertext and minimal metadata are stored remotely. The sync secret is derived from the password you enter, and we do not store that password.

- Recommended: **AWS S3**, **Cloudflare R2**, or any other **S3-compatible** provider.
- Fill Endpoint / Region / Bucket / Access Key / Secret Key (Session Token and Prefix are optional).
- Save settings, test the connection, then set the sync secret and enable sync.

::: warning
The sync secret stays local and cannot be recovered. If you forget the password, new clients cannot decrypt old data and you must re-encrypt and re-sync.
:::

## FAQ highlights

- **How do I export to Markdown?** Use the detail panel or the dashboard’s “Copy Markdown” action.
- **What if the page is an SPA and navigation resets my highlights?** The extension monitors URL changes and replays highlights. If locating fails, the popup and dashboard will flag the entry so you can downgrade it.