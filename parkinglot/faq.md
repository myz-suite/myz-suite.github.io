# 常见问题

::: warning 版本尚未 Stable
ParkingLot 仍在快速演进，线协议与命令**可能存在破坏性变更**。请谨慎用于生产环境，升级前先查看仓库的变更说明。
:::

## 扩展提示 EXTENSION_OFFLINE / 连不上

- 看扩展工具栏图标角标：**绿**=已连接、**红**=断开（server 未运行或掉线）、**橙**=未配置或 token 错误。红色/橙色时打开 popup 按提示处理，点 **Retry** 重试。
- token 错误（橙色）：重新复制 `plt serve` 输出的 pair token 填入。
- 确认 server 正在运行（`plt status` 可访问 `http://127.0.0.1:8787`）。
- 偶发 `EXTENSION_OFFLINE`：浏览器回收扩展后台后会自动重连，稍等重试即可；若持续失败请按上面的角标状态排查。
- 每次 `pnpm build` 改动扩展代码后，需在 `chrome://extensions` 点 ParkingLot 的**刷新**按钮重新加载。

## 命令报错 "Cannot access a chrome:// URL" / 无响应

扩展无法在 `chrome://`、Web Store 等 Chrome 内部页面执行命令。请先在普通网页上操作，例如 `plt tab-new https://example.com`。

## TARGET_NOT_FOUND / TARGET_AMBIGUOUS

先 `plt extract` 查看页面真实内容，再改用更精确的 CSS selector 或文本。

## session 报错 "No tab with id" / SESSION_NOT_FOUND

会话指向的标签页可能已被关闭。此时 server 会清除该绑定，下一条命令自动回退到**最近激活的标签页**；也可 `plt session list` 查看、`plt session close <id>` 后重新 `plt goto`。

## search 返回为空或想翻页

- 反爬/验证码：换 `--engine duckduckgo`，或 `plt goto` 直接访问。
- 翻页：`--page 2`（google 支持；duckduckgo html 端点不支持 offset）。

## 对登录站点的自动化风险

扩展在你自己的登录会话中操作（例如 X/银行等）。自动化可能触发第三方风控（验证码、限流、封禁）。请自行判断使用对象与频率；我们不运营任何代理或远程服务，相关风险与后果由你自行承担。

## 我可以只装扩展吗？

不能。扩展是"执行端"，必须搭配你自己运行的本地 `parkinglot-server` 使用。

## 商店里可以安装吗？

可以。扩展已上架 Chrome Web Store：<https://chromewebstore.google.com/detail/ajpkphgdonekdpifjhfffffjhikiafdj>。server 通过 `npm install -g @parkinglot/server` 安装并 `plt serve` 启动，详见[安装指南](/parkinglot/install)。

## 更多问题？

欢迎在[项目仓库 Issue](https://github.com/myz-suite/parkinglot/issues) 反馈。
