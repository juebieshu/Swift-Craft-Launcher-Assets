# Swift Craft Launcher Assets

这是一个整合了 Swift Craft Launcher 所有相关资源的统一仓库。

## 仓库结构

本仓库整合了以下子项目：

### 📚 help/
**Swift-Craft-Launcher-Help** - macOS 应用帮助文档
- 包含多语言帮助文档（英文、简体中文、繁体中文）
- macOS Help Book 格式的帮助文档资源
- 目录结构：`SwiftCraftLauncher.help/Contents/Resources/`

#### 帮助文档编写指南

帮助文档遵循 macOS Help Book 格式，使用特定的 HTML 结构和 CSS 类来确保在 macOS 帮助查看器中正确显示。

##### 基本 HTML 结构

每个帮助文档页面必须遵循以下基本结构：

```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>页面标题</title>
    <meta name="description" content="页面描述">
    <meta name="keywords" content="关键词1, 关键词2">
    <meta content="light dark" name="color-scheme">
    <link media="all" href="../css/app.css" type="text/css" rel="stylesheet">
</head>
<body dir="ltr" id="页面id" class="AppleTopic apd-topic dark-mode-enabled" data-istaskopen="true" data-designversion="2">
    <a name="页面id"></a>
    <!-- 页面内容 -->
</body>
</html>
```

**关键属性说明：**
- `lang`: 语言代码（`en`、`zh-Hans`、`zh-Hant` 等）
- `dir`: 文本方向（`ltr` 从左到右，`rtl` 从右到左）
- `id`: 页面唯一标识符，与 `<a name>` 保持一致
- `class`: 必须包含 `AppleTopic apd-topic dark-mode-enabled`
- `data-istaskopen`: 任务折叠状态（`true` 展开，`false` 折叠）
- `data-designversion`: 设计版本（`1` 或 `2`，推荐使用 `2`）

##### 页面元素

###### 1. 主题图标 (Topic Icon)

在页面顶部显示应用图标：

```html
<figure class="topicIcon">
    <img src="图标URL" alt="" height="30" width="30">
</figure>
```

###### 2. 主标题 (H1)

```html
<h1>主标题</h1>
```

带样式的副标题：

```html
<h1 class="Name" style="margin-top: 0.8em;">副标题</h1>
```

###### 3. 段落 (Paragraph)

普通段落：

```html
<p>段落内容</p>
```

带底部边框的段落（常用于章节介绍）：

```html
<p style="border-bottom: 1px solid var(--border-color); padding-bottom: 1em;">介绍性文字</p>
```

###### 4. 任务步骤 (Task)

用于展示操作步骤，支持折叠/展开：

```html
<div id="step-id" class="Task">
    <h2 aria-controls="aria-step-id" class="Name">步骤标题</h2>
    <div class="TaskBody" role="region" aria-hidden="false" id="aria-step-id">
        <p>步骤说明文字</p>
        <figure>
            <img src="图片URL" alt="图片描述">
        </figure>
    </div>
</div>
```

**关键属性：**
- `id`: 任务唯一标识符
- `aria-controls`: 指向对应的 `TaskBody` 的 `id`（格式：`aria-{step-id}`）
- `aria-hidden`: `false` 表示可见，`true` 表示隐藏
- `role="region"`: 语义化标记

**多个任务连续显示时，会自动合并边框，无需额外处理。**

###### 5. 图片 (Figure)

```html
<figure>
    <img src="图片URL" alt="图片描述">
</figure>
```

图片应使用完整的 URL 地址（推荐使用 GitHub raw 链接）。

###### 6. 警告框 (Alert)

用于显示重要提示、注意事项等：

```html
<div class="Alert">
    <p class="Important"><em>Important:</em> 重要提示内容</p>
</div>
```

**提示类型：**
- `Important`: 重要提示（红色强调）
- `Note`: 注意事项（蓝色）
- `Warning`: 警告信息
- `Caution`: 谨慎提示

示例：

