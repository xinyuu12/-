# 🧠 艾宾浩斯记忆助手

基于**艾宾浩斯遗忘曲线**的间隔复习工具，帮助你在最佳时间点复习学习内容，用科学的方法提升记忆效率。

> 单文件 HTML 应用，无需安装，打开即用。数据存储在浏览器本地，不会上传到任何服务器。

---

## ✨ 功能特性

### 📊 仪表盘
- 今日复习任务一览，逾期任务标红提醒
- 一键勾选完成复习，支持撤销
- 连续打卡天数统计
- 复习完成率进度条
- **平均熟练度**概览

### 🤖 AI 教练
- 粘贴学习内容，AI 自动分析内容类型与难度
- 智能推荐个性化复习间隔（基于艾宾浩斯曲线）
- 提供实用记忆策略建议
- 支持一键导入学习库
- 支持 **Claude / OpenAI / DeepSeek / 自定义 API**

### 📝 内容管理
- 添加、编辑、删除学习内容
- 每条内容支持：标题、详情、分类、重要性（1-5⭐）、**熟练度（0-10）**
- 按标题搜索、按分类 / 来源筛选
- **批量导入**：支持编号列表、换行分割、逗号分割、自定义分隔符

### 🎯 熟练度标注
- 每条学习内容可标注 0-10 分熟练度
- 颜色分级：🔴 0-3 生疏 · 🟡 4-6 一般 · 🟢 7-10 熟练
- 内容列表、复习列表、日历视图均显示熟练度进度条
- 统计分析页提供熟练度分布柱状图
- 仪表盘展示平均熟练度，统计页展示已掌握数量（≥8 分）

### 📅 日历视图
- 月视图日历，标注有复习任务的日期
- 点击日期查看当天复习详情
- 逾期任务红色高亮

### 📈 统计分析
- 遗忘曲线对比图（自然遗忘 vs 有复习）
- 复习完成情况饼图
- 熟练度分布柱状图
- 按分类统计内容数量

### ⚙️ 设置
- AI API 配置（支持 Claude / OpenAI / DeepSeek / 自定义）
- API 连接测试（含 file:// 协议提示）
- 分类管理（自定义添加、删除、恢复默认）
- 默认复习间隔自定义
- 数据导出 / 导入（JSON 格式）

---

## 🚀 快速开始

### 方式一：直接打开（部分功能受限）
直接用浏览器打开 `index.html`。但 AI 教练功能可能因 `file://` 协议 CORS 限制无法使用。

### 方式二：本地服务器（推荐）

```bash
# 进入项目目录
cd 艾宾浩斯记忆曲线

# Python（任选一种）
python -m http.server 8080

# 或 Node.js
npx http-server -p 8080

# 或 npx
npx serve .
```

然后访问 `http://localhost:8080`。

---

## 🤖 AI API 配置

### Claude API
| 设置项 | 值 |
|--------|-----|
| API 地址 | `https://api.anthropic.com/v1/messages` |
| 模型 | `claude-sonnet-5-20251001` |
| 获取 Key | [console.anthropic.com](https://console.anthropic.com) |

### OpenAI API
| 设置项 | 值 |
|--------|-----|
| API 地址 | `https://api.openai.com/v1/chat/completions` |
| 模型 | `gpt-4o` |
| 获取 Key | [platform.openai.com](https://platform.openai.com) |

### DeepSeek API
| 设置项 | 值 |
|--------|-----|
| API 地址 | `https://api.deepseek.com/chat/completions` |
| 模型 | `deepseek-chat` |
| 获取 Key | [platform.deepseek.com](https://platform.deepseek.com) |

> ⚠️ 在国内使用 Claude/OpenAI 官方 API 时可能需要代理或中转地址。API Key 仅存储在浏览器本地 localStorage，不会上传到任何第三方服务器。

---

## 📖 使用指南

### 添加学习内容
1. 点击「添加内容」按钮
2. 填写标题、内容详情
3. 选择分类，设置重要性（1-5⭐）和熟练度（0-10）
4. 可选：自定义复习间隔（小时，逗号分隔）

### 日常复习
1. 打开仪表盘查看今日复习任务
2. 点击圆形复选框完成复习
3. **可编辑熟练度**：完成复习后点击 📝 编辑按钮，调整熟练度分数

### 批量导入
1. 点击「批量导入」按钮
2. 粘贴内容列表（支持编号、换行、逗号等格式）
3. 预览分割结果，确认后导入

### 使用 AI 教练
1. 进入「AI 教练」页面
2. 粘贴你要记忆的内容
3. AI 会分析内容、给出复习方案和记忆策略
4. 点击「一键导入」保存到学习库

---

## 🗂️ 数据结构

每条学习内容存储以下字段：

```json
{
  "id": "唯一标识",
  "title": "标题",
  "body": "内容详情",
  "category": "分类",
  "importance": 3,
  "proficiency": 5,
  "intervals": [0.083, 0.5, 12, 24, 48, 96, 168, 360],
  "source": "manual | ai",
  "aiAdvice": null,
  "createdAt": "2026-08-05T00:00:00.000Z",
  "reviewHistory": [
    {"round": 1, "status": "completed", "completedDate": "2026-08-05T..."}
  ]
}
```

---

## 🧪 技术栈

- **HTML5 + CSS3 + Vanilla JS** — 单文件应用，零依赖（除 Chart.js CDN）
- **Chart.js 4.4** — 数据可视化图表
- **localStorage** — 浏览器本地存储
- **Fetch API** — AI API 调用（Claude / OpenAI 兼容格式）

---

## 🔒 隐私说明

- 所有学习数据存储在**浏览器本地 localStorage**
- 数据**不会上传**到任何服务器
- AI API 调用仅在用户主动触发时发生，仅发送用户输入的内容
- API Key 存储在本地浏览器，不会泄露

---

## 📄 许可

MIT License — 自由使用、修改和分发。
