[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


[![LazyingArt banner](https://github.com/lachlanchen/lachlanchen/raw/main/figs/banner.png)](https://github.com/lachlanchen/lachlanchen/blob/main/figs/banner.png)

![GitHub last commit](https://img.shields.io/github/last-commit/ntegrals/aura-voice?style=for-the-badge&logo=github&logoColor=white&color=0EA5E9)
![Node.js](https://img.shields.io/badge/Node.js-18%2B-10B981?style=for-the-badge&logo=nodedotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5.1-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![GitHub stars](https://img.shields.io/github/stars/ntegrals/aura-voice?style=for-the-badge&logo=github&logoColor=white&color=F59E0B)
![Open Issues](https://img.shields.io/github/issues/ntegrals/aura-voice?style=for-the-badge&logo=github&logoColor=white&color=EF4444)

<a name="readme-top"></a>

<br />
<div align="center">

# Aura

<h3 align="center">向 Aura 打个招呼 👋</h3>

<p align="center">
Aura 是一款基于浏览器、类 Siri 的语音助手，专为低延迟回复优化。它使用 Vercel Edge Functions、OpenAI Whisper 语音识别、GPT-4o 以及 ElevenLabs TTS 流式播放。
<br />
<br />
<a href="https://voice.julianschoen.co"><img src="https://img.shields.io/badge/▶_Live_Demo-0EA5E9?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Live Demo"/></a>
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title="><img src="https://img.shields.io/badge/🐞_Report_Bug-F43F5E?style=for-the-badge&logo=github&logoColor=white" alt="Report Bug"/></a>
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title="><img src="https://img.shields.io/badge/💡_Request_Feature-22C55E?style=for-the-badge&logo=github&logoColor=white" alt="Request Feature"/></a>
</p>

<p align="center">
<a href="https://github.com/ntegrals/aura-voice"><img alt="Repo" src="https://img.shields.io/badge/GitHub-ntegrals%2Faura--voice-181717?logo=github" /></a>
<a href="https://nextjs.org/"><img alt="Next.js" src="https://img.shields.io/badge/Next.js-13.4.13-black?logo=next.js" /></a>
<a href="https://www.typescriptlang.org/"><img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-5.1-3178C6?logo=typescript&logoColor=white" /></a>
<a href="https://openai.com/"><img alt="OpenAI" src="https://img.shields.io/badge/OpenAI-GPT--4o%20%2B%20Whisper-10A37F" /></a>
<a href="https://elevenlabs.io/"><img alt="ElevenLabs" src="https://img.shields.io/badge/ElevenLabs-TTS%20Streaming-222222" /></a>
<a href="https://vercel.com/"><img alt="Vercel Edge" src="https://img.shields.io/badge/Vercel-Edge%20Runtime-000000?logo=vercel" /></a>
<a href="./LICENCE"><img alt="License" src="https://img.shields.io/badge/License-MIT-22C55E.svg" /></a>
</p>

</div>

<a href="https://github.com/ntegrals/aura-voice">
<img src=".assets//header.png" alt="Logo">
</a>

## 目录

- [📌 概览](#概览)
- [✨ 特性](#特性)
- [🎥 演示](#演示)
- [🧠 动机](#动机)
- [⏱️ 对延迟与用户体验的思考](#对延迟与用户体验的思考)
- [🏗️ 架构](#架构)
- [📁 项目结构](#项目结构)
- [✅ 先决条件](#先决条件)
- [🧰 安装](#安装)
- [⚙️ 配置](#配置)
- [🧪 使用](#使用)
- [📦 API 示例](#api-示例)
- [🛠️ 开发说明](#开发说明)
- [🧯 故障排查](#故障排查)
- [🗺️ 路线图](#路线图)
- [❤️ Support](#%e2%9d%a4%ef%b8%8f-support)
- [🤝 贡献](#贡献)
- [📬 联系](#联系)
- [⚠️ 免责声明](#免责声明)
- [📄 许可证](#许可证)

## 概览

Aura 是一个基于 Next.js（App Router）和 TypeScript 构建的、基于浏览器的 Siri 风格语音助手。

### 一览

| 领域 | 说明 |
| --- | --- |
| 主要目标 | 在网页端实现快速、实用、低延迟的语音交互 |
| 运行模型 | 浏览器录音 + 服务器 API 路由 + Edge 聊天端点 |
| 语音转文本 | OpenAI Whisper（`whisper-1`） |
| 助手模型 | OpenAI GPT-4o |
| 文本转语音 | 在浏览器端进行 ElevenLabs 流式播放 |

交互循环是：

1. 在浏览器中采集麦克风音频。
2. 通过 OpenAI Whisper（`whisper-1`）进行语音转录。
3. 使用 OpenAI GPT-4o 生成简洁回答。
4. 使用 ElevenLabs 在浏览器中回传并播放合成音频。

该项目围绕实用的低延迟体验进行优化：助手在监听或思考时会提供可视化反馈。

### 视觉摘要

| 阶段 | 目的 |
| --- | --- |
| 🎙️ 采集 | 浏览器音频采集 + 麦克风权限感知状态 |
| 🧠 处理 | Whisper 转录 + GPT-4o 回答生成 |
| 🔉 投递 | ElevenLabs 流式播放并带状态反馈 |

## 特性

| 能力 | 含义 |
| --- | --- |
| ✅ 类 Siri 的浏览器助手 | 在简洁的网页界面中完成完整的语音输入与语音输出交互 |
| ⚡ 低延迟流程 | 优化了采集、转录、生成和播放闭环 |
| 🧠 LLM + TTS 技术栈 | OpenAI Whisper、GPT-4o 与 ElevenLabs 流式语音合成 |
| 🧩 可扩展的应用架构 | 可通过项目级修改切换模型端点或语音服务提供方 |

补充实现细节：

| 关注点 | 当前行为 |
| --- | --- |
| 框架 | 使用 TypeScript 的 Next.js 13 App Router |
| API 运行时 | Edge runtime 聊天端点（`/api/chat`） |
| 体验反馈 | 通过 Toast 提示麦克风权限、监听和思考状态 |
| 交互界面 | 有动画效果的助手按钮，搭配流式 TTS 播放 |
| 网络 | 可选支持 OpenAI Base URL 覆写（适配代理/自建网关） |

## 演示

你可以在这里试用 Aura：[https://voice.julianschoen.co](https://voice.julianschoen.co)

## 动机

语音助手已经成为日常生活的一部分：手机、汽车、家庭设备等。把这种体验在网页上做到响应迅速，一直都不容易。

直到最近，网页语音助手的主要瓶颈仍然是延迟：将音频发送到服务器、生成 LLM 回复并回传语音都花费较长时间。OpenAI、ElevenLabs 与 Vercel 的最新进展让我们可以构建出在网页上足够快、足够实用的语音助手。

本仓库目标是为想要构建自己语音助手的人提供参考，并帮助理解真实落地时的取舍。

## 对延迟与用户体验的思考

延迟是良好语音 UX 的最关键因素。当前有三个主要来源：

- 转录耗时（Whisper 语音识别）。
- 回答生成耗时（原始说明中的 GPT-4o Mini）。
- 语音合成流式耗时（ElevenLabs TTS）。

从实际测试看，语音生成通常最耗时且最难预测，尤其是长回复时。

一种可能的缓解策略是把回复拆成多段并按顺序串流。这样用户可更早开始收听，而后续内容仍在生成中。这个功能尚未实现，但方向很有前景。

另一个关键概念是“感知等待时间”。即使端到端延迟不变，若用户在等待时能拿到即时反馈，容忍度通常更高。项目目前在处理阶段显示“thinking”提示，以提升感知响应性。

## 架构

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

关键文件：

- `src/components/AssistantButton/AssistantButton.tsx`：录音状态、请求编排与播放。
- `src/app/api/speechToText/route.ts`：base64 音频 -> `/tmp/input.webm` -> Whisper 转录。
- `src/app/api/chat/route.ts`：通过 OpenAI 进行聊天补全。
- `src/app/page.tsx`：桌面优先界面与移动端降级提示。

## 项目结构

```text
voice-assistant-web/
├─ README.md
├─ .env.example
├─ package.json
├─ LICENCE
├─ CONTRIBUTING.md
├─ CODE_OF_CONDUCT.md
├─ .assets/
│  ├─ header.png
│  └─ buymeacoffee.png
├─ i18n/
├─ public/
│  ├─ font2.png
│  ├─ favicon.ico
│  ├─ next.svg
│  └─ vercel.svg
└─ src/
   ├─ app/
   │  ├─ page.tsx
   │  ├─ layout.tsx
   │  ├─ globals.css
   │  ├─ button.css
   │  └─ api/
   │     ├─ chat/route.ts
   │     └─ speechToText/route.ts
   └─ components/
      └─ AssistantButton/
         └─ AssistantButton.tsx
```

## 先决条件

| 要求 | 说明 |
| --- | --- |
| Node.js | 18+（推荐：Node.js 18.17+ 或 Next.js 13 对应的 20 LTS） |
| 包管理器 | npm（项目使用 `package-lock.json`） |
| API 访问 | OpenAI API Key |
| TTS 访问 | ElevenLabs API Key 和 Voice ID |
| 客户端 | 支持麦克风权限的桌面浏览器（当前移动端仍以桌面优先） |

## 安装

1. 克隆仓库：

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. 复制环境模板并编辑变量：

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL="" # 可选
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. 安装依赖：

```sh
npm install
```

4. 本地运行：

```sh
npm run dev
```

5. 打开应用：`http://localhost:3000`。

补充假设：如果在非本地域名测试麦克风权限，通常需要 HTTPS。

6. 部署到 Vercel：

该项目遵循标准的 Next.js 部署流程。使用 Vercel 的默认导入设置，并在项目中设置同样的环境变量。

## 配置

本项目使用的环境变量：

| 变量 | 必填 | 说明 |
| --- | --- | --- |
| `OPENAI_API_KEY` | 是 | 用于 Whisper 转录与 GPT 聊天补全的 API Key。 |
| `OPENAI_BASE_URL` | 否 | OpenAI API Base URL 的可选覆盖（代理/网关）。 |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | 是 | 浏览器端 TTS 请求使用的 ElevenLabs API Key。 |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | 是 | 用于 TTS 合成的 ElevenLabs Voice ID。 |

说明：

- 按 Next.js 约定，`NEXT_PUBLIC_*` 变量会暴露给客户端。
- `speechToText` 目前会在转录前将音频先写入 `/tmp/input.webm`。

## 使用

1. 在桌面浏览器打开应用。
2. 点击助手按钮一次并授权麦克风权限。
3. 再点一次开始录音，第三次点停止并发送。
4. Aura 会转录你的输入、生成回复，再播放合成语音。

本地脚本：

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## API 示例

这些示例用于调试本地 API 路由。

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

预期返回格式：

```json
{
  "result": "transcribed text"
}
```

### `POST /api/chat`

```bash
curl -X POST http://localhost:3000/api/chat \
  -H "Content-Type: application/json" \
  -d '{"messages":[{"role":"user","content":"Hello Aura"}]}'
```

预期返回格式：

```json
"Assistant response text"
```

## 开发说明

- Chat 路由已配置为 Edge runtime（`export const runtime = "edge"`）。
- Whisper 路由在服务端运行，并依赖文件系统进行临时存储访问。
- 当前 UI 在移动端仅显示 fallback 提示，而非完整的移动交互。
- Toast 通知用于展示权限、监听和思考状态。
- 当前提示词约束要求回答尽量简洁（`Your answer has to be as concise as possible.`）。
- 运行时日志、请求可追踪性和流式行为当前在 CI 中尚未验证（仓库里暂无自动化测试）。

## 故障排查

### 🎤 麦克风权限提示未出现

- 确保浏览器允许 `localhost` 的麦克风访问。
- 在非 localhost 域名上测试时使用 HTTPS。

### 🔈 无音频播放

- 检查 `NEXT_PUBLIC_ELEVENLABS_API_KEY` 与 `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`。
- 确认浏览器自动播放和 AudioContext 限制（需要用户交互）。

### 📡 `/api/speechToText` 返回 500

- 确认 `OPENAI_API_KEY` 已设置。
- 确认输入包含有效的 base64 编码 `webm` 音频。

### 📡 `/api/chat` 返回 500

- 确认 `OPENAI_API_KEY` 与可选的 `OPENAI_BASE_URL` 正确。
- 检查你的 OpenAI 账号是否可用 `gpt-4o` 模型。

### ⏳ 高延迟

- TTS 合成时间通常是端到端延迟的主要部分。
- 保持提示词简洁，并考虑拆分长回复。

## 路线图

潜在的后续优化（基于当前代码与说明）：

- 支持移动优先交互（替换当前桌面优先门槛）。
- 流式返回分段助手回复以降低感知延迟。
- 改进转录与 TTS 失败场景的重试与错误体验。
- 增加自动化测试和 CI 检查。
- 扩展 [`/i18n`](./i18n/) 下的多语言文档。

## 贡献

欢迎投稿并参与贡献。

- 阅读 [CONTRIBUTING.md](./CONTRIBUTING.md) 了解流程和预期。
- 参与前请阅读 [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)。
- 针对 bug 或功能建议可提交 issue：
- Bug 报告：[template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- 功能请求：[template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## 联系

你好！感谢你查看并使用这个仓库。如果你想讨论你的项目、寻求指导、考虑聘请我，或者只是聊聊，我都很乐意交流。

你可以发邮件到 `j.schoen@mail.com`，也可以在 Twitter 上私信我：[@julianschoen](https://twitter.com/julianschoen)

如果你想支持我的工作，我有一个 Buy Me A Coffee 账户：

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

谢谢你，祝你今天愉快 👋

## 免责声明

Voice Assistant 是一个实验性应用程序，按“原样”提供，不附带任何明示或默示担保。使用此软件即表示你同意自行承担其使用所带来的所有风险，包括但不限于数据丢失、系统故障或其他可能出现的问题。

本项目的开发者和贡献者不承担因使用本软件而导致的任何损失、损害或其他后果的任何责任。你应对基于 Voice Assistant 提供的信息所做的任何决策和行为承担全部责任。

请注意，使用 GPT-4 语言模型可能因 token 消耗而产生较高成本。使用本项目即表示你负责监控和管理自己的 token 使用与相关费用。强烈建议定期检查 OpenAI API 的使用情况，并设置必要的额度或提醒，以避免意外扣费。

在使用 Voice Assistant 时，你同意为开发者、贡献者及任何关联方提供赔偿、辩护并使其免受任何因此产生的索赔、损害、损失、责任、成本和费用（包括合理的律师费），该等索赔源于你使用本软件或违反本条款。

<!-- LICENSE -->

## 许可证

依据 MIT 许可证发布。详情见 `LICENSE`。

仓库说明：当前仓库将许可文件命名为 [`LICENCE`](./LICENCE)。


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
