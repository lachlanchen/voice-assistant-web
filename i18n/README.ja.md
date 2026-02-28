[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


<a name="readme-top"></a>

<br />
<div align="center">

<h3 align="center">Aura へようこそ 👋</h3>

<p align="center">
Aura は低レイテンシ応答向けに最適化されたスマート音声アシスタントです。Vercel Edge Functions、Whisper 音声認識、GPT-4o、ElevenLabs TTS ストリーミングを使用しています。
<br />
<br />
<a href="https://voice.julianschoen.co">デモを見る</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=">バグを報告</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=">機能を提案</a>
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

- [概要](#概要)
- [主な機能](#主な機能)
- [デモ](#デモ)
- [背景](#背景)
- [レイテンシとユーザー体験について](#レイテンシとユーザー体験について)
- [アーキテクチャ](#アーキテクチャ)
- [プロジェクト構成](#プロジェクト構成)
- [前提条件](#前提条件)
- [インストール](#インストール)
- [設定](#設定)
- [使い方](#使い方)
- [API 例](#api-例)
- [開発メモ](#開発メモ)
- [トラブルシューティング](#トラブルシューティング)
- [ロードマップ](#ロードマップ)
- [コントリビューション](#コントリビューション)
- [連絡先](#連絡先)
- [免責事項](#免責事項)
- [ライセンス](#ライセンス)

## 概要

Aura は Next.js（App Router）と TypeScript で構築された、ブラウザベースの Siri ライクな音声アシスタントです。

### ひと目で分かるポイント

| 項目 | 詳細 |
| --- | --- |
| 主な目的 | Web 上での高速・実用的・低レイテンシな音声インタラクション |
| 実行モデル | ブラウザ収音 + サーバー API ルート + Edge チャットエンドポイント |
| 音声認識 | OpenAI Whisper (`whisper-1`) |
| アシスタントモデル | OpenAI GPT-4o |
| 音声合成 | ElevenLabs のストリーミング再生（ブラウザ） |

対話ループは次のとおりです。

1. ブラウザでマイク音声を取得する。
2. OpenAI Whisper (`whisper-1`) で音声を文字起こしする。
3. OpenAI GPT-4o で簡潔な回答を生成する。
4. ElevenLabs を使って合成音声をユーザーへストリーミング再生する。

このプロジェクトは、アシスタントが「聞いている/考えている」状態を視覚的にフィードバックしながら、実用的な低レイテンシ UX を実現することに最適化されています。

## 主な機能

✅ ブラウザ内で動く Siri ライクな音声アシスタント  
✅ 低レイテンシ応答向けに最適化  
✅ OpenAI、Whisper 音声認識、ElevenLabs を活用

追加の実装詳細:

- TypeScript を用いた Next.js 13 App Router。
- Edge runtime のチャットエンドポイント（`/api/chat`）。
- トースト通知による操作フィードバック（マイク権限、リスニング中、思考中）。
- ストリーミング TTS 再生に対応したアニメーション付きアシスタントボタン。
- プロキシ/セルフホスト型ゲートウェイ構成向けの OpenAI base URL 上書きオプション。

## デモ

Aura は以下で試せます: [https://voice.julianschoen.co](https://voice.julianschoen.co)

## 背景

音声アシスタントは、スマートフォン、車、家庭など日常のさまざまな場面で欠かせない存在になっています。一方で、同等の体験を Web で高い応答性とともに実現するのは、これまで難しい課題でした。

最近まで、Web 音声アシスタントの主な問題はレイテンシでした。音声をサーバーへ送信し、LLM の応答を生成し、合成音声を返して再生するまでに時間がかかりすぎていたためです。OpenAI、ElevenLabs、Vercel の近年の進展により、Web でも実用的な速度の音声アシスタントが構築可能になりました。

このリポジトリは、自分で音声アシスタントを作りたい人や、実装上のトレードオフを理解したい人にとって、有用な参照先になることを目指しています。

## レイテンシとユーザー体験について

優れた音声 UX において、レイテンシは最重要要素です。現在の主な要因は 3 つあります。

- 文字起こし時間（Whisper 音声認識）。
- 応答生成時間（元プロジェクトノートでは GPT-4o Mini）。
- 音声合成ストリーミング時間（ElevenLabs TTS）。

実運用ベースの検証メモでは、音声生成に最も時間がかかりやすく、特に長文応答ではばらつきも大きい傾向があります。

緩和策として、応答を複数パートに分割して順次ストリーミングする方法が考えられます。これにより残りの生成中でも、ユーザーは早く聞き始められます。現時点では未実装ですが、有望な方向性です。

もうひとつの重要概念は、待ち時間の体感です。総レイテンシが同じでも、即時フィードバックがあるとユーザーは遅延を受け入れやすくなります。本プロジェクトでは、処理中に "thinking" 通知を表示し、体感レスポンスの改善を図っています。

## アーキテクチャ

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

主要ファイル:

- `src/components/AssistantButton/AssistantButton.tsx`: 録音状態管理、リクエスト制御、再生処理。
- `src/app/api/speechToText/route.ts`: base64 音声 -> `/tmp/input.webm` -> Whisper 文字起こし。
- `src/app/api/chat/route.ts`: OpenAI によるチャット補完。
- `src/app/page.tsx`: デスクトップ優先 UI とモバイル向けフォールバックメッセージ。

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

- Node.js 18+（推奨: Next.js 13 向けに Node.js 18.17+ または 20 LTS）。
- npm（本プロジェクトは `package-lock.json` を使用）。
- OpenAI API キー。
- ElevenLabs API キーと voice ID。
- マイクアクセス可能なデスクトップブラウザ（モバイル UX は設計上まだ制限あり）。

## インストール

1. リポジトリをクローン:

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. [https://openai.com/](https://openai.com/) と [https://elevenlabs.com/](https://elevenlabs.com/) で API キーを取得します。

`.env.example` を `.env.local` にコピーし、キーを設定します。

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL=(Optional)
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. 依存関係をインストール:

```sh
npm install
```

4. ローカルで起動:

```sh
npm run dev
```

5. Vercel へデプロイ:

このプロジェクトは Next.js の標準的な Vercel デプロイフローに対応しています。

## 設定

このプロジェクトで使用する環境変数:

| 変数 | 必須 | 説明 |
| --- | --- | --- |
| `OPENAI_API_KEY` | Yes | Whisper 文字起こしと GPT チャット補完で使用する API キー。 |
| `OPENAI_BASE_URL` | No | OpenAI API ベース URL の任意上書き（proxy/gateway）。 |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Yes | ブラウザ側の TTS リクエストで使用する ElevenLabs API キー。 |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Yes | TTS 合成に使用する ElevenLabs voice ID。 |

補足:

- `NEXT_PUBLIC_*` 変数は Next.js の規約でクライアントに公開されます。
- `speechToText` は現在、文字起こし前に一時音声を `/tmp/input.webm` に書き込みます。

## 使い方

1. デスクトップブラウザでアプリを開きます。
2. アシスタントのオーブを 1 回クリックし、マイク権限を許可します。
3. もう一度クリックで録音開始、さらにもう一度クリックで停止して送信します。
4. Aura が入力を文字起こしし、応答を生成して、合成音声を再生します。

ローカルスクリプト:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## API 例

以下の例はローカル API ルートのデバッグに便利です。

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

期待されるレスポンス形式:

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

期待されるレスポンス形式:

```json
"Assistant response text"
```

## 開発メモ

- Chat ルートは Edge runtime で設定されています（`export const runtime = "edge"`）。
- Whisper ルートはサーバー側で動作し、一時保存のためにファイルシステムアクセスが必要です。
- UI は現在、完全なモバイル操作の代わりにモバイル向けフォールバックメッセージを表示します。
- マイク権限/リスニング中/思考中の状態通知にトーストを利用しています。
- 現在のプロンプト整形は簡潔な回答を要求します（`Your answer has to be as consise as possible.`）。

## トラブルシューティング

### マイク権限のダイアログが表示されない

- ブラウザで `localhost` のマイクアクセスが許可されているか確認してください。
- `localhost` 以外で検証する場合は HTTPS を使用してください。

### 音声が再生されない

- `NEXT_PUBLIC_ELEVENLABS_API_KEY` と `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` を確認してください。
- ブラウザの autoplay/audio-context 制約を確認してください（ユーザー操作が必要です）。

### `/api/speechToText` が API 500 を返す

- `OPENAI_API_KEY` が設定されていることを確認してください。
- 入力が有効な base64 エンコード済み `webm` 音声であることを確認してください。

### `/api/chat` が API 500 を返す

- `OPENAI_API_KEY` と任意の `OPENAI_BASE_URL` が正しいことを確認してください。
- OpenAI アカウントで `gpt-4o` が利用可能か確認してください。

### レイテンシが高い

- エンドツーエンド遅延は通常、TTS 合成時間の影響が最も大きくなります。
- プロンプトを簡潔にし、長い応答は分割を検討してください。

## ロードマップ

現在のコードとメモから考えられる次の改善:

- モバイルファーストの操作対応（現在のデスクトップ限定ゲーティングを置き換え）。
- 体感レイテンシ削減のためのアシスタント応答部分ストリーミング。
- 文字起こし/TTS 失敗時のリトライとエラー UX 改善。
- 自動テストと CI チェックの追加。
- [`/i18n`](./i18n/) 配下の多言語ドキュメント拡充。

## コントリビューション

コントリビューションを歓迎します。

- ワークフローと期待事項は [CONTRIBUTING.md](./CONTRIBUTING.md) を参照してください。
- 参加前に [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) を確認してください。
- バグや機能アイデアは issue を作成してください:
- バグ報告: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- 機能提案: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## 連絡先

このライブラリを見つけて使っていただきありがとうございます。あなたのプロジェクトの相談、メンタリングの依頼、採用のご相談、あるいは気軽な雑談まで、いつでも歓迎です。

メール: `j.schoen@mail.com` または Twitter: [@julianschoen](https://twitter.com/julianschoen) までご連絡ください。

もしお返ししたいと思っていただけたら、Buy Me A Coffee があります:

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

ありがとうございます。良い一日を 👋

## 免責事項

Voice Assistant は実験的なアプリケーションであり、明示・黙示を問わず一切の保証なく "as-is" で提供されます。本ソフトウェアを使用することで、データ損失、システム障害、その他発生し得る問題を含む、利用に伴うすべてのリスクを利用者自身が負うことに同意したものとみなされます。

本プロジェクトの開発者およびコントリビューターは、本ソフトウェアの使用に起因して生じるいかなる損失、損害、その他の結果についても、一切の責任を負いません。Voice Assistant が提供する情報に基づく判断および行動は、すべて利用者自身の責任で行ってください。

GPT-4 言語モデルの利用は、トークン使用量により高額になる場合があります。本プロジェクトを利用することで、トークン使用量および関連コストの監視・管理は利用者自身の責任であることを認めるものとします。想定外の請求を防ぐため、OpenAI API の利用状況を定期的に確認し、必要な上限設定やアラート設定を行うことを強く推奨します。

Voice Assistant を使用することで、利用者は本ソフトウェアの使用または本規約違反に起因して生じるあらゆる請求、損害、損失、責任、費用および経費（合理的な弁護士費用を含む）について、開発者、コントリビューターおよび関連当事者を防御し、補償し、免責することに同意するものとします。

<!-- LICENSE -->

## ライセンス

MIT ライセンスの下で配布されています。詳細は `LICENSE` を参照してください。

リポジトリ注記: このリポジトリでは現在、ライセンスファイル名が [`LICENCE`](./LICENCE) になっています。
