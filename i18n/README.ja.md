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

<h3 align="center">Aura へようこそ 👋</h3>

<p align="center">
Aura は、低遅延応答向けに最適化されたブラウザーベースの Siri ライクな音声アシスタントです。Vercel Edge Functions、Whisper 音声認識、GPT-4o、ElevenLabs TTS ストリーミングを使用しています。
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

## 目次

- [📌 概要](#概要)
- [✨ 機能](#機能)
- [🎥 デモ](#デモ)
- [🧠 背景](#背景)
- [⏱️ レイテンシとユーザー体験について](#レイテンシとユーザー体験について)
- [🏗️ アーキテクチャ](#アーキテクチャ)
- [📁 プロジェクト構成](#プロジェクト構成)
- [✅ 前提条件](#前提条件)
- [🧰 インストール](#インストール)
- [⚙️ 設定](#設定)
- [🧪 使い方](#使い方)
- [📦 API の例](#api-の例)
- [🛠️ 開発ノート](#開発ノート)
- [🧯 トラブルシューティング](#トラブルシューティング)
- [🗺️ ロードマップ](#ロードマップ)
- [🤝 コントリビューション](#コントリビューション)
- [❤️ Support](#%e2%9d%a4%ef%b8%8f-support)
- [📬 連絡先](#連絡先)
- [⚠️ 免責事項](#免責事項)
- [📄 ライセンス](#ライセンス)

## 概要

Aura は、Next.js（App Router）と TypeScript で構築された、ブラウザベースの Siri ライクな音声アシスタントです。

### 一目で分かるポイント

| 項目 | 詳細 |
| --- | --- |
| 主な目的 | Web 上で高速かつ実用的な低遅延の音声インタラクション |
| 実行モデル | ブラウザ録音 + サーバー API ルート + Edge チャットエンドポイント |
| 音声認識 | OpenAI Whisper（`whisper-1`） |
| アシスタントモデル | OpenAI GPT-4o |
| 音声合成 | ElevenLabs によるブラウザ内ストリーミング再生 |

対話の流れは次のとおりです。

1. ブラウザでマイク音声を取得します。
2. OpenAI Whisper（`whisper-1`）で文字起こしを行います。
3. OpenAI GPT-4o で簡潔な回答を生成します。
4. ElevenLabs を使って合成音声をユーザーへストリーミング再生します。

このプロジェクトは、アシスタントが聞いている/考えている状態を視覚的に示すことで、実用的な低レイテンシ UX を実現するよう最適化されています。

### ビジュアル要約

| ステージ | 目的 |
| --- | --- |
| 🎙️ Capture | ブラウザ録音 + 権限状態に応じた UI |
| 🧠 Process | Whisper 文字起こし + GPT-4o 応答生成 |
| 🔉 Deliver | ElevenLabs ストリーミング再生と状態フィードバック |

## 機能

| 機能 | 意味 |
| --- | --- |
| ✅ Siri ライクなブラウザアシスタント | シンプルな Web UI で音声入力・音声出力を完結 |
| ⚡ 低遅延ワークフロー | 録音、文字起こし、生成、再生ループを最適化 |
| 🧠 LLM + TTS 構成 | OpenAI Whisper、GPT-4o、ElevenLabs ストリーミング合成 |
| 🧩 拡張しやすいアーキテクチャ | モデルのエンドポイントや音声プロバイダーをプロジェクト単位で差し替え可能 |

追加実装の詳細:

| フォーカス | 現在の挙動 |
| --- | --- |
| フレームワーク | Next.js 13 App Router と TypeScript |
| API ランタイム | Edge runtime チャットエンドポイント（`/api/chat`） |
| UX フィードバック | マイク権限、聞き取り、思考状態のトースト通知 |
| インタラクション UI | ストリーミング TTS 再生付きアニメーションアシスタントボタン |
| ネットワーク | プロキシ/セルフホストゲートウェイ向けに OpenAI ベース URL を任意上書き |

## デモ

Aura はこちらで試せます: [https://voice.julianschoen.co](https://voice.julianschoen.co)

## 背景

音声アシスタントは、スマートフォン、車載、スマートホームなど日常のあらゆるシーンで重要な位置を占めるようになりました。高い応答性を維持したままその体験を Web に持ち込むのは、長く難しい課題でした。

これまで、Web 上の音声アシスタント最大の問題はレイテンシでした。音声をサーバーへ送信して LLM 応答を生成し、音声を再生するまでに時間がかかりすぎていました。最近の OpenAI、ElevenLabs、Vercel の進化により、Web でも実用レベルで高速な音声アシスタントを構築できるようになりました。

このリポジトリは、自分自身で音声アシスタントを作成したい開発者が、実装上のトレードオフを理解しながら進められるベースとして役立つことを目指しています。

## レイテンシとユーザー体験について

レイテンシは良い音声 UX の最重要要素です。現在、主な要因は 3 つあります。

- 文字起こし時間（Whisper 音声認識）
- 応答生成時間（元プロジェクトノートでは GPT-4o Mini）
- 音声合成のストリーミング時間（ElevenLabs TTS）

実務的な検証では、特に長い応答になるほど、音声生成の時間が最も長く、かつばらつきが大きい傾向があります。

有効な対策として、返答を複数パートに分割して順にストリーミングする方法が考えられます。これにより、残りの生成が続いている間でもユーザーは早く聞き始められます。現時点では未実装ですが、有望な方針です。

もうひとつの重要概念は知覚される待ち時間です。総レイテンシが同じでも、即時のフィードバックがある場合、ユーザーは遅延をより許容しやすいです。プロジェクトには、処理中の「thinking」通知があり、体感レスポンスを改善しています。

## アーキテクチャ

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

主要ファイル:

- `src/components/AssistantButton/AssistantButton.tsx`: 録音状態、リクエスト制御、再生処理。
- `src/app/api/speechToText/route.ts`: base64 音声 -> `/tmp/input.webm` -> Whisper 文字起こし。
- `src/app/api/chat/route.ts`: OpenAI 経由のチャット補完。
- `src/app/page.tsx`: デスクトップファーストのインターフェースと、モバイル向けフォールバック表示。

## プロジェクト構成

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

## 前提条件

| 要件 | 詳細 |
| --- | --- |
| Node.js | 18+（推奨: Next.js 13 向けに Node.js 18.17+ または 20 LTS） |
| パッケージマネージャー | npm（プロジェクトは `package-lock.json` を使用） |
| API 利用権限 | OpenAI API キー |
| TTS 利用権限 | ElevenLabs API キーと Voice ID |
| クライアント | マイク利用可能なデスクトップブラウザ（モバイル UX は現在デスクトップ優先） |

## インストール

1. リポジトリをクローンします。

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. 環境変数テンプレートをコピーして値を編集します。

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL="" # Optional
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. 依存関係をインストールします。

```sh
npm install
```

4. ローカルでアプリを起動します。

```sh
npm run dev
```

5. `http://localhost:3000` を開きます。

補足: 非ローカルドメインでマイクアクセスを試す場合、通常は HTTPS が必要です。

6. Vercel へデプロイします。

このプロジェクトは標準的な Next.js のデプロイフローに従います。Vercel の既定インポート設定を使い、同じ環境変数をプロジェクトに設定してください。

## 設定

このプロジェクトで使用する環境変数:

| 変数 | 必須 | 説明 |
| --- | --- | --- |
| `OPENAI_API_KEY` | はい | Whisper 文字起こしと GPT チャット補完で使用する API キー。
 |
| `OPENAI_BASE_URL` | いいえ | OpenAI API ベース URL の任意上書き（proxy/gateway 用）。 |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | はい | ブラウザ側の TTS リクエストで使用する ElevenLabs API キー。 |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | はい | TTS 合成で使用する ElevenLabs の Voice ID。 |

補足:

- `NEXT_PUBLIC_*` 変数は Next.js の規約に従いクライアントへ公開されます。
- `speechToText` は現在、文字起こし前に一時ファイルとして `/tmp/input.webm` を使用します。

## 使い方

1. デスクトップブラウザでアプリを開きます。
2. アシスタントボタンを 1 回クリックしてマイク権限を許可します。
3. 再度クリックして録音を開始し、もう一度クリックして停止して送信します。
4. Aura が入力を文字起こしし、回答を生成し、合成音声を再生します。

ローカル実行スクリプト:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## API の例

ローカル API ルートのデバッグ時に役立つ例です。

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

想定レスポンス:

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

想定レスポンス:

```json
"Assistant response text"
```

## 開発ノート

- チャットルートは Edge runtime で設定されています（`export const runtime = "edge"`）。
- Whisper ルートはサーバー側で実行され、一時保存のためファイルシステムアクセスに依存します。
- UI は現在モバイル向けに完全対応しておらず、モバイルフォールバックメッセージを表示します。
- トースト通知で、許可・録音・思考状態を表示します。
- 現在のプロンプト設計は簡潔な回答を要求します（`Your answer has to be as concise as possible.`）。
- 実行時ログ、リクエスト追跡、ストリーミング挙動は現時点で CI では未検証です（リポジトリに自動テストはありません）。

## トラブルシューティング

### 🎤 マイク権限の許可ダイアログが表示されない

- ブラウザが `localhost` でのマイクアクセスを許可していることを確認します。
- 非 localhost ドメインでテストする場合は HTTPS を利用します。

### 🔈 再生されない

- `NEXT_PUBLIC_ELEVENLABS_API_KEY` と `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` を確認します。
- ブラウザの自動再生 / AudioContext の制限を確認します（ユーザー操作が必要）。

### 📡 `/api/speechToText` で API 500 が発生する

- `OPENAI_API_KEY` が設定されているか確認します。
- 入力値が有効な base64 エンコードの `webm` 音声になっているか検証します。

### 📡 `/api/chat` で API 500 が発生する

- `OPENAI_API_KEY` と必要に応じて `OPENAI_BASE_URL` が正しいか確認します。
- OpenAI アカウントで `gpt-4o` のモデル利用可能性を確認します。

### ⏳ レイテンシが高い

- エンドツーエンド遅延は通常、TTS 合成時間が支配的です。
- プロンプトを短く保ち、長い応答は分割を検討します。

## ロードマップ

現在のコードとメモから見込まれる次の改善:

- モバイルファーストのインタラクション対応（現在のデスクトップ限定ガードの置き換え）。
- 体感遅延を下げるために、応答を分割してストリーミング再生。
- 文字起こしや TTS 失敗時のリトライとエラー UX 改善。
- 自動テストと CI チェックの追加。
- [`/i18n`](./i18n/) 以下の多言語ドキュメント拡充。

## コントリビューション

コントリビューションは歓迎します。

- 作業フローと期待値は [CONTRIBUTING.md](./CONTRIBUTING.md) を参照してください。
- 参加前に [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) を確認してください。
- バグ報告や機能提案は issue を作成してください。
- バグ報告: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- 機能提案: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## 連絡先

ご覧いただき、ありがとうございます。プロジェクト相談、メンタリング依頼、採用ご提案、その他お問い合わせがあればお声がけください。

メール: `j.schoen@mail.com`、または X（旧 Twitter）: [@julianschoen](https://twitter.com/julianschoen)

ご支援をご検討いただける場合は、Buy Me A Coffee があります。

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

素敵な1日をお過ごしください 👋

## 免責事項

Voice Assistant は実験的なアプリケーションであり、明示的または黙示の如何を問わず「現状のまま（as-is）」で提供されます。本ソフトウェアを使用することにより、データ損失、システム障害、その他発生し得る問題を含め、本ソフトウェアの利用に伴うすべてのリスクは利用者の責任となることに同意したものとみなされます。

本プロジェクトの開発者とコントリビューターは、本ソフトウェアの使用から生じる損失、損害、その他の結果について一切の責任を負いません。Voice Assistant が提供する情報に基づく判断や行動は、利用者ご自身の責任で行ってください。

GPT-4 言語モデルの利用はトークン消費が原因で高額になる場合があります。本プロジェクトを利用することで、トークン消費量と関連コストの監視・管理は利用者自身の責任で行うことに同意したものとします。予期しない課金を防ぐため、OpenAI API 利用状況を定期的に確認し、必要に応じて上限やアラートを設定することを強く推奨します。

Voice Assistant の使用により、利用者は本ソフトウェアの使用、あるいは本規約違反により生じた、あらゆる請求、損害、損失、責任、費用、経費（合理的な弁護士費用を含む）について、開発者、コントリビューター、および関連当事者を補償し、防御し、無害化することに同意します。

<!-- LICENSE -->

## ライセンス

MIT ライセンスの下で配布されています。詳細は `LICENSE` を参照してください。

本リポジトリのライセンスファイルは現在 [`LICENCE`](./LICENCE) という名前で保存されています。


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