```html
<!-- 重要提示 -->
<div class="Alert">
    <p class="Important"><em>Important:</em> 这是重要提示</p>
</div>

<!-- 注意事项 -->
<div class="Alert">
    <p class="Note"><em>Note:</em> 这是注意事项</p>
</div>
```

###### 7. 列表 (Lists)

无序列表：

```html
<ul>
    <li><p>列表项 1</p></li>
    <li><p>列表项 2</p></li>
</ul>
```

有序列表：

```html
<ol>
    <li><p>步骤 1</p></li>
    <li><p>步骤 2</p></li>
</ol>
```

带强调的列表项：

```html
<ul>
    <li><p><strong>关键词</strong>: 说明文字</p></li>
</ul>
```

###### 8. 代码 (Code)

行内代码：

```html
<code>代码内容</code>
```

代码块：

```html
<code class="CodeLine">单行代码</code>
```

###### 9. 导航链接 (Navigation Links)

返回索引页：

```html
<div class="LinkUniversal">
    <a href="index.html#index" class="xRef AppleTopic">← Back to Index</a>
</div>
```

##### CSS 类和样式

###### 主要 CSS 类

- `.AppleTopic`: 主题容器类
- `.apd-topic`: 帮助文档主题类
- `.dark-mode-enabled`: 启用深色模式支持
- `.Task`: 任务/步骤容器
- `.TaskBody`: 任务内容区域
- `.Alert`: 警告/提示框容器
- `.Name`: 标题样式类
- `.LinkUniversal`: 导航链接容器
- `.topicIcon`: 主题图标容器

###### 常用内联样式

- `margin-top: 0.8em`: 用于副标题的顶部间距
- `border-bottom: 1px solid var(--border-color)`: 底部边框
- `padding-bottom: 1em`: 底部内边距

##### 最佳实践

1. **文件命名**
   - 使用小写字母和连字符：`add-game.html`、`edit-skins.html`
   - 保持简洁且具有描述性

2. **ID 命名**
   - 使用连字符分隔：`step-1`、`mod-step1`、`skin-step2`
   - 保持唯一性和一致性

3. **图片使用**
   - 使用完整的 URL（推荐 GitHub raw 链接）
   - 提供有意义的 `alt` 属性
   - 图片应存储在 `imagebed/` 目录下，按功能分类

4. **多语言支持**
   - 每个语言版本放在对应的 `.lproj` 目录下
   - 保持文件结构和命名一致
   - 翻译时保持 HTML 结构不变

5. **可访问性**
   - 正确使用 `aria-controls` 和 `aria-hidden`
   - 为图片提供 `alt` 文本
   - 使用语义化的 HTML 标签

6. **内容组织**
   - 使用 `h1` 作为主标题
   - 使用 `h1.Name` 作为章节标题
   - 使用 `Task` 组织操作步骤
   - 在适当位置使用 `Alert` 显示重要信息

##### 示例：完整页面结构

```html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Add Game</title>
    <meta name="description" content="Learn how to add and install Minecraft games">
    <meta name="keywords" content="add game, install minecraft">
    <meta content="light dark" name="color-scheme">
    <link media="all" href="../css/app.css" type="text/css" rel="stylesheet">
</head>
<body dir="ltr" id="addgame" class="AppleTopic apd-topic dark-mode-enabled" data-istaskopen="true" data-designversion="2">
    <a name="addgame"></a>
    <figure class="topicIcon">
        <img src="图标URL" alt="" height="30" width="30">
    </figure>
    <h1>Add Game</h1>
    <p style="border-bottom: 1px solid var(--border-color); padding-bottom: 1em;">
        介绍性文字
    </p>
    
    <h1 class="Name" style="margin-top: 0.8em;">Install Game</h1>
    
    <div id="step1" class="Task">
        <h2 aria-controls="aria-step1" class="Name">Step 1: Title</h2>
        <div class="TaskBody" role="region" aria-hidden="false" id="aria-step1">
            <p>步骤说明</p>
            <figure>
                <img src="图片URL" alt="图片描述">
            </figure>
        </div>
    </div>
    
    <div class="Alert">
        <p class="Note"><em>Note:</em> 注意事项</p>
    </div>
    
    <div class="LinkUniversal">
        <a href="index.html#index" class="xRef AppleTopic">← Back to Index</a>
    </div>
</body>
</html>
```

