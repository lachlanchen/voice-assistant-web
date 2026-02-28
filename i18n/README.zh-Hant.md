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

<h3 align="center">向 Aura 打聲招呼 👋</h3>

<p align="center">
Aura 是一款以瀏覽器為核心、類 Siri 的語音助理，並針對低延遲回應做了最佳化。它使用 Vercel Edge Functions、OpenAI Whisper 語音辨識、GPT-4o 與 ElevenLabs TTS 串流播放。
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

## 目錄

- [📌 概覽](#概覽)
- [✨ 特性](#特性)
- [🎥 演示](#演示)
- [🧠 動機](#動機)
- [⏱️ 關於延遲與使用者體驗的思考](#關於延遲與使用者體驗的思考)
- [🏗️ 架構](#架構)
- [📁 專案結構](#專案結構)
- [✅ 先決條件](#先決條件)
- [🧰 安裝](#安裝)
- [⚙️ 設定](#設定)
- [🧪 使用方式](#使用方式)
- [📦 API 範例](#api-範例)
- [🛠️ 開發說明](#開發說明)
- [🧯 疑難排解](#疑難排解)
- [🗺️ 路線圖](#路線圖)
- [❤️ Support](#%e2%9d%a4%ef%b8%8f-support)
- [🤝 貢獻](#貢獻)
- [📬 聯絡](#聯絡)
- [⚠️ 免責聲明](#免責聲明)
- [📄 授權](#授權)

## 概覽

Aura 是以 Next.js（App Router）和 TypeScript 建置的、以瀏覽器為基礎的 Siri 風格語音助理。

### 一覽

| 項目 | 說明 |
| --- | --- |
| 主要目標 | 在網頁端提供快速、實用、低延遲的語音互動 |
| 運行模式 | 瀏覽器擷取 + 伺服器 API 路由 + Edge 聊天端點 |
| 語音轉文字 | OpenAI Whisper（`whisper-1`） |
| 助理模型 | OpenAI GPT-4o |
| 文字轉語音 | 在瀏覽器端進行 ElevenLabs 串流播放 |

互動循環如下：

1. 在瀏覽器中擷取麥克風音訊。
2. 透過 OpenAI Whisper（`whisper-1`）進行語音轉錄。
3. 使用 OpenAI GPT-4o 產生精簡回答。
4. 使用 ElevenLabs 將合成音訊回傳並在使用者端播放。

本專案圍繞實用導向的低延遲使用者體驗做了最佳化，並在助理正在偵聽或思考時提供視覺回饋。

### 視覺摘要

| 階段 | 目的 |
| --- | --- |
| 🎙️ 擷取 | 瀏覽器音訊擷取 + 權限感知的介面狀態 |
| 🧠 處理 | Whisper 轉錄 + GPT-4o 回應生成 |
| 🔉 交付 | 搭配狀態回饋的 ElevenLabs 串流播放 |

## 特性

| 功能 | 意涵 |
| --- | --- |
| ✅ 類 Siri 的瀏覽器助理 | 在簡潔的網頁介面中，完成「語音輸入」到「語音輸出」的完整互動 |
| ⚡ 低延遲流程 | 最佳化擷取、轉錄、產生與播放閉環 |
| 🧠 LLM + TTS 技術堆疊 | OpenAI Whisper、GPT-4o 與 ElevenLabs 串流語音合成 |
| 🧩 可延展的應用架構 | 可透過專案層級調整，切換模型端點或語音供應商 |

補充實作細節：

| 重點 | 當前行為 |
| --- | --- |
| 框架 | 使用 TypeScript 的 Next.js 13 App Router |
| API 運行環境 | Edge runtime 聊天端點（`/api/chat`） |
| 體驗回饋 | 透過 Toast 提示麥克風權限、偵聽與思考狀態 |
| 互動介面 | 具動畫效果的助理按鈕，並搭配串流 TTS 播放 |
| 網路 | 可選用 OpenAI Base URL 覆寫，支援代理/自建 gateway |

## 演示

你可以在此測試 Aura：[https://voice.julianschoen.co](https://voice.julianschoen.co)

## 動機

語音助理已成為日常生活的一部份：手機、汽車、家庭與更多場景都在使用。過去要在網頁上提供這類體驗，且維持良好回應速度，常常不太容易。

直到最近，網頁語音助理的主要問題仍是延遲。音訊傳到伺服器、生成 LLM 回覆、再把語音串流回傳給使用者，這一整段流程時間偏長。OpenAI、ElevenLabs 與 Vercel 的最新進展，讓在網頁上建出足夠快、可實際使用的語音助理成為可能。

這個儲存庫希望成為想要自己打造語音助理者的參考據點，也幫助理解真實落地實作中的取捨。

## 關於延遲與使用者體驗的思考

延遲是好用語音 UX 最關鍵的因素。目前主要有三個主要來源：

- 轉錄時間（Whisper 語音辨識）。
- 回應生成時間（原始專案註記中的 GPT-4o Mini）。
- 語音合成串流時間（ElevenLabs TTS）。

從實務測試來看，語音生成通常最耗時，也最難預測，特別是回應較長時。

一種可行的緩解策略，是將回應切成多段並逐段串流。這樣使用者可更早開始聆聽，後續內容仍在產生中。這項功能目前尚未實作，但方向值得期待。

另一個關鍵概念是「感知等待時間」。即使總延遲不變，若使用者在等待時立刻收到回饋，容忍度通常會更高。專案目前在處理階段已加入「thinking」提示，以提升感知上的回應速度。

## 架構

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

關鍵檔案：

- `src/components/AssistantButton/AssistantButton.tsx`：錄音狀態、請求協調與播放。
- `src/app/api/speechToText/route.ts`：base64 音訊 -> `/tmp/input.webm` -> Whisper 轉錄。
- `src/app/api/chat/route.ts`：透過 OpenAI 進行聊天補全。
- `src/app/page.tsx`：桌面優先的介面與行動端回退訊息。

## 專案結構

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

## 先決條件

| 要求 | 說明 |
| --- | --- |
| Node.js | 18+（建議：Node.js 18.17+ 或 Next.js 13 對應的 20 LTS） |
| 套件管理工具 | npm（專案使用 `package-lock.json`） |
| API 存取 | OpenAI API 金鑰 |
| TTS 存取 | ElevenLabs API 金鑰與語音 ID |
| 用戶端 | 支援麥克風權限的桌面瀏覽器（目前行動端仍以桌面優先） |

## 安裝

1. 複製此儲存庫：

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. 複製環境設定樣板並編輯值：

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL="" # 可選
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. 安裝相依套件：

```sh
npm install
```

4. 本機執行：

```sh
npm run dev
```

5. 開啟應用程式：`http://localhost:3000`。

補充：若要在非本地域名測試麥克風權限，通常需要 HTTPS。

6. 部署到 Vercel：

本專案沿用標準 Next.js 部署流程。使用 Vercel 的預設匯入設定，並在專案中設定相同的環境變數。

## 設定

本專案使用的環境變數：

| 變數 | 是否必填 | 說明 |
| --- | --- | --- |
| `OPENAI_API_KEY` | 是 | 用於 Whisper 轉錄與 GPT 聊天補完的 API 金鑰。 |
| `OPENAI_BASE_URL` | 否 | OpenAI API Base URL 的可選覆寫（代理/閘道）。 |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | 是 | 在瀏覽器端 TTS 請求中使用的 ElevenLabs API 金鑰。 |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | 是 | 用於 TTS 合成的 ElevenLabs Voice ID。 |

補充說明：

- 按 Next.js 慣例，`NEXT_PUBLIC_*` 變數會暴露給客戶端。
- `speechToText` 目前在轉錄前會先將音訊寫到 `/tmp/input.webm`。

## 使用方式

1. 在桌面瀏覽器開啟應用程式。
2. 點擊一次助理圓球並授權麥克風權限。
3. 再次點擊開始錄音；第三次點擊則停止並送出。
4. Aura 會先轉錄你的輸入、再產生回應，最後播放合成語音。

本機指令：

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## API 範例

這些範例可用於本機 API 路由除錯。

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

預期回傳格式：

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

預期回傳格式：

```json
"Assistant response text"
```

## 開發說明

- Chat 路由已設定為 Edge runtime（`export const runtime = "edge"`）。
- Whisper 路由在伺服器端執行，並依賴檔案系統存取暫存空間。
- 目前 UI 在行動端只提供 fallback 提示，而非完整互動體驗。
- Toast 通知用於顯示權限、偵聽與思考狀態。
- 目前提示語要求回應儘量精簡（`Your answer has to be as concise as possible.`）。
- 執行時日誌、請求追蹤能力與串流行為目前未在 CI 中驗證（此專案未包含自動化測試套件）。

## 疑難排解

### 🎤 麥克風權限提示未出現

- 確保你的瀏覽器允許 `localhost` 的麥克風權限。
- 在非 localhost 網域測試時使用 HTTPS。

### 🔈 無音訊播放

- 檢查 `NEXT_PUBLIC_ELEVENLABS_API_KEY` 與 `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`。
- 確認瀏覽器自動播放與 AudioContext 限制（需使用者互動）。

### 📡 `/api/speechToText` 回傳 500

- 確認 `OPENAI_API_KEY` 已正確設定。
- 驗證輸入內容包含有效的 base64 編碼 `webm` 音訊。

### 📡 `/api/chat` 回傳 500

- 確認 `OPENAI_API_KEY` 與可選的 `OPENAI_BASE_URL` 設定正確。
- 檢查你的 OpenAI 帳號是否可用 `gpt-4o` 模型。

### ⏳ 高延遲

- TTS 合成時間通常是端對端延遲的主要來源。
- 保持提示詞簡潔，並考慮拆分長回應。

## 路線圖

根據目前程式碼與說明，可能的下一步改進：

- 支援行動優先互動（取代目前的桌面優先門檻）。
- 串流分段助理回應，以降低感知延遲。
- 改善轉錄與 TTS 失敗時的重試與錯誤體驗。
- 增加自動化測試與 CI 檢查。
- 擴充 [`/i18n`](./i18n/) 下的多語言文件。

## 貢獻

歡迎投稿並一同改進。

- 參考 [CONTRIBUTING.md](./CONTRIBUTING.md) 了解流程與期待。
- 參與前先閱讀 [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)。
- 若有 bug 或功能提案，請開啟 issue：
- Bug 回報：[template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- 功能建議：[template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## 聯絡

哈囉，感謝你來到並使用這個專案。如果你想討論你的專案、需要指導、考慮聘請我，或只是想聊天，我都很樂意聊聊。

你可以寄信到：`j.schoen@mail.com`，或在 Twitter 私訊我：[@julianschoen](https://twitter.com/julianschoen)

如果你想回饋支持，我有一個 Buy Me A Coffee 帳戶：

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

謝謝你，祝你有美好的一天 👋

## 免責聲明

Voice Assistant 是一個實驗性應用程式，依「現況」提供，不附帶任何明示或默示保證。使用此軟體即表示你同意自行承擔所有使用風險，包括但不限於資料遺失、系統故障或其他可能發生的問題。

本專案的開發者與貢獻者不負責因使用本軟體而造成的任何損失、損害或其他後果。你應自行對基於 Voice Assistant 所提供資訊而做出的決策與行為負全責。

請注意，使用 GPT-4 語言模型可能因 token 用量而產生高額成本。使用本專案即表示你需自行監控並管理自己的 token 使用量與相關費用。強烈建議定期檢查 OpenAI API 使用情況，並設定必要的限制或提醒，以避免意外扣款。

使用 Voice Assistant 即表示你同意賠償、辯護並使開發者、貢獻者以及任何相關方免於承擔因你使用本軟體或違反這些條款而產生的所有索賠、損害、損失、責任、費用與支出（包含合理律師費）。

<!-- LICENSE -->

## 授權

以 MIT 授權條款發佈。更多資訊請見 `LICENSE`。

專案說明：本儲存庫目前將授權檔命名為 [`LICENCE`](./LICENCE)。


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
