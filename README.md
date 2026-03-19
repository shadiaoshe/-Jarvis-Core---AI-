# 🤖 Jarvis Core - 桌面级全能 AI 智能体 (Autonomous Agent)

![Python Version](https://img.shields.io/badge/Python-3.8%2B-blue)
![PyQt6](https://img.shields.io/badge/UI-PyQt6-green)
![OpenAI](https://img.shields.io/badge/AI-OpenAI%20Vision-orange)
![License](https://img.shields.io/badge/License-MIT-brightgreen)

Jarvis Core 是一个基于 Python 和大语言模型视觉能力（Vision）构建的 **真·桌面级自主智能体**。
它不仅仅是一个聊天框，而是一双可以**“看见”**你的屏幕、一双可以**“操控”**你键鼠的虚拟赛博手。通过高度集成的 RPA（机器人流程自动化）技术，它可以帮你静默装软件、自动回微信、甚至在网格坐标系下精准点击任意 UI 按钮。

---

## ✨ 核心特性 (Key Features)

- 👁️ **视觉网格定位 (Visual GUI Navigation)**
  - 按下 `Alt+V`，程序会在后台为当前屏幕附魔一层 `10x10` 的红色坐标网格。
  - AI 通过分析网格坐标，能够直接调用物理鼠标，精准点击屏幕上**任何不支持接口的第三方软件按钮**。
- 🛸 **全自动后台巡航 (Auto-Pilot)**
  - 开启自动巡航后，程序每隔 30 分钟在后台静默截屏并进行视觉分析。
  - 自动识别微信/钉钉的新消息，理解语境并**自动操控键鼠回复**（自动强制添加 `【AI自动回复】` 前缀防社死）。
  - 每次巡航生成“幽灵观察报告”，无事发生时不消耗多余 Token 记忆。
- 📦 **软件静默管家 (Winget Integration)**
  - 直接对 AI 说：“帮我安装 Chrome” 或 “卸载百度网盘”，AI 将自动调用 Windows 底层 `winget` 完成操作。
- 🐍 **动态代码沙盒 (Dynamic Python Sandbox)**
  - 遇到没有内置工具的复杂需求（如：批量重命名文件、爬取网页），AI 会**当场编写 Python 代码并执行**，直接返回结果。
- 🎨 **沉浸式亚克力 UI (Glassmorphism Design)**
  - 基于 PyQt6 打造的现代暗黑/半透明磨砂 UI。
  - 支持完全自定义背景图 (`bg.jpg`) 与专属系统托盘图标 (`logo.ico`)，优雅隐匿于桌面。

---

## 🛠️ 安装与配置 (Installation)

### 1. 克隆项目 & 安装依赖

确保你的电脑已安装 Python 3.8+，然后在终端中运行以下命令安装必要的依赖库：

```bash
pip install openai PyQt6 mss pyautogui screen-brightness-control pygetwindow pillow markdown pygments keyboard
```

### 2. 核心配置准备

在项目根目录下，你需要准备以下三个核心要件：
1. **API Key**：打开 `jarvis.py`，在顶部找到 `API_KEY = "sk-xxx"`，将其替换为你的大模型 API 密钥（推荐使用支持 Function Calling 和 Vision 的 GPT-4o / GPT-5 系列模型）。
2. **背景图片 (可选)**：在同级目录下放置一张名为 `bg.jpg` 的图片。
3. **软件图标 (可选)**：在同级目录下放置一个名为 `logo.ico` 的图标文件。

---

## 🚀 快速上手 (Usage)

直接在终端运行脚本即可唤醒 Jarvis：

```bash
python jarvis.py
```

### ⌨️ 全局快捷键
* `Alt + Space`：一键呼出 / 隐藏 Jarvis 核心面板。
* `Alt + V`：截取当前屏幕，并带上视觉网格发给 AI 分析。
* `Esc`：快速隐藏面板。

### 💬 魔法指令示例 (Prompts)
你可以尝试对它说：
* *"帮我看看屏幕上这个 Python 报错是什么意思？"* (配合 `Alt+V`)
* *"帮我点击屏幕右上角那个红色的关闭按钮。"* (配合 `Alt+V`)
* *"帮我给微信名为【老板】的人发消息，说：收到，马上处理。"*
* *"帮我把电脑系统音量调小一点，然后屏幕变暗一点。"*
* *"帮我扫描一下桌面上都有什么文件？"*

---

## 📦 打包为独立软件 (Build EXE)

如果你想把它做成一个独立的 `.exe` 桌面软件，设置为开机自启或分享给朋友，请使用 PyInstaller 一键打包。

1. 安装打包工具：
```bash
pip install pyinstaller
```
2. 在项目根目录执行以下终极神谕（包含隐藏控制台、请求管理员权限、注入双图标、打包背景图）：
```bash
pyinstaller -F -w --uac-admin --icon="logo.ico" --add-data "bg.jpg;." --add-data "logo.ico;." jarvis.py
```
*(注：Mac/Linux 用户请将打包命令中的分号 `;` 替换为冒号 `:`)*

打包完成后，前往 `dist` 文件夹即可获取 `jarvis.exe`。

---

## ⚠️ 注意事项与免责声明

1. **防封号建议**：自动回复微信依赖模拟键鼠（RPA），代码中已加入**拟人化随机延迟**。但请勿设置过高频率的自动巡航，以免触发第三方通讯软件的风控。
2. **锁屏限制**：由于 Windows 安全机制，当使用 `Win + L` 锁屏时，系统的 GUI 渲染和物理键鼠会被阻断，此时截屏和鼠标控制功能将失效。建议使用“关闭显示器电源”或“物理显卡欺骗器”进行纯后台挂机。
3. **API 消耗**：开启“自动巡航”功能会定期调用 Vision 模型，请关注您的 API Token 余额。

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
