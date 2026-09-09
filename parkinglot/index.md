---
layout: home
title: ParkingLot
hero:
  name: ParkingLot
  text: 让 AI Agent 控制你的真实浏览器
  tagline: >
    通过本地 relay 把 <code>goto / click / extract / screenshot / search / fetch</code> 等命令
    变成真实浏览器操作 —— 带上你自己的登录态与 Cookie<br/>
    <a href="https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj"><img style="display: inline" src="https://img.shields.io/chrome-web-store/v/ajpkphgdonekdpifjhfffffjhikiafdj"/></a> &nbsp; <a href="https://github.com/myz-suite/parkinglot"><img style="display: inline" src="https://img.shields.io/badge/GitHub-myz--suite%2Fparkinglot-1a6de0"/></a>
  actions:
    - text: Chrome 商店安装
      link: https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj
      theme: brand
    - text: 安装指南
      link: /parkinglot/install
    - text: 使用指南
      theme: alt
      link: /parkinglot/guide
features:
  - title: 真实登录态
    icon: 🔐
    details: 命令在你的 Chrome 会话里执行，天然携带登录、Cookie 与反爬环境；页面内 fetch 可访问登录后接口。
  - title: 连续性与可审计
    icon: 🧭
    details: session / tab / navId + 每次响应的 context 快照让 Agent 始终自证页面状态；命令账本 JSONL 本地留痕、敏感字段脱敏。
  - title: 人工可控
    icon: 🛡️
    details: 会话可切 ask 模式，写操作需在扩展 popup 批准；服务只绑 127.0.0.1 且需 token 配对，eval 默认禁用。
  - title: 本地优先
    icon: 💻
    details: 扩展仅连接你自己运行的本地 relay，无任何远程服务，不收集遥测。
---

**ParkingLot** 是 [MyZ Suite](https://github.com/myz-suite) 下的浏览器自动化基础设施：一个 Chrome 扩展 + 一个本地 relay（Node.js），让 AI Agent（或你自己）通过简单的命令行控制真实浏览器。

- **`parkinglot-extension`**：Chrome MV3 扩展，在页面中执行命令（导航、点击、表单、提取、滚动、截图、搜索、页面内请求）。[Chrome Web Store 安装](https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj)。
- **`parkinglot-server`**：本机 relay（`plt` CLI / HTTP），`npm install -g @parkinglot/server` 安装。负责扩展配对、命令路由、会话与人工审批。
- 数据只在你本机与你自己打开的站点之间流动。
