[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


<a name="readme-top"></a>

<br />
<div align="center">

<h3 align="center">向 Aura 打個招呼 👋</h3>

<p align="center">
Aura 是一個為低延遲回應最佳化的智慧語音助理。它使用 Vercel Edge Functions、Whisper 語音辨識、GPT-4o，以及 ElevenLabs TTS 串流。
<br />
<br />
<a href="https://voice.julianschoen.co">查看示範</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=">回報錯誤</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=">功能建議</a>
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

- [總覽](#總覽)
- [功能特色](#功能特色)
- [示範](#示範)
- [動機](#動機)
- [關於延遲與使用者體驗的想法](#關於延遲與使用者體驗的想法)
- [架構](#架構)
- [專案結構](#專案結構)
- [先決條件](#先決條件)
- [安裝](#安裝)
- [設定](#設定)
- [使用方式](#使用方式)
- [API 範例](#api-範例)
- [開發備註](#開發備註)
- [疑難排解](#疑難排解)
- [路線圖](#路線圖)
- [貢獻](#貢獻)
- [聯絡方式](#聯絡方式)
- [免責聲明](#免責聲明)
- [授權](#授權)

## 總覽

Aura 是一個在瀏覽器中運作、類似 Siri 的語音助理，使用 Next.js（App Router）與 TypeScript 建置。

### 快速看懂

| 領域 | 詳細內容 |
| --- | --- |
| 主要目標 | 在網頁上提供快速、實用、低延遲的語音互動 |
| 執行模型 | 瀏覽器錄音 + 伺服器 API routes + Edge 聊天端點 |
| 語音轉文字 | OpenAI Whisper (`whisper-1`) |
| 助理模型 | OpenAI GPT-4o |
| 文字轉語音 | 在瀏覽器端播放 ElevenLabs 串流音訊 |

互動流程如下：

1. 在瀏覽器中擷取麥克風音訊。
2. 使用 OpenAI Whisper (`whisper-1`) 進行語音轉錄。
3. 使用 OpenAI GPT-4o 產生精簡回答。
4. 使用 ElevenLabs 將合成語音串流回傳給使用者。

本專案以實際可用的低延遲 UX 為核心最佳化，助理在聆聽或思考時也會提供視覺回饋。

## 功能特色

✅ 在瀏覽器中即可使用的 Siri 風格語音助理  
✅ 為低延遲回應做過最佳化  
✅ 以 OpenAI、Whisper 語音辨識與 ElevenLabs 建構

其他實作細節：

- 使用 Next.js 13 App Router 與 TypeScript。
- Edge runtime 聊天端點（`/api/chat`）。
- 以 Toast 呈現互動回饋（麥克風權限、聆聽中、思考中）。
- 含串流 TTS 播放的助理按鈕動畫。
- 可選擇覆寫 OpenAI base URL，用於 proxy/self-hosted gateway 架構。

## 示範

你可以在此測試 Aura：[https://voice.julianschoen.co](https://voice.julianschoen.co)

## 動機

語音助理已成為日常生活不可或缺的一部分：手機、汽車、居家裝置等。要把這種體驗帶到網頁並保持良好即時性，過去一直相當困難。

直到最近，網頁語音助理的主要問題仍是延遲。把音訊送到伺服器、生成 LLM 回應，再把語音串流回來，整體流程往往過慢。OpenAI、ElevenLabs 與 Vercel 的近期進展，讓打造真正夠快、可實際使用的網頁語音助理成為可能。

此儲存庫希望成為想打造自己語音助理的人可參考的實作基地，並幫助理解真實系統中的取捨。

## 關於延遲與使用者體驗的想法

延遲是優秀語音 UX 最關鍵的因素。目前主要有三個來源：

- 轉錄時間（Whisper 語音辨識）。
- 回應生成時間（原始專案筆記中為 GPT-4o Mini）。
- 語音合成串流時間（ElevenLabs TTS）。

依照實務測試筆記，語音生成通常最耗時且最不穩定，尤其在回應較長時。

一個可行的緩解策略是將回應切成多段並依序串流。這能讓使用者更早開始聽到內容，同時其餘段落仍在生成中。此功能目前尚未實作，但方向很有潛力。

另一個關鍵概念是「感知等待時間」。即使總延遲固定，只要使用者立刻收到回饋，對等待的容忍度通常會更高。專案目前在處理過程中提供「thinking」通知，以改善感知上的反應速度。

## 架構

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

關鍵檔案：

- `src/components/AssistantButton/AssistantButton.tsx`：錄音狀態、請求協調、播放。
- `src/app/api/speechToText/route.ts`：base64 audio -> `/tmp/input.webm` -> Whisper transcription。
- `src/app/api/chat/route.ts`：透過 OpenAI 進行 chat completion。
- `src/app/page.tsx`：桌面優先介面與行動裝置 fallback 訊息。

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

- Node.js 18+（建議：Node.js 18.17+ 或 20 LTS，適用於 Next.js 13）。
- npm（本專案使用 `package-lock.json`）。
- OpenAI API key。
- ElevenLabs API key 與 voice ID。
- 可存取麥克風的桌面瀏覽器（行動裝置 UX 目前在設計上仍有限制）。

## 安裝

1. 複製儲存庫：

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. 從 [https://openai.com/](https://openai.com/) 與 [https://elevenlabs.com/](https://elevenlabs.com/) 取得 API keys。

將 `.env.example` 複製為 `.env.local`，並加入你的 keys：

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL=(Optional)
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. 安裝相依套件：

```sh
npm install
```

4. 在本機執行應用程式：

```sh
npm run dev
```

5. 部署到 Vercel：

本專案相容於 Next.js 的標準 Vercel 部署流程。

## 設定

本專案使用的環境變數：

| Variable | Required | Description |
| --- | --- | --- |
| `OPENAI_API_KEY` | Yes | API key used for Whisper transcription and GPT chat completion. |
| `OPENAI_BASE_URL` | No | Optional override for OpenAI API base URL (proxy/gateway). |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Yes | ElevenLabs API key used in the browser-side TTS request. |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Yes | ElevenLabs voice ID for TTS synthesis. |

備註：

- 依照 Next.js 慣例，`NEXT_PUBLIC_*` 變數會暴露給 client。
- `speechToText` 目前在轉錄前會先將暫存音訊寫入 `/tmp/input.webm`。

## 使用方式

1. 在桌面瀏覽器中開啟應用程式。
2. 點擊助理球體一次並授予麥克風權限。
3. 再點一次開始錄音，接著再點一次停止並送出。
4. Aura 會轉錄你的輸入、產生回應，然後播放合成語音。

本機 scripts：

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## API 範例

以下範例有助於除錯本機 API routes。

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

預期回應格式：

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

預期回應格式：

```json
"Assistant response text"
```

## 開發備註

- Chat route 設定為 Edge runtime（`export const runtime = "edge"`）。
- Whisper route 在伺服器端執行，並依賴檔案系統做暫存。
- UI 目前在行動端提供 fallback 訊息，而非完整互動流程。
- 使用 Toast 通知呈現權限／聆聽中／思考中狀態。
- 目前的 prompt shaping 要求簡短回答（`Your answer has to be as consise as possible.`）。

## 疑難排解

### 麥克風權限提示未出現

- 請確認瀏覽器允許 `localhost` 的麥克風存取。
- 在非 localhost 網域測試時請使用 HTTPS。

### 沒有音訊播放

- 檢查 `NEXT_PUBLIC_ELEVENLABS_API_KEY` 與 `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`。
- 確認瀏覽器 autoplay/audio-context 限制（需要使用者互動）。

### `/api/speechToText` 回傳 API 500

- 確認已設定 `OPENAI_API_KEY`。
- 驗證輸入是否為有效的 base64 編碼 `webm` 音訊。

### `/api/chat` 回傳 API 500

- 確認 `OPENAI_API_KEY` 與選用的 `OPENAI_BASE_URL` 設定正確。
- 確認你的 OpenAI 帳戶可使用 `gpt-4o` 模型。

### 延遲偏高

- 端到端延遲通常以 TTS 合成時間為主。
- 讓 prompts 更精簡，並考慮將長回應拆分。

## 路線圖

根據目前程式碼與備註可推測的下一步改進：

- 支援行動優先互動（取代目前僅桌面可用的 gating）。
- 串流部分助理回應以降低感知延遲。
- 強化轉錄與 TTS 失敗情境的重試／錯誤 UX。
- 新增自動化測試與 CI 檢查。
- 在 [`/i18n`](./i18n/) 下擴充多語系文件。

## 貢獻

歡迎且感謝各種貢獻。

- 請先閱讀 [CONTRIBUTING.md](./CONTRIBUTING.md) 了解流程與期望。
- 參與前請先閱讀 [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)。
- 針對 bug 或功能想法開 issue：
- Bug report：[template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- Feature request：[template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## 聯絡方式

嗨！感謝你查看並使用這個函式庫。如果你想討論你的專案、需要 mentoring、考慮合作聘用，或只是想聊聊，我都很樂意交流。

你可以寄信到：`j.schoen@mail.com`，或透過 Twitter 聯絡：[ @julianschoen ](https://twitter.com/julianschoen)

如果你想回饋支持，我有一個 Buy Me A Coffee：

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

謝謝，祝你有美好的一天 👋

## 免責聲明

Voice Assistant 是一個實驗性應用程式，並以「現狀」提供，不附任何明示或暗示保證。使用本軟體即表示你同意承擔其使用相關的所有風險，包括但不限於資料遺失、系統故障或其他可能發生的問題。

本專案的開發者與貢獻者不對因使用本軟體而導致的任何損失、損害或其他後果承擔責任。你需自行對根據 Voice Assistant 提供資訊所做的任何決策與行動負全責。

請注意，使用 GPT-4 語言模型可能因 token 使用量而產生較高成本。使用本專案即表示你確認自己有責任監控並管理 token 使用量與相關費用。強烈建議你定期檢查 OpenAI API 使用情況，並設定必要的限制或警示，以避免非預期費用。

使用 Voice Assistant 即表示你同意就因使用本軟體或違反這些條款所產生的任何與所有索賠、損害、損失、責任、成本與費用（包括合理律師費），對開發者、貢獻者及任何關聯方進行賠償、抗辯並使其免受損害。

<!-- LICENSE -->

## 授權

依 MIT License 發布。更多資訊請見 `LICENSE`。

儲存庫備註：此儲存庫目前將授權檔案命名為 [`LICENCE`](./LICENCE)。
