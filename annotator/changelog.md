# 更新日志

以下内容摘自扩展的变更记录，便于用户快速了解版本更新。

当前商店版本：
- [![](https://img.shields.io/chrome-web-store/v/mhakfcbobhdemicjelhjjpmgibhnnplg)](https://chromewebstore.google.com/detail/mhakfcbobhdemicjelhjjpmgibhnnplg) 
- [![](https://img.shields.io/badge/dynamic/json?label=edge%20add-on&prefix=v&query=$.version&url=https://microsoftedge.microsoft.com/addons/getproductdetailsbycrxid/fepakkoggnancnpcclldodfbpgobkabj)](https://microsoftedge.microsoft.com/addons/detail/fepakkoggnancnpcclldodfbpgobkabj)

## v0.6.3 — PDF 阅读器导航侧栏与选择修复

- PDF 阅读器新增左侧导航侧栏：可按 PDF 目录（书签）跳转章节，或按页查看标注并精确定位到标注位置；侧栏开关与标签页会记忆。
- 标注列表支持关键词搜索，可按选中文本 / 批注 / 标签过滤，也可按类型（高亮 / 保存文字）筛选。
- 修复下划线 / 波浪线会覆盖选中文字前后内容的问题。
- 修复长段落选中或高亮时，范围在文字右侧多出一截空白的问题。
- 修复从 Dashboard 跳转到阅读器打开本地 PDF 时的授权失败问题，并在必要时提供「重新授权并打开」。

## v0.6.1 — PDF 阅读与标注

- 新增内置 PDF 阅读器：显式打开本地文件或网页 PDF，默认连续滚动、缩放（50%–300%）与阅读进度记忆。
- 支持在 PDF 中选中文本进行高亮 / 保存文字、添加批注与标签；重开同一 PDF 自动还原高亮（本地按文件指纹、网页按 URL）。
- 支持 JPEG2000 / JBIG2 图片型 PDF。
- 入口：Popup 的 PDF 按钮、右键链接「在 MyZ 中打开 PDF」；网页 PDF 无 `.pdf` 后缀（如 arXiv）也可识别。
- Dashboard 显示「第 N 页」徽标，并可一键跳回阅读器对应页。
- 新建标注沿用上次使用的高亮样式与颜色；Inspector 提供显式保存按钮与状态提示。
- 说明：本地 PDF 目前仅支持 Chrome。

## v0.6.0 — 移除 AI 能力与 Dashboard 收敛

- 移除 AI 智能助理（SidePanel）及其全部相关能力：自定义 Provider、MCP Server、本地 tools、Agent Skills、向量检索（Vectoria）、自动高亮、Superpower 多 Agent 协作与 Dashboard 聊天页面。
- 移除社区导入（X / Mastodon）；导入统一为文件导入（MyZ JSON、RainDrop CSV、Weava CSV、Chrome 书签 HTML）。
- 精简扩展权限与右键菜单：移除 sidePanel 权限，右键菜单仅保留禅定模式（Zen Mode）相关项。
- Dashboard 收敛为高亮管理与设置：高亮列表、高亮查看器，以及设置（高亮偏好 / 外观 / 导入 / 同步）。

## v0.5.0 — Dashboard UI 重构与交互优化

- ThemeToggle 下拉按 effective theme 显示状态，修复 Dashboard 中下拉被面板遮挡的问题。
- 高亮卡片的类型标识与操作按钮统一改为 lucide 图标，支持 hover tooltip。
- 标签区紧凑化排列；卡片视图改为 CSS columns 瀑布流布局；摘要内容应用 prose 排版。
- Card 内批注改为上下结构，适配瀑布流卡片高度。
- 内容浮动工具条新增搜索按钮：调用浏览器搜索打开新页面搜索选中内容。

## v0.4.4 — Provider Tiering 与 Mistral SDK 接入

- 新增 mistral provider 类型，接入官方 SDK 用于模型列表、连接测试、对话、streaming 与 tool calling。
- OpenAI 兼容接口按供应商 profile 进行 request patching，收敛 Tier 1 兼容支持列表。

## v0.4.3 — OpenAI-compatible reasoning 续传修复

- 修复第三方 OpenAI-compatible 接口在 thinking mode 下的多轮对话失败问题。
- 传输层切换到官方 SDK（openai / anthropic / genai），收缩 provider 类型范围。

## v0.4.2 — Dashboard 新查看器与页面聚合

- 新增 `/highlights/:id` 查看器页面，支持同页标注连续阅读、滚动到底自动切换、上一页/下一页导航。
- Dashboard 高亮列表新增可折叠页面侧边栏，支持按网页筛选与按时间/Range 顺序查看。
- 标注内容新增 `contentType` 字段，支持 Markdown/HTML/纯文本渲染。

## v0.4.1 — Dashboard 体验升级

- Dashboard 结构升级，更清晰易用。
- 设置页面新增侧边导航，快速跳转到不同设置区域。
- 导入能力增强：支持 RainDrop CSV 和 Chrome 书签 HTML。

## v0.4.0 — Superpower 模式与多 Agent 协作

- 新增 Superpower 模式，支持多 Agent 协作式的任务流程。
- 对话侧边栏界面更清爽，信息更集中。
- 对话标题与历史列表展示优化，浏览更直观。
- 修复调色板颜色编辑无法打开的问题。

## v0.3.2 — 自动高亮与分类标注

- 新增自动高亮能力，自动生成关键内容标注。
- 关键要点发现改为独立入口，操作更便捷。
- AI 设置新增自动高亮的模型与分类样式配置。
- Popup 空状态新增“一键自动高亮”按钮。
- 高亮匹配更稳健，降低误差与重叠。

## v0.3.1 — 交互与设置稳定性

- 修复高亮点击后 Inspector 不显示的问题，并改为贴近高亮的工具条式展示（有批注则上方展示，编辑时自动关闭）。
- 调整高亮定位提示为更柔和的脉冲/光晕动画，提升夜间与马克笔模式的可见性。
- Interests 功能仅在向量检索启用且配置了模型时显示；同时清理悬浮指示器并降低指示点体积。
- 统一新增 SVG 图标到共享库，更新 Popup/SidePanel/Inspector 的设置与操作图标样式。
- 修复 AiProviderEditor 模型列表在重新排序时的误选问题，取消勾选时自动选中相邻项方便继续编辑。

## v0.3.0 — 端到端加密同步（E2EE）

- 新增加密同步（S3 兼容）：由你自行填写对象存储信息并发起同步。
- 同步密钥仅保存在本地，云端只存储密文与必要的元信息。
- 新增同步状态展示与手动同步入口（KeyId、Manifest 版本、上次同步时间等）。

## v0.2.0 — Agent Skills

- 加入 Agent Skills 能力：
  - 支持内置技能与自定义技能（Zip/文件夹导入）。
  - 支持 `@skill-name` 显式引用技能。
  - 支持“自动”模式，用选择器模型为每次输入挑选技能。
- 新增技能管理与编辑入口（Dashboard → AI 设置）。

## v0.1.5 — 集成 AI

- 加入 AI Assistant 集成：
  - 支持 AI 模型分析页面，
  - 支持发送页面上下文与 AI 对话，
  - 支持自定义 Provider 和 MCP 服务器，
  - 支持向量索引和网页内容智能发现。
- 移除 LogSeq 同步功能。
- 加入社交网络内容导入功能 - 支持 X（Twitter）、Mastodon。

## v0.1.4 — 图标统一与 SPA 修复
- 浮动工具条、Popup、Dashboard 的按钮图标全部改为自研 SVG，避免不同系统的 Emoji 渲染差异。
- 标注样式切换器恢复马克笔高亮图标，新增带下划线的字母 U 图标，三种样式一眼可辨。
- Dashboard 设置按钮增大字号并添加描边，入口更醒目。
- 修复 Twitter 等单页应用在站内跳转时高亮不会刷新问题，现在点击推文也会立即重新应用标注。

## v0.1.3 — Vue3 架构与高亮稳健性
- 迁移到 Vite + `@crxjs/vite-plugin` + Vue 3/JSX 架构。
- 重构 Popup、Dashboard、content 与 background 模块。
- 重新设计高亮 Range 序列化，修复删除旧标注导致错位的问题。
- 增加重叠检测与相关 Playwright 覆盖用例。
- 更新暗色友好调色板与导出描述同步。
- 为 SPA 导航挂钩 History API，保证页面跳转后即时刷新。
- 扩充端到端测试套件与统一图标视觉语言。

## v0.1.2 — 多样标注与纯文本收藏
- 新增「保存文字」按钮，将选中文本作为收藏保存。
- Popup/Dashboard 清晰区分类型并支持降级为纯文本。
- 三种样式：高亮、下划线、波浪线；导出包含样式描述。
- 优化文本装饰在窄行距页面的表现。

## v0.1.1 — 标注与截图增强
- 导入功能与浏览器工具栏角标。
- 定位失败标注提醒；修复多项稳定性问题。
- 截图流程优化，解决选中态截取问题。

## v0.1.0 — 初始发布
MyZ Annotator 帮助你在任意网页高亮文本、撰写批注、截图收集，并在本地管理这些资料。支持导出 JSON/Markdown 与 LogSeq 增量同步。