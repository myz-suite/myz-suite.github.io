---
layout: home
title: ParkingLot
hero:
  name: ParkingLot
  text: Let an AI agent drive your real browser
  tagline: >
    Turn <code>goto / click / extract / screenshot / search / fetch</code> into real
    browser actions through a local relay — with your own login state and cookies<br/>
    <a href="https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj"><img style="display: inline" src="https://img.shields.io/chrome-web-store/v/ajpkphgdonekdpifjhfffffjhikiafdj"/></a> &nbsp; <a href="https://github.com/myz-suite/parkinglot"><img style="display: inline" src="https://img.shields.io/badge/GitHub-myz--suite%2Fparkinglot-1a6de0"/></a>
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
  - title: Human in the loop
    icon: 🛡️
    details: Sessions can run in ask mode so write operations need popup approval; the relay binds 127.0.0.1 with token pairing and eval is off by default.
  - title: Local first
    icon: 💻
    details: The extension only connects to a relay you run yourself — no remote service, no telemetry.
---

**ParkingLot** is the browser-automation infrastructure of [MyZ Suite](https://github.com/myz-suite): a Chrome extension plus a local relay (Node.js) that lets an AI agent — or you — drive a real browser with simple commands.

- **`parkinglot-extension`**: Chrome MV3 extension executing page commands (navigation, clicks, forms, extraction, scrolling, screenshots, search, in-page requests). [Install from Chrome Web Store](https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj).
- **`parkinglot-server`**: local relay with the `plt` CLI / HTTP — `npm install -g @parkinglot/server`. Handles extension pairing, command routing, sessions and human approvals.
- Data flows only between your machine and the sites you open.
