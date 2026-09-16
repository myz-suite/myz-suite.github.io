# Release Notes

Highlights from recent extension updates.

## v0.6.3 — PDF reader sidebar & selection fixes

- New sidebar in the PDF reader: navigate by table of contents (bookmarks), or browse highlights by page and jump precisely to an annotation; the sidebar state and active tab are remembered.
- Search your highlights by text, note or tag, and filter by kind (highlight / saved text).
- Fixed underline / wavy decorations covering text before and after the selection.
- Fixed selection and highlights spilling into the right margin on long paragraphs.
- Fixed opening a local PDF from the Dashboard failing with a `requestPermission` error; added a “Re-authorize and open” retry when needed.

## v0.6.1 — PDF reading & annotation

- Added a built-in PDF reader: open local files or web PDFs, with continuous scrolling, zoom (50%–300%) and reading-progress memory.
- Select PDF text to highlight / save text and add notes and tags; reopening the same PDF restores highlights (local by file fingerprint, web by URL).
- Supports JPEG2000 / JBIG2 image-based PDFs.
- Entry points: the popup PDF button and the right-click `在 MyZ 中打开 PDF` link action; web PDFs without a `.pdf` suffix (e.g. arXiv) are detected too.
- Dashboard shows a “page N” badge and can jump back to the corresponding reader page.
- New annotations reuse the last used highlight style and color; the inspector now has an explicit Save button and status.
- Note: local PDF support is currently Chrome-only.

## v0.6.0 — AI features removed & Dashboard consolidated

- Removed the AI Assistant (Side Panel) and all related capabilities: custom Providers, MCP servers, local tools, Agent Skills, vector search (Vectoria), auto highlight, Superpower multi-agent collaboration, and the Dashboard chat page.
- Removed social import (X / Mastodon); imports are now file-based (MyZ JSON, RainDrop CSV, Weava CSV, Chrome bookmarks HTML).
- Slimmed down extension permissions and the right-click menu: removed the `sidePanel` permission; only Zen Mode items remain.
- Consolidated the Dashboard into highlight management and settings: highlight list, highlight viewer, and settings (highlight preferences / appearance / import / sync).

## v0.5.0 — Dashboard UI refactor & interaction polish

- The ThemeToggle dropdown now reflects the effective theme and no longer gets clipped by panels.
- Highlight card type icons and action buttons use lucide icons with hover tooltips.
- Compact tag layout; card view switched to a CSS-columns masonry flow; summary content uses prose typography.
- Card notes are stacked vertically to fit masonry card heights.
- Added a search button to the content floating toolbar: opens a new page to search the selected text via the browser.

## v0.4.4 — Provider tiering & Mistral SDK

- Added a `mistral` provider type using the official SDK for model listing, connection tests, chat, streaming, and tool calling.
- OpenAI-compatible requests are patched per provider profile; Tier 1 compatibility is limited to a curated list.

## v0.4.3 — OpenAI-compatible reasoning replay fix

- Fixed multi-turn chat failures with third-party OpenAI-compatible endpoints in thinking mode.
- Moved transports to official SDKs (openai / anthropic / genai) and narrowed the provider type set.

## v0.4.2 — New Dashboard viewer & page aggregation

- Added the `/highlights/:id` viewer with continuous same-page reading, scroll-to-end auto-advance, and previous/next navigation.
- Added a collapsible page sidebar to the Dashboard highlight list, with filtering by page and ordering by time/Range.
- Added a `contentType` field so annotations render as Markdown/HTML/plain text.

## v0.4.1 — Dashboard experience upgrade

- Restructured the Dashboard for clarity.
- Added a sidebar to the settings page for quick navigation between sections.
- Enhanced imports: support for RainDrop CSV and Chrome bookmarks HTML.

## v0.4.0 — Superpower mode & multi-agent collaboration

- Introduced Superpower mode with multi-agent collaboration flows.
- Cleaner, denser conversation sidebar.
- Improved conversation titles and history list.
- Fixed the palette color editor not opening.

## v0.3.2 — Auto highlight & categorized annotations

- Added auto highlight that generates key-content annotations automatically.
- “Discover key points” became a standalone entry point.
- AI settings gained auto-highlight model and category style configuration.
- Added a “one-click auto highlight” button to the popup empty state.
- More robust highlight matching with fewer errors and overlaps.

## v0.3.1 — UX & settings stability

- Fixed the Inspector not appearing after clicking a highlight, and redesigned it as a toolbar-style popover (notes show above; edit closes the panel).
- Replaced the highlight flash with a softer pulse/halo animation for better visibility in dark/paint styles.
- Interests now only appear when vector search is enabled and a model is configured; cleaned up indicators and reduced their footprint.
- Unified new SVG icons in the shared icon library, updating popup/sidepanel/inspector buttons.
- Fixed AiProviderEditor model list mis-selection during reorder; disabling a model now auto-selects the next item for editing.

## v0.3.0 — End-to-end encrypted sync (E2EE)

- Added encrypted sync with S3-compatible storage (bring your own storage configuration).
- The sync secret stays local; only ciphertext and minimal metadata are stored remotely.
- Added sync status and manual sync actions (KeyId, manifest version, last sync time).

## v0.2.0 — Agent Skills

- Introduced Agent Skills:
  - Built-in and custom skills (import via zip/folder).
  - Explicit skill invocation via `@skill-name`.
  - Auto mode that uses a selector model to pick skills per message.
- Added skill management and editor in Dashboard → AI settings.

## v0.1.5 - AI Assistant integration

- Integrated with AI Assistant:
  - Using AI models analyse page,
  - Conversation with AI models using page context,
  - Support customized AI Providers and MCP servers,
  - Discover interests using vector indexes.
- Remove LogSeq sync.
- Integrated with social network - X (Twitter), Mastodon.

## v0.1.4 — Unified icons & SPA fixes
- Replaced all toolbar/popup/dashboard emoji buttons with custom SVG icons for consistent rendering across platforms.
- Restored the marker-style highlight icon and added an underlined “U” icon so the three text styles are instantly recognizable.
- Enlarged and outlined the dashboard settings icon to improve discoverability.
- Fixed a bug where Twitter and other SPAs failed to reapply highlights when navigating internally—the overlay now listens to History API changes.

## v0.1.3 — Vue 3 architecture & resilient highlights
- Migrated the entire extension to Vite + `@crxjs/vite-plugin` + Vue 3/JSX.
- Refactored popup, dashboard, content, and background modules into composable components.
- Redesigned Range serialization so removing old highlights no longer shifts subsequent entries.
- Added overlap detection and Playwright coverage to prevent conflicting highlights.
- Updated the dark-friendly palette and kept export descriptions in sync.
- Hooked into the History API to refresh highlights after SPA navigation.
- Expanded end-to-end tests and unified the iconography.

## v0.1.2 — More highlight styles & text-only saves
- Added a “Save Text” button to store selections as plain clips.
- Popup/dashboard now distinguish highlight types and let you downgrade to text-only entries.
- Three styles—marker, underline, wavy—are all included in exports.
- Improved text-decoration rendering on narrow line-height pages.

## v0.1.1 — Highlight & screenshot upgrades
- Added import capability plus a toolbar badge that shows highlight counts.
- Warn users when entries cannot be located and fixed several stability issues.
- Screenshot capture no longer includes the selection highlight.

## v0.1.0 — Initial release
MyZ Annotator lets you highlight, annotate, capture screenshots, and manage everything locally. Export JSON/Markdown or sync directly to LogSeq.