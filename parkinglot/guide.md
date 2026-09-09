# 使用指南

通过 `plt` CLI 向本地 relay 发命令，扩展在真实浏览器中执行。

## 命令速查

| 分类 | 命令 |
|---|---|
| 状态 | `plt status` · `plt ping` |
| 导航 | `plt goto <url>` · `plt back` · `plt forward` · `plt reload` |
| 交互 | `plt click <css>` · `plt click-text <text>` · `plt fill <css> <value>` · `plt type <css> <text>` · `plt press <key>` · `plt hover <css>` · `plt select <css> --value <v>` |
| 视图 | `plt scroll <up\|down\|top\|bottom\|amount>` · `plt screenshot --path out.png` |
| 提取 | `plt extract [--limit N]` · `plt page-info` |
| 网络 | `plt fetch <url> [--method POST] [--header "k: v"]…` · `plt search <query> [--engine google\|duckduckgo] [--page N]` |
| 标签页 | `plt tabs` · `plt tab <id>` · `plt tab-new <url>` · `plt tab-close [id]` |
| 会话/运维 | `plt session list\|new\|use\|close\|mode` · `plt logs [--follow]` · `plt approve <id>` · `plt deny <id>` |

全局选项：`--server <url>`、`--json`、`--timeout <ms>`、`--session <id>`。

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
plt extract --limit 3000
plt scroll down && plt extract --limit 3000

# 带登录态的 API 请求（在已登录站点页面执行）
plt goto https://github.com
plt fetch https://api.github.com/user --header "Accept: application/json"
```

## 人工审批（HITL）

```bash
plt session mode <id> --mode ask    # 该 session 进入 ask 模式（默认 auto）
plt click-text "Delete"             # 写操作挂起，等待批准
# 批准：扩展 popup 的批准队列点 ✔/✖，或
#       plt approve <requestId> / plt deny <requestId>
```

- 只读命令（extract/tabs/page-info…）永不挂起。
- 拒绝或超时（60s）默认不执行（fail-closed）。
- 恢复：`plt session mode <id> --mode auto`。

## 服务端配置（环境变量）

| 变量 | 默认 | 说明 |
|---|---|---|
| `PARKINGLOT_PORT` | 8787 | 监听端口 |
| `PARKINGLOT_BIND` | 127.0.0.1 | 仅回环（勿改 0.0.0.0） |
| `PARKINGLOT_TOKEN` | 自动生成（`~/.parkinglot/token`） | 扩展配对 token |
| `PARKINGLOT_ALLOWED_HOSTS` | 空（全部） | 可选域名白名单 |
| `PARKINGLOT_DISABLED_COMMANDS` | `eval` | 禁用命令列表 |
| `PARKINGLOT_ENABLE_EVAL` | 0 | 显式开启 eval |

## 安全须知

- server 只绑 `127.0.0.1`，扩展连接需 token —— token 是密钥，勿外泄。
- 扩展需要 `<all_urls>` 权限以在任意页面执行命令；请只在你信任的机器/环境使用。
- `eval` 默认禁用；`search`/`fetch` 等访问第三方站点受其条款与风控约束，请自行评估（详见[常见问题](/parkinglot/faq)与[隐私政策](/privacy)）。
