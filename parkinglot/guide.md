# 使用指南

::: warning 版本尚未 Stable
ParkingLot 仍在快速演进，线协议与命令**可能存在破坏性变更**。请谨慎用于生产环境，升级前先查看仓库的变更说明。
:::

通过 `plt` CLI 向本地 relay 发命令，扩展在真实浏览器中执行。

## 命令速查

| 分类 | 命令 |
|---|---|
| 状态 | `plt status` · `plt ping` |
| 导航 | `plt goto <url>` · `plt back` · `plt forward` · `plt reload` |
| 交互 | `plt click <css>` · `plt click-text <text>` · `plt fill <css> <value>` · `plt type <css> <text>` · `plt press <key\|combo>`（如 `Control+c`） · `plt hover <css>` · `plt select <css> --value <v>` |
| 视图 | `plt scroll <up\|down\|top\|bottom\|amount>` · `plt screenshot [--path out.png] [--selector <css>]` |
| 提取 | `plt extract [--selector <css>] [--mode text\|structured] [--article] [--depth N] [--offset N] [--limit N] [--max-chars N]` · `plt page-info` |
| 网络 | `plt fetch <url> [--method POST] [--header "k: v"]…` · `plt search <query> [--engine google\|duckduckgo] [--page N]` |
| 标签页 | `plt tabs` · `plt tab <id>` · `plt tab-new <url>` · `plt tab-close [id]` |
| 会话/运维 | `plt session list\|new\|use\|close` · `plt logs [--follow]` · `plt events [--tail N]` |

全局选项：`--server <url>`、`--json`、`--timeout <ms>`、`--session <id>`。运行 `plt <命令> --help` 查看该命令的选项。

要点：

- `plt screenshot` 不给 `--path` 时默认写入 `./screenshot-<时间戳>.png` 并打印绝对路径。
- `plt extract --article` 返回 **Markdown** 正文 + YAML frontmatter。
- `plt extract --mode structured --selector …` 返回 DOM 树，含 `total` 并回显 `offset`/`limit`，可据此翻页。

## 连续性模型：session / tab / navId

- **Session** 是逻辑目标：首次 `plt goto` 自动创建并成为默认，后续命令默认作用于它。
- **tabId** 是物理标签页；**navId** 每次页面导航递增。
- 每个命令响应都携带 `context {url, title, navId, tabId}` 快照 —— **`context` 变了就是页面变了**（URL/title 变化=跳转；navId 递增=发生导航）。Agent 应先读 context 再决定是否沿用旧内容。

```bash
plt goto https://example.com    # session=pl-xxx, navId=1
plt extract                     # 同一 session
plt click-text "Learn more"     # 真实点击 → 页面跳转 → navId=2, url 变化
```

## 常见工作流

```bash
# 查资料
plt search "playwright vs puppeteer"
plt goto https://github.com/…   # 从结果挑一个
plt extract --max-chars 3000
plt scroll down && plt extract --max-chars 3000

# 带登录态的 API 请求（在已登录站点页面执行）
plt goto https://github.com
plt fetch https://api.github.com/user --header "Accept: application/json"
```

## 连接状态与事件

- 扩展工具栏图标以 **绿/红/橙** 角标显示连接状态（绿=已连接、红=断开、橙=未配置或 token 错误）；popup 内有引导与 **Retry**。
- 断开会自动重连；token 被拒时停止自动重连，需修正配置。
- 标签页生命周期事件（`tab.created`/`tab.removed`）由 server 缓存，`plt events` 查看；其他命令输出会附带未读数提醒。
- session 绑定的标签页被关闭后，绑定清除并自动回退到最近激活的标签页。

## 服务端配置（环境变量）

| 变量 | 默认 | 说明 |
|---|---|---|
| `PARKINGLOT_PORT` | 8787 | 监听端口 |
| `PARKINGLOT_BIND` | 127.0.0.1 | 仅回环（勿改 0.0.0.0） |
| `PARKINGLOT_TOKEN` | 自动生成（`~/.parkinglot/token`） | 扩展配对 token |
| `PARKINGLOT_ALLOWED_HOSTS` | 空（全部） | 可选域名白名单 |
| `PARKINGLOT_DISABLED_COMMANDS` | `eval` | 禁用命令列表 |
| `PARKINGLOT_STATE_DIR` | `~/.parkinglot` | state / ledger / token 目录 |

## 安全须知

- server 只绑 `127.0.0.1`，扩展连接需 token —— token 是密钥，勿外泄。
- 扩展需要 `<all_urls>` 权限以在任意页面执行命令；请只在你信任的机器/环境使用。
- `eval` 默认禁用；`search`/`fetch` 等访问第三方站点受其条款与风控约束，请自行评估（详见[常见问题](/parkinglot/faq)与[隐私政策](/privacy)）。
