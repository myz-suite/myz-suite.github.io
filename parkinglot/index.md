---
layout: home
title: ParkingLot
hero:
  name: ParkingLot
  text: 浏览器自动化套件
  tagline: >
    链接你的 AI Agent 和 浏览器<br/>
    <a href="https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj"><img style="display: inline" src="https://img.shields.io/chrome-web-store/v/ajpkphgdonekdpifjhfffffjhikiafdj"/></a> &nbsp; <a href="https://www.npmjs.com/package/@parkinglot/server"><img style="display: inline" src="https://img.shields.io/npm/v/%40parkinglot%2Fserver?label=%40parkinglot%2Fserver"/></a>
  image:
    src: /parkinglot.png
    alt: ParkingLot 工作流
  actions:
    - text: Chrome 商店安装
      link: https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj
      theme: brand
    - text: 安装指南
      link: /parkinglot/install
features:
  - title: 真实登录态
    icon: 🔐
    details: 命令在你的 Chrome 会话里执行，天然携带登录、Cookie 与反爬环境；页面内 fetch 可访问登录后接口。
  - title: 连续性与可审计
    icon: 🧭
    details: tab / navId + 每次响应的 context 快照让 Agent 始终自证页面状态；命令默认作用于当前 tab，可用 --tab 显式指定。命令账本 JSONL 本地留痕、敏感字段脱敏。
  - title: 状态可见与稳定连接
    icon: 🟢
    details: 扩展图标以绿/红/橙角标显示连接状态，popup 提供引导与重试；断线自动重连，服务端支持 Ctrl-C 优雅退出。
  - title: 本地优先
    icon: 💻
    details: 扩展仅连接你自己运行的本地 relay，无任何远程服务，不收集遥测。
---

::: warning 版本尚未 Stable
ParkingLot 仍在快速演进，线协议与命令**可能存在破坏性变更**。请谨慎用于生产环境，升级前先查看仓库的变更说明。
:::

**ParkingLot** 是 [MyZ Suite](https://github.com/myz-suite) 下的浏览器自动化基础设施：一个 Chrome 扩展 + 一个本地 relay（Node.js），让 AI Agent（或你自己）通过简单的命令行控制真实浏览器。

- **`parkinglot-extension`**：Chrome MV3 扩展，在页面中执行命令（导航、点击、表单、提取、滚动、截图、搜索、页面内请求）。[Chrome Web Store 安装](https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj)。
- **`parkinglot-server`**：本机 relay（`plt` CLI / HTTP），`npm install -g @parkinglot/server` 安装。负责扩展配对、命令路由、当前 tab 与事件缓存。服务只绑 `127.0.0.1` 且需 token 配对，`eval` 默认禁用。
- 数据只在你本机与你自己打开的站点之间流动。
