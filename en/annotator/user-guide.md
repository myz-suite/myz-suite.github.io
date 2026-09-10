# User Guide (MyZ Annotator)

This document explains how to use MyZ Annotator’s core highlighting features and the Dashboard settings.

> Important (network features)
>
> - The extension provides **no remote service**. Any optional network requests are sent **directly from your browser** to third-party services you configure (for example: S3-compatible storage).
> - Encrypted sync is end-to-end encrypted (E2EE): only ciphertext and minimal metadata go to your storage; the sync secret stays local.
> - Be careful with sensitive/private data.

> UI language note
>
> Some menus/buttons in the extension are currently labeled in Chinese. This guide includes the exact labels in backticks so you can find them easily.

## 1. Installation and entry points

- After installing, pin the extension to your browser toolbar.
- **Popup**: click the extension icon for a quick view of highlights on the current page.
- **Dashboard (management & settings)**: in the popup, click the “Open Dashboard” button (Chinese UI: `打开 Dashboard`) to open the options page.

## 2. Basic annotation (highlight / underline / wavy underline)

1. Select text on the page.
2. A floating toolbar appears near your selection:
   - `添加标注` (Add annotation): creates a replayable highlight annotation (with color/style).
   - `保存文字` (Save text): saves the selected text as a “text-only” record (no highlight DOM is applied to the page).
   - `截取选区截图` (Capture selection screenshot): captures a screenshot of the selection (the extension temporarily clears the native selection highlight before capturing to avoid blue selection artifacts).
3. The extension badge on the toolbar icon shows how many highlights exist on the current page.

## 3. Manage and organize (Popup / Dashboard)

### 3.1 Popup: quick view for the current page

- Shows the highlights/text clips for the current page.
- Provides quick actions such as open details, edit, delete, and jump to Dashboard.

### 3.2 Dashboard: global management & settings

The Dashboard top navigation contains:

- **Highlights list**: shows all annotations with card/list views (your last choice is remembered), multi-select tags, full-text search, date-range and site filters, and lazy loading for performance.
- **Highlight viewer**: open any highlight at `/highlights/:id` for continuous reading of same-page annotations, scroll-to-end auto-advance, and previous/next navigation.
- **Settings** (Chinese UI: `设置`): highlight preferences, appearance, import, and encrypted sync (see section 4).

## 4. Dashboard Settings

### 4.1 Highlight preferences

- **View mode**: default card or list view for the highlight list.
- **Color palette**: the 5-color palette used for annotations; colors are customizable.
- **Default style / Default color**: default style (marker / underline / wavy) and color for new highlights.

### 4.2 Appearance

- **Theme**: Follow system / Light / Dark.

### 4.3 Import highlights

- Supports **MyZ JSON**, **RainDrop CSV**, **Weava CSV**, and **Chrome bookmarks HTML** files.
- Choose a conflict strategy: **skip / overwrite / keep latest**; a summary is shown when the import finishes.

### 4.4 Encrypted Sync (E2EE)

Encrypted sync uses your own S3-compatible storage; we do not run any online service. Only ciphertext and minimal metadata are stored remotely, and the sync secret stays on your device. The sync secret is derived from the password you enter, and we do not store that password.

Recommended storage: **AWS S3**, **Cloudflare R2**, or any other **S3-compatible** storage provider.

### 4.5 Setup steps

1. Open Dashboard → Settings → **Encrypted Sync** (`加密同步`).
2. Fill in the S3 settings:
   - **Endpoint**: the S3-compatible endpoint URL
   - **Region / Bucket**
   - **Access Key ID / Secret Access Key**
   - **Session Token** (optional)
   - **Prefix** (optional): isolate data across devices/projects
3. Click **Save settings** (`保存设置`), then **Test connection** (`测试连接`).
4. Set the **Sync secret** (`同步密钥`) — it stays local; use a strong passphrase.
5. Enable **Sync** (`启用同步`) and click **Sync now** (`立即同步`) once.

The status panel shows KeyId, Manifest version, last sync time, and key updated time.

::: warning Important
The sync secret cannot be recovered. If you forget the password, new clients cannot decrypt old data; you must re-encrypt and re-sync from scratch.
:::

::: tip Public audit
The E2EE implementation is open for review at <https://github.com/myz-suite/sync/>.
:::

## 5. Zen Mode

On pages with a detectable article body, you can use the right-click menu:

- `禅定模式 (仅显示文章)` (Zen Mode): keeps only the primary article content for a distraction-free view (designed to be non-destructive to DOM structure so highlight restoration remains stable)
- `保存文章为图片` (Save article as image): available only when Zen Mode is enabled; captures the article body

If you don’t see the menu, the extension couldn’t detect a suitable article container on that page.

## 6. Troubleshooting

- **Highlight cannot be located?** Page structure changes may temporarily prevent restoration; downgrade the entry to plain text from the Popup or Dashboard so its content isn’t lost.
- **Overlapping highlight?** The extension warns you and refuses to create the annotation to avoid nesting, which would break positioning.
- **Highlight not refreshed after SPA navigation?** The extension listens to History API and URL changes and replays highlights; if it still misbehaves, reload the extension and try again.