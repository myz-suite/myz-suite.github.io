# 安装指南

ParkingLot 由两部分组成：**parkinglot-server**（本机 relay）与 **parkinglot-extension**（Chrome 扩展）。安装即把它们跑起来并完成配对。

## 前置条件

- **Node.js ≥ 20** 与 **pnpm ≥ 9**（运行 server）
- **Chrome / Chromium ≥ 120**（运行扩展；依赖 `chrome.alarms` 0.5 分钟周期做 service worker 保活）

## 第 1 步：构建并启动 server

```bash
git clone https://github.com/myz-suite/parkinglot.git
cd parkinglot
pnpm install
pnpm build

# 启动 relay（前台阻塞，另开终端继续）
pnpm --filter @parkinglot/server start
```

启动输出会给出监听地址与 **pair token**（默认 `http://127.0.0.1:8787`，token 持久化于 `~/.parkinglot/token`，重启不变）：

```
parkinglot-server listening on http://127.0.0.1:8787
pair token: e59fd1316be7aa2fb839fd016fbe1b0b589ce08ee6af2db3
```

## 第 2 步：在 Chrome 加载扩展

> Chrome 137+ 移除了 `--load-extension` 命令行参数，必须用开发者模式加载。

1. 打开 `chrome://extensions`，开启右上角**开发者模式**；
2. 点**加载已解压的扩展程序**，选择 `packages/extension/dist`；
3. 工具栏出现 **ParkingLot** 图标。

## 第 3 步：配对（一次性）

1. 点扩展图标打开 popup；
2. 填入 **Server URL** `http://127.0.0.1:8787` 与 server 输出的 **pair token**；
3. 点 **Save & Connect**，按钮变为 **Connected ✓** 即成功。

配对信息保存在扩展本地存储，Chrome 重启后扩展会自动重连，无需重复操作。

## 第 4 步：验证

```bash
node packages/server/dist/cli.js status
# extension: connected ✅
```

> CLI 命令名是 **`plt`**（`packages/server/dist/cli.js`）。后续使用见[使用指南](/parkinglot/guide)。
