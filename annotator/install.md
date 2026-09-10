# 安装指南

选择你的浏览器并进入对应的商店页面进行安装：

- Chrome 商店：<https://chromewebstore.google.com/detail/myz-annotator/mhakfcbobhdemicjelhjjpmgibhnnplg>
- Edge 商店：<https://microsoftedge.microsoft.com/addons/detail/myz-annotator/fepakkoggnancnpcclldodfbpgobkabj>

你也可以直接在首页点击「Chrome 安装」或「Edge 安装」按钮快速进入商店。

## 开始使用

1. 安装后，固定扩展图标到工具栏以便快速使用。
2. 选中网页中的文本，浮动工具条会出现，可进行高亮、下划线、波浪线标注，或点击 📸 截取选区图片。
3. 在页面右上角的图标角标中查看当前页面标注数量。
4. 打开 Popup 或 Dashboard 管理你的收藏与标注：搜索、标签筛选、导入/导出皆可在此完成。

## Dashboard 设置（功能配置）

在 Dashboard 顶部导航点击「设置」，可看到以下配置项：

### 高亮偏好

- **视图模式**：选择高亮列表默认使用的卡片或列表视图。
- **调色板**：选择标注使用的 5 色调色板，可自定义颜色值。
- **默认样式**：设置新标注默认使用的标注样式（高亮 / 下划线 / 波浪线）。
- **默认颜色**：设置新标注默认使用的颜色。

### 外观

- **主题**：可选择「跟随系统 / 亮色 / 暗色」三种模式。

### 导入标注

- **文件导入**：支持导入 MyZ JSON、RainDrop CSV、Weava CSV、Chrome 书签 HTML 文件。
- **冲突处理**：
  - **遇到重复时跳过**
  - **遇到重复时覆盖**
  - **保留最近更新**

### 加密同步（E2EE）

加密同步使用你自己的 S3 兼容对象存储；我们不提供任何线上服务。云端仅存储密文与必要元信息，同步密钥由你输入的密码派生，我们不保存你的密码。

- 推荐：**AWS S3**、**Cloudflare R2**，或其他国内 **S3 兼容**对象存储服务。
- 填写 Endpoint / Region / Bucket / Access Key / Secret Key（可选 Session Token 与 Prefix）
- 保存设置后先测试连接，再设置同步密钥并启用同步

::: warning
同步密钥仅保存在本地且无法找回；若遗忘密码，新客户端将无法解密旧数据，需要重新全量加密并同步。
:::

## 常见问题

- 如何导出到 Markdown？在详情面板或 Dashboard 中点击复制 Markdown 即可。
- 页面是单页应用（SPA）导航后丢失标注？扩展会自动感知 URL 变化并恢复，若仍无法定位会在页面与 Popup 中提示处理。