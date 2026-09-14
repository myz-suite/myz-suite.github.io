---
layout: home
title: ParkingLot
hero:
  name: ParkingLot
  text: Browser Automation
  tagline: >
    Connect your browser to your AI agent<br/>
    <a href="https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj"><img style="display: inline" src="https://img.shields.io/chrome-web-store/v/ajpkphgdonekdpifjhfffffjhikiafdj"/></a> &nbsp; <a href="https://www.npmjs.com/package/@parkinglot/server"><img style="display: inline" src="https://img.shields.io/npm/v/%40parkinglot%2Fserver?label=%40parkinglot%2Fserver"/></a>
  image:
    src: /parkinglot.png
    alt: ParkingLot Workflow  
  actions:
    - text: Install from Chrome Web Store
      link: https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj
      theme: brand
    - text: Installation
      link: /en/parkinglot/install
    - text: Guide
      theme: alt
      link: /en/parkinglot/guide
features:
  - title: Real login state
    icon: 🔐
    details: Commands run inside your Chrome session — cookies, logins and anti-bot realism included; in-page fetch reaches authenticated APIs.
  - title: Continuity & auditability
    icon: 🧭
    details: session / tab / navId plus a context snapshot on every response lets the agent verify page state; a local JSONL command ledger redacts secrets.
  - title: Visible status, stable connection
    icon: 🟢
    details: A toolbar badge (green/red/orange) shows the connection state with popup guidance and Retry; connections auto-reconnect and the server shuts down gracefully on Ctrl-C.
  - title: Local first
    icon: 💻
    details: The extension only connects to a relay you run yourself — no remote service, no telemetry.
---

::: warning Not yet stable
ParkingLot is still evolving — the wire protocol and commands **may change in breaking ways**. Use it with caution in production, and review the repository changelog before upgrading.
:::

**ParkingLot** is the browser-automation infrastructure of [MyZ Suite](https://github.com/myz-suite): a Chrome extension plus a local relay (Node.js) that lets an AI agent — or you — drive a real browser with simple commands.

- **`parkinglot-extension`**: Chrome MV3 extension executing page commands (navigation, clicks, forms, extraction, scrolling, screenshots, search, in-page requests). [Install from Chrome Web Store](https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj).
- **`parkinglot-server`**: local relay with the `plt` CLI / HTTP — `npm install -g @parkinglot/server`. Handles extension pairing, command routing, sessions and human approvals.
- Data flows only between your machine and the sites you open.
