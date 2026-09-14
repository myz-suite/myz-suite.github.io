# 安装指南

::: warning 版本尚未 Stable
ParkingLot 仍在快速演进，线协议与命令**可能存在破坏性变更**。请谨慎用于生产环境，升级前先查看仓库的变更说明。
:::

ParkingLot 由 **parkinglot-server**（relay）与 **parkinglot-extension**（Chrome 扩展）组成。安装分三步：装 server → 装扩展 → 配对。

## 前置条件

- **Node.js ≥ 20**（运行 server）
- **Chrome / Chromium ≥ 120**（运行扩展）

## 1. 安装并启动 server（npm 全局安装）

```bash
npm install -g @parkinglot/server
```

启动 relay（前台运行，Ctrl-C 停止）：

```bash
plt serve
```

启动日志会给出监听地址与 **pair token**（默认 `http://127.0.0.1:8787`；token 持久化在 `~/.parkinglot/token`，重启不变，可用 `plt serve --token <自定义>` 覆盖）：

```
parkinglot-server listening on http://127.0.0.1:8787
pair token: e59fd1316be7aa2fb839fd016fbe1b0b589ce08ee6af2db3
```

> 也可直接从源码运行：`git clone https://github.com/myz-suite/parkinglot && pnpm install && pnpm build`，再 `pnpm --filter @parkinglot/server start`。

## 2. 安装扩展（Chrome Web Store）

在 Chrome 中打开商店页并点击安装：

<p><a class="markdown" href="https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj">🔗 ParkingLot — Chrome Web Store</a></p>

安装后把扩展固定到工具栏。

## 3. 配对（一次性）

1. 点扩展图标打开 popup；
2. 填入 **Server URL** `http://127.0.0.1:8787` 与 `plt serve` 输出的 **pair token**；
3. 点 **Save & Connect**，按钮变为 **Connected ✓** 即成功。

配对信息保存在扩展本地，Chrome 重启后会自动重连，无需重复操作。

## 4. 验证

```bash
plt status
# extension: connected ✅
```

## （可选）Agent 用户：安装 parkinglot skill

若你要让 AI Agent 通过 `pl`-类 CLI 控制浏览器，可在目标环境中安装配套 skill：

```bash
npx skills add myz-suite/parkinglot --skill parkinglot
```

skill 会提供命令参考、session 连续性心智模型与标准工作流（详见[使用指南](/parkinglot/guide)）。
