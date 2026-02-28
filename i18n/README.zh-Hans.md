[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


<a name="readme-top"></a>


<br />
<div align="center">

<h3 align="center">向 Aura 打个招呼 👋</h3>

<p align="center">
Aura 是一款针对低延迟响应优化的智能语音助手。它使用 Vercel Edge Functions、Whisper 语音识别、GPT-4o，以及 ElevenLabs TTS 流式合成。
<br />
<br />
<a href="https://voice.julianschoen.co">查看演示</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=">报告 Bug</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=">功能建议</a>
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

- [概览](#概览)
- [功能](#功能)
- [演示](#演示)
- [项目动机](#项目动机)
- [关于延迟与用户体验的思考](#关于延迟与用户体验的思考)
- [架构](#架构)
- [项目结构](#项目结构)
- [前置要求](#前置要求)
- [安装](#安装)
- [配置](#配置)
- [使用方式](#使用方式)
- [API 示例](#api-示例)
- [开发说明](#开发说明)
- [故障排查](#故障排查)
- [路线图](#路线图)
- [贡献](#贡献)
- [联系方式](#联系方式)
- [免责声明](#免责声明)
- [许可证](#许可证)

## 概览

Aura 是一个基于浏览器、类似 Siri 的语音助手，使用 Next.js（App Router）和 TypeScript 构建。

### 快速了解

| 领域 | 说明 |
| --- | --- |
| 主要目标 | 在 Web 上实现快速、实用、低延迟的语音交互 |
| 运行模型 | 浏览器采集 + 服务端 API 路由 + Edge 对话端点 |
| 语音转文本 | OpenAI Whisper（`whisper-1`） |
| 助手模型 | OpenAI GPT-4o |
| 文本转语音 | 浏览器端 ElevenLabs 流式播放 |

交互流程如下：

1. 在浏览器中采集麦克风音频。
2. 使用 OpenAI Whisper（`whisper-1`）转写语音。
3. 使用 OpenAI GPT-4o 生成简洁回答。
4. 使用 ElevenLabs 将合成音频流式返回给用户。

项目围绕低延迟的实用 UX 进行优化，并在助手“监听中”或“思考中”时提供可视化反馈。

## 功能

✅ 浏览器内的 Siri 风格语音助手  
✅ 针对低延迟响应优化  
✅ 基于 OpenAI、Whisper 语音识别和 ElevenLabs 构建

更多实现细节：

- 使用 Next.js 13 App Router 与 TypeScript。
- Edge Runtime 对话端点（`/api/chat`）。
- 基于 Toast 的交互反馈（麦克风权限、监听中、思考中）。
- 带动画的助手按钮与流式 TTS 播放。
- 可选 OpenAI Base URL 覆盖（适用于代理/自托管网关）。

## 演示

你可以在这里体验 Aura：[https://voice.julianschoen.co](https://voice.julianschoen.co)

## 项目动机

语音助手已成为日常生活的重要组成部分：手机、汽车、家庭等场景都在使用。将这种体验以良好响应速度带到 Web 端，过去一直不容易。

直到最近，Web 语音助手的主要问题仍是延迟。把音频发送到服务端、生成 LLM 回复、再把语音流式返回，整体耗时过长。得益于 OpenAI、ElevenLabs 与 Vercel 的近期进展，现在终于可以构建出在 Web 上足够实用的语音助手。

这个仓库希望成为想要构建自己语音助手、并理解真实实现权衡的人们的首选参考。

## 关于延迟与用户体验的思考

延迟是语音 UX 的关键因素。目前主要有三个贡献项：

- 转写耗时（Whisper 语音识别）。
- 响应生成耗时（原项目注释中提到 GPT-4o Mini）。
- 语音合成流式耗时（ElevenLabs TTS）。

根据实际测试记录，语音生成通常最耗时且最不稳定，尤其在回答较长时更明显。

一个可行的缓解策略是将回答拆分为多个片段并依次流式输出。这样用户可以更早开始收听，而其余内容仍在生成中。当前尚未实现，但这是一个很有前景的方向。

另一个关键概念是“感知等待时间”。即使总延迟固定，只要用户能立刻收到反馈，通常会更能接受等待。项目当前在处理期间提供“思考中”提示，以改善感知响应速度。

## 架构

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

关键文件：

- `src/components/AssistantButton/AssistantButton.tsx`：录音状态、请求编排、播放。
- `src/app/api/speechToText/route.ts`：base64 音频 -> `/tmp/input.webm` -> Whisper 转写。
- `src/app/api/chat/route.ts`：通过 OpenAI 完成对话。
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

## 前置要求

- Node.js 18+（推荐：Node.js 18.17+ 或 20 LTS，用于 Next.js 13）。
- npm（项目使用 `package-lock.json`）。
- OpenAI API key。
- ElevenLabs API key 与 voice ID。
- 可访问麦克风的桌面浏览器（当前设计下移动端 UX 有所限制）。

## 安装

1. 克隆仓库：

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. 从 [https://openai.com/](https://openai.com/) 和 [https://elevenlabs.com/](https://elevenlabs.com/) 获取 API key。

将 `.env.example` 复制为 `.env.local`，并填入你的密钥：

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL=(Optional)
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. 安装依赖：

```sh
npm install
```

4. 在本地运行应用：

```sh
npm run dev
```

5. 部署到 Vercel：

该项目兼容 Next.js 在 Vercel 上的标准部署流程。

## 配置

本项目使用的环境变量：

| 变量 | 必填 | 说明 |
| --- | --- | --- |
| `OPENAI_API_KEY` | Yes | 用于 Whisper 转写与 GPT 对话补全的 API key。 |
| `OPENAI_BASE_URL` | No | 可选：覆盖 OpenAI API base URL（代理/网关）。 |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Yes | 浏览器侧 TTS 请求使用的 ElevenLabs API key。 |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Yes | 用于 TTS 合成的 ElevenLabs voice ID。 |

说明：

- 按 Next.js 约定，`NEXT_PUBLIC_*` 变量会暴露给客户端。
- `speechToText` 当前会先将临时音频写入 `/tmp/input.webm` 再执行转写。

## 使用方式

1. 在桌面浏览器中打开应用。
2. 点击一次助手圆球并授予麦克风权限。
3. 再次点击开始录音，第三次点击停止并发送。
4. Aura 会转写你的输入、生成回复，然后播放合成语音。

本地脚本：

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## API 示例

以下示例有助于调试本地 API 路由。

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

期望响应结构：

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

期望响应结构：

```json
"Assistant response text"
```

## 开发说明

- 对话路由配置为 Edge Runtime（`export const runtime = "edge"`）。
- Whisper 路由在服务端运行，并依赖文件系统进行临时存储。
- 当前 UI 在移动端提供降级提示，而不是完整交互。
- 使用 Toast 通知展示权限/监听中/思考中状态。
- 当前提示词约束为简洁回答（`Your answer has to be as consise as possible.`）。

## 故障排查

### 麦克风权限提示未出现

- 确认浏览器已允许 `localhost` 访问麦克风。
- 在非 localhost 域名下测试时请使用 HTTPS。

### 没有音频播放

- 检查 `NEXT_PUBLIC_ELEVENLABS_API_KEY` 与 `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`。
- 确认浏览器自动播放/AudioContext 限制（需要用户交互触发）。

### `/api/speechToText` 返回 API 500

- 确认已设置 `OPENAI_API_KEY`。
- 校验输入是否为有效的 base64 编码 `webm` 音频。

### `/api/chat` 返回 API 500

- 确认 `OPENAI_API_KEY` 和可选 `OPENAI_BASE_URL` 配置正确。
- 检查你的 OpenAI 账户是否可用 `gpt-4o` 模型。

### 延迟较高

- TTS 合成时间通常是端到端延迟中的主要部分。
- 保持提示词简洁，并考虑拆分长回复。

## 路线图

根据当前代码和注释推断的后续改进方向：

- 支持移动端优先交互（替换当前仅桌面端的限制）。
- 流式输出部分助手回复，降低感知延迟。
- 完善转写与 TTS 失败场景下的重试/错误 UX。
- 增加自动化测试与 CI 检查。
- 扩展 [`/i18n`](./i18n/) 下的多语言文档。

## 贡献

欢迎并感谢你的贡献。

- 请先阅读 [CONTRIBUTING.md](./CONTRIBUTING.md) 了解流程与要求。
- 参与前请阅读 [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)。
- Bug 或功能建议请通过 Issue 提交：
- Bug report: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- Feature request: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## 联系方式

你好！感谢你查看并使用这个库。如果你想讨论你的项目、需要指导、考虑合作，或者只是想聊聊，都欢迎联系我。

你可以发邮件到：`j.schoen@mail.com`，或在 Twitter 联系我：[ @julianschoen ](https://twitter.com/julianschoen)

如果你愿意支持一下，我有一个 Buy Me A Coffee 账户：

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

感谢支持，祝你今天愉快 👋

## 免责声明

Voice Assistant 是一个实验性应用，以“按现状（as-is）”提供，不附带任何明示或暗示担保。使用本软件即表示你同意承担与使用相关的全部风险，包括但不限于数据丢失、系统故障或其他可能出现的问题。

本项目的开发者与贡献者不对因使用本软件导致的任何损失、损害或其他后果承担责任。你需对基于 Voice Assistant 提供信息所作出的任何决定和行为负责。

请注意，使用 GPT-4 语言模型可能因 token 消耗产生较高费用。使用本项目即表示你确认需自行监控和管理 token 使用量及相关成本。强烈建议你定期检查 OpenAI API 使用情况，并设置必要的限额或告警以防止意外费用。

使用 Voice Assistant 即表示你同意赔偿、抗辩并使开发者、贡献者及任何关联方免受因你使用本软件或违反这些条款而产生的任何及所有索赔、损害、损失、责任、成本和费用（包括合理律师费）。

<!-- LICENSE -->

## 许可证

基于 MIT License 分发。详情请见 `LICENSE`。

仓库说明：当前仓库中许可证文件名为 [`LICENCE`](./LICENCE)。
