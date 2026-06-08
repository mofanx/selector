# Selector

选择器 - 可视化元素选择器

在网页上指向任意元素，告诉 AI 需要修改什么。

一个书签工具，让你可以在任何网页上可视化选择元素、添加指令，并复制结构化提示 — 粘贴到 Claude Code、Codex、Cursor 或任何 AI 编程助手中。

[English](README.md)

## 安装

1. 访问 **[安装页面](https://oil-oil.github.io/selector/)**
2. 将 **Selector** 按钮拖到书签栏（只需一次）
3. 完成

## 使用方法

打开任意网页，点击 **Selector** 书签。

| 操作 | 功能 |
|---|---|
| **点击** | 选择元素 |
| **Shift + 点击** | 多选元素 |
| **拖拽** | 框选多个元素 |
| **↑ / ↓** | 导航到父/子元素 |
| **← / →** | 导航到上/下一个兄弟元素 |
| **✎ 按钮** | 添加元素指令 |
| **⌘C** | 复制提示到剪贴板 |
| **⌘Z** | 撤销上次选择变更 |
| **Space** | 暂停/恢复选择 |
| **Esc** | 清除选择 |

复制的内容包含元素元数据（标签、选择器、文本、React 组件信息）以及你添加的元素指令。

## 功能特性

### 元素选择
- 点击选择页面上任何可见元素
- Shift+点击多选
- 拖拽框选多个元素
- 方向键导航 DOM 层级
- 通过注解按钮添加元素级指令

### 智能元数据
- 完整路径的 CSS 选择器
- React 组件名称（开发模式）
- 源文件引用（React 开发模式）
- 文本内容和 HTML 片段
- 数据属性

### 高级支持 (v2.0)
- **iframe 支持** - 可选择同源 iframe 内元素（📄 标识）
- **Shadow DOM 支持** - 可选择 Shadow DOM 内元素（🔲 标识）
- **动态检测** - 自动检测并绑定动态添加的 iframe
- **自动修复** - iframe 内容变化时自动修复事件监听器

## 输出示例

```
Page: /dashboard

1. .hero-title <h1>
   selector: body > main > section > h1
   source: src/components/Hero.tsx:12
   react: Layout › Hero
   text: "欢迎使用仪表板"
   html: <h1 class="hero-title">欢迎使用仪表板</h1>
   instruction: 将此标题改为红色并放大

2. .sidebar-btn <button> 📄 https://example.com/preview
   selector: iframe[preview] > button.sidebar-btn
   text: "点击我"
   html: <button class="sidebar-btn">点击我</button>

3. .custom-element <div> 🔲 shadow:my-component
   selector: shadow:my-component > .custom-element
   text: "Shadow DOM 内容"
```

## 工作原理

书签工具会将 `editor.css` + `editor.js` 注入到当前页面。所有操作都在客户端运行 — 不会发送任何数据。代码在安装时被打包到书签中，之后可以离线使用。

### iframe 支持
工具自动检测同源 iframe 并向其文档注入事件监听器。iframe 内的元素用紫色边框标识，输出中标记为 📄。

### Shadow DOM 支持
Shadow DOM 根内的元素也可选择。它们显示为绿色边框，输出中标记为 🔲。

### 跨域限制
由于浏览器安全策略，无法选择跨域 iframe 内的元素。这些 iframe 会被自动检测并跳过。

## 开发

```bash
git clone https://github.com/oil-oil/selector.git
cd selector
# 编辑 assets/editor.js 和 assets/editor.css
# 本地测试: python -m http.server 8080
# 然后访问 http://localhost:8080
# 推送到 main 分支 — GitHub Pages 自动部署
```

## 许可证

MIT
