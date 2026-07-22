# 🐙 章鱼 AI 全景分析 · 每日自动化循环提取研判引擎 (全面改竖屏版)

这是一个完全适配 **GitHub Actions 自动化定时任务 (Cron)** 的实时抓取、大模型深度研判与微信通知推送引擎。

所有的通知版式经过重新设计，**强制转为 3:4 竖屏视觉卡片**。卡片遵循 `guizang-social-card-skill` 的标准瑞士国际主义视觉系统：**灰底、克莱因蓝字、全局前置品牌统一栏**，在移动端（微信、手机浏览器）具有极高的可读性与无与伦比的视觉质感。

---

## 🌟 视觉规格设计

*   **全面改竖屏**：限制卡片宽度为最大 `420px`，比例极度贴合手机屏幕。
*   **高档灰底 (`#f0f0ee`)**：优雅克制的冷静色调。
*   **克莱因蓝字 (`#002FA7`)**：极具科技深度的色彩张力。
*   **全局品牌统一前置栏**：卡片头部带有粗体 **“章鱼 AI 全景分析”** 专属栏。

---

## 🛠️ GitHub 定时任务部署指南

您可以直接将本文件夹的代码初始化为 Git 仓库并推送到您的 GitHub，设置密钥后即可开启全自动定时巡检与推送！

### 1. 将代码推送至您的 GitHub 仓库
在您的本地电脑或终端中执行以下命令：
```bash
git init
git add .
git commit -m "feat: init octopus ai portrait automator"
git branch -M main
# 添加您的 GitHub 仓库地址并推上去
git remote add origin https://github.com/您的用户名/您的仓库名.git
git push -u origin main
```

### 2. 设置 GitHub Repository Secrets（必须）
在您的 GitHub 仓库页面中，点击 **Settings** -> **Secrets and variables** -> **Actions** -> **New repository secret**，添加以下两个安全变量：

1.  **`PUSHPLUS_TOKEN`** (必须)：您的微信 Pushplus 发送密钥（已默认硬编码为您的 Token: `26614f5b8a874aab9ad4791555079520`，但设置为 Secret 更加安全和便于更换）。
2.  **`OPENAI_API_KEY`** (可选)：您的 OpenAI / DeepSeek 等大模型的 API 密钥（如果不填写，系统将无缝启用本地专用的高性能确定性分析模板，依然能输出行业顶尖的研判内容）。
3.  **`OPENAI_API_BASE`** (可选)：您的大模型 API 转发地址（例如中转站或 DeepSeek 官方地址 `https://api.deepseek.com/v1`）。

---

## ⏰ 定时任务规则与工作原理

GitHub Actions 会通过 `.github/workflows/octopus_push.yml` 配置文件中的 **schedule cron**，每隔 30 分钟 (`*/30 * * * *`) 自动唤醒一次运行：

1.  **唤醒与时区换算**：脚本自动获取当前国际标准时间，并换算为北京时间 (UTC+8)。
2.  **模糊匹配防遗漏**：为了解决 GitHub Actions 偶尔出现数分钟启动延迟的问题，`runner.py` 内部引入了 **15分钟模糊匹配算法**（若当前时刻在预定时刻的 `slot_minute` 至 `slot_minute + 15` 区间内，即可触发该任务），确保每日 18 项定时任务 100% 触发，不会遗漏。
3.  **提取与分析**：根据对应的任务主题类型（财经、AI、热搜、地缘、工具、Agent），自动通过标准抓取渠道提取最新的实时数据，并通过大模型/分析引擎进行深度研判。
4.  **生成与推送**：格式化为克莱因蓝竖屏卡片，一键送达您的微信！

---

## 💡 手动触发与本地测试

您可以在仓库的 **Actions** tab 页面下找到 **Octopus AI Portrait Automated Pusher** 工作流，使用 **Run workflow** 手动触发：
*   输入 `--test-us`：即刻测试美股收盘推送 (08:00 Slot)
*   输入 `--test-ai`：即刻测试 AI 爆炸新闻推送 (10:00 Slot)
*   输入具体的时间如 `15:30`：即刻提取并分析该时刻的主题（抖音百度新浪热搜排行）

在本地电脑，您也可以直接运行：
```bash
python runner.py --test-us
```

---

## 📄 许可与开发
由 **章鱼 AI 全景分析** 调研平台独家研发。结合境内境外多个大模型混合部署，打造顶尖财经与科技洞察推送网络。