##### 目录结构

```
help/SwiftCraftLauncher.help/Contents/Resources/
├── css/
│   └── app.css                    # 样式文件
├── en.lproj/                      # 英文版本
│   ├── index.html
│   ├── addgame.html
│   └── ...
├── zh-Hans.lproj/                 # 简体中文版本
│   ├── index.html
│   ├── addgame.html
│   └── ...
└── zh-Hant.lproj/                 # 繁体中文版本
    ├── index.html
    ├── addgame.html
    └── ...
```

##### 参考文件

查看现有帮助文档作为参考：
- `help/SwiftCraftLauncher.help/Contents/Resources/en.lproj/addgame.html` - 简单页面示例
- `help/SwiftCraftLauncher.help/Contents/Resources/en.lproj/addresources.html` - 复杂页面示例
- `help/SwiftCraftLauncher.help/Contents/Resources/en.lproj/settings.html` - 设置页面示例

### 📰 news/
**Swift-Craft-Launcher-News** - 版本公告

基于 GitHub Pages + GitHub Actions 的静态公告 API。

#### 使用方法

**添加公告**

在 `news/` 目录下创建 JSON 文件，文件名使用版本号格式：`[version].json`

例如：`0.3.1-beta.json`、`1.0.0.json`

JSON 格式（支持22种语言）：
```json
{
  "en": {
    "title": "Important Notice",
    "content": "Content",
    "author": "Swift Craft Launcher Team"
  },
  "zh-Hans": {
    "title": "重要通知",
    "content": "内容",
    "author": "Swift Craft Launcher 团队"
  },
  "es": {
    "title": "Aviso importante",
    "content": "Contenido",
    "author": "Equipo Swift Craft Launcher"
  }
}
```

**API 端点**

`/api/announcements/[version]/[lang].json`

示例：
- `/api/announcements/0.3.1-beta/en.json`
- `/api/announcements/0.3.1-beta/zh-Hans.json`

**使用函数**

```javascript
const { getAnnouncement } = require('./scripts/generate-api.js');
const result = getAnnouncement('0.3.1-beta', 'en');
```

**生成静态文件**

```bash
node scripts/generate-api.js
```

#### 支持的22种语言

ar, da, de, en, es, fi, fr, hi, it, ja, ko, nb, nl, pl, pt, ru, sv, th, tr, vi, zh-Hans, zh-Hant

### 👥 contributors/
**Swift-Craft-Launcher-Contributors** - 贡献者信息
- 包含贡献者列表和致谢信息
- JSON 格式的数据文件

### 🖼️ imagebed/
**Swift-Craft-Launcher-ImageBed** - 图床
- 用于存储 macOS 应用帮助文档的图片资源
- 按功能模块分类存储（注册、添加游戏、添加资源、设置、编辑皮肤等）

### 🌐 web/
**Swift-Craft-Launcher-Web** - 前端代码
- 项目官网前端代码
- 包含多语言支持（英文、简体中文、繁体中文）
- 静态网站资源

## 原始仓库

- [Swift-Craft-Launcher-Help](https://github.com/suhang12332/Swift-Craft-Launcher-Help)
- [Swift-Craft-Launcher-News](https://github.com/suhang12332/Swift-Craft-Launcher-News)
- [Swift-Craft-Launcher-Contributors](https://github.com/suhang12332/Swift-Craft-Launcher-Contributors)
- [Swift-Craft-Launcher-HelpBook](https://github.com/suhang12332/Swift-Craft-Launcher-HelpBook)
- [swift-craft-launcher-web.github.io](https://github.com/suhang12332/swift-craft-launcher-web.github.io)

## 使用说明

各个子目录保持原有的结构和功能，可以独立使用。整合后的仓库便于统一管理和维护所有相关资源。

