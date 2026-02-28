[English](README.md) · [العربية](i18n/README.ar.md) · [Español](i18n/README.es.md) · [Français](i18n/README.fr.md) · [日本語](i18n/README.ja.md) · [한국어](i18n/README.ko.md) · [Tiếng Việt](i18n/README.vi.md) · [中文 (简体)](i18n/README.zh-Hans.md) · [中文（繁體）](i18n/README.zh-Hant.md) · [Deutsch](i18n/README.de.md) · [Русский](i18n/README.ru.md)

<a name="readme-top"></a>


<br />
<div align="center">

<h3 align="center">Say hi to Aura 👋</h3>

<p align="center">
Aura is a smart voice assistant optimized for low-latency responses. It uses Vercel Edge Functions, Whisper speech recognition, GPT-4o, and ElevenLabs TTS streaming.
<br />
<br />
<a href="https://voice.julianschoen.co">View Demo</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=">Report Bug</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=">Request Feature</a>
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

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Demo](#demo)
- [Motivation](#motivation)
- [Thoughts on latency and user experience](#thoughts-on-latency-and-user-experience)
- [Architecture](#architecture)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [API Examples](#api-examples)
- [Development Notes](#development-notes)
- [Troubleshooting](#troubleshooting)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [Contact](#contact)
- [Disclaimer](#disclaimer)
- [License](#license)

## Overview

Aura is a browser-based, Siri-like voice assistant built with Next.js (App Router) and TypeScript.

### At a glance

| Area | Details |
| --- | --- |
| Primary goal | Fast, practical, low-latency voice interaction on the web |
| Runtime model | Browser capture + server API routes + Edge chat endpoint |
| Speech-to-text | OpenAI Whisper (`whisper-1`) |
| Assistant model | OpenAI GPT-4o |
| Text-to-speech | ElevenLabs streaming playback in the browser |

The interaction loop is:

1. Capture microphone audio in the browser.
2. Transcribe speech with OpenAI Whisper (`whisper-1`).
3. Generate a concise answer with OpenAI GPT-4o.
4. Stream synthesized audio back to the user using ElevenLabs.

The project is optimized around practical low-latency UX, with visual feedback while the assistant is listening or thinking.

## Features

✅ A Siri-like voice assistant within your browser  
✅ Optimized for low-latency responses  
✅ Built with OpenAI, Whisper speech recognition, and ElevenLabs

Additional implementation details:

- Next.js 13 App Router with TypeScript.
- Edge runtime chat endpoint (`/api/chat`).
- Toast-based interaction feedback (microphone permission, listening, thinking).
- Animated assistant button with streaming TTS playback.
- Optional OpenAI base URL override for proxy/self-hosted gateway setups.

## Demo

You can test Aura here: [https://voice.julianschoen.co](https://voice.julianschoen.co)

## Motivation

Voice assistants have become an integral part of everyday life: phones, cars, homes, and more. Bringing that experience to the web with good responsiveness has historically been difficult.

Until recently, the main problem with voice assistants on the web was latency. It took too long to send audio to the server, generate an LLM completion, and stream speech back. Recent advances from OpenAI, ElevenLabs, and Vercel made it possible to build a voice assistant that is fast enough to be practical on the web.

This repository aims to be a go-to place for people who want to build their own voice assistant and understand the tradeoffs in real implementations.

## Thoughts on latency and user experience

Latency is the most important factor for a good voice UX. Currently there are three major contributors:

- Transcription time (Whisper speech recognition).
- Response generation time (GPT-4o Mini in the original project notes).
- Speech synthesis streaming time (ElevenLabs TTS).

From practical testing notes, speech generation tends to take the most time and is the least predictable, especially for longer responses.

A possible mitigation strategy is splitting the response into multiple parts and streaming them one after another. This lets the user start listening earlier while the rest is still being generated. This is not implemented yet, but it is a promising direction.

Another key concept is perceived wait time. Even when total latency is fixed, users tolerate delays better when they receive immediate feedback. The project currently includes a "thinking" notification during processing to improve perceived responsiveness.

## Architecture

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

Key files:

- `src/components/AssistantButton/AssistantButton.tsx`: recording state, request orchestration, playback.
- `src/app/api/speechToText/route.ts`: base64 audio -> `/tmp/input.webm` -> Whisper transcription.
- `src/app/api/chat/route.ts`: chat completion via OpenAI.
- `src/app/page.tsx`: desktop-first interface and mobile fallback message.

## Project Structure

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

## Prerequisites

- Node.js 18+ (recommended: Node.js 18.17+ or 20 LTS for Next.js 13).
- npm (project uses `package-lock.json`).
- OpenAI API key.
- ElevenLabs API key and voice ID.
- A desktop browser with microphone access (mobile UX is currently limited by design).

## Installation

1. Clone the repo:

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. Get API keys from [https://openai.com/](https://openai.com/) and [https://elevenlabs.com/](https://elevenlabs.com/).

Copy the `.env.example` file to `.env.local` and add your keys:

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL=(Optional)
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. Install dependencies:

```sh
npm install
```

4. Run the app locally:

```sh
npm run dev
```

5. Deploy to Vercel:

This project is compatible with the standard Vercel deployment flow for Next.js.

## Configuration

Environment variables used by this project:

| Variable | Required | Description |
| --- | --- | --- |
| `OPENAI_API_KEY` | Yes | API key used for Whisper transcription and GPT chat completion. |
| `OPENAI_BASE_URL` | No | Optional override for OpenAI API base URL (proxy/gateway). |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Yes | ElevenLabs API key used in the browser-side TTS request. |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Yes | ElevenLabs voice ID for TTS synthesis. |

Notes:

- `NEXT_PUBLIC_*` variables are exposed to the client by Next.js conventions.
- `speechToText` currently writes temporary audio to `/tmp/input.webm` before transcription.

## Usage

1. Open the app in a desktop browser.
2. Click the assistant orb once and grant microphone permissions.
3. Click again to start recording, then click again to stop and send.
4. Aura transcribes your input, generates a response, then plays synthesized speech.

Local scripts:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## API Examples

These examples are useful for debugging local API routes.

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

Expected response shape:

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

Expected response shape:

```json
"Assistant response text"
```

## Development Notes

- Chat route is configured for Edge runtime (`export const runtime = "edge"`).
- Whisper route runs server-side and depends on file system access for temporary storage.
- The UI currently provides a mobile fallback message instead of full mobile interaction.
- Toast notifications are used to surface permission/listening/thinking states.
- Current prompt shaping asks for concise answers (`Your answer has to be as consise as possible.`).

## Troubleshooting

### Microphone permission prompt does not appear

- Ensure your browser allows microphone access for `localhost`.
- Use HTTPS when testing on non-localhost domains.

### No audio playback

- Check `NEXT_PUBLIC_ELEVENLABS_API_KEY` and `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`.
- Verify browser autoplay/audio-context restrictions (user interaction is required).

### API 500 from `/api/speechToText`

- Confirm `OPENAI_API_KEY` is set.
- Validate input contains valid base64-encoded `webm` audio.

### API 500 from `/api/chat`

- Confirm `OPENAI_API_KEY` and optional `OPENAI_BASE_URL` are correct.
- Check model availability for `gpt-4o` in your OpenAI account.

### High latency

- TTS synthesis time usually dominates end-to-end latency.
- Keep prompts concise and consider splitting long responses.

## Roadmap

Potential next improvements inferred from current code and notes:

- Mobile-first interaction support (replace current desktop-only gating).
- Streaming partial assistant responses to reduce perceived latency.
- Better retry/error UX around transcription and TTS failures.
- Add automated tests and CI checks.
- Expand multilingual documentation under [`/i18n`](./i18n/).

## Contributing

Contributions are welcome and appreciated.

- Read [CONTRIBUTING.md](./CONTRIBUTING.md) for workflow and expectations.
- Read [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) before participating.
- Open issues for bugs or feature ideas:
- Bug report: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- Feature request: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## Contact

Hi! Thanks for checking out and using this library. If you are interested in discussing your project, require mentorship, consider hiring me, or just want to chat, I'm happy to talk.

You can send me an email: `j.schoen@mail.com` or message me on Twitter: [@julianschoen](https://twitter.com/julianschoen)

If you'd like to give something back, I've got a Buy Me A Coffee account:

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

Thanks and have an awesome day 👋

## Disclaimer

Voice Assistant is an experimental application and is provided "as-is" without any warranty, express or implied. By using this software, you agree to assume all risks associated with its use, including but not limited to data loss, system failure, or any other issues that may arise.

The developers and contributors of this project do not accept any responsibility or liability for any losses, damages, or other consequences that may occur as a result of using this software. You are solely responsible for any decisions and actions taken based on the information provided by Voice Assistant.

Please note that use of the GPT-4 language model can be expensive due to token usage. By utilizing this project, you acknowledge that you are responsible for monitoring and managing your own token usage and associated costs. It is highly recommended to check your OpenAI API usage regularly and set up any necessary limits or alerts to prevent unexpected charges.

By using Voice Assistant, you agree to indemnify, defend, and hold harmless the developers, contributors, and any affiliated parties from and against any and all claims, damages, losses, liabilities, costs, and expenses (including reasonable attorneys' fees) arising from your use of this software or your violation of these terms.

<!-- LICENSE -->

## License

Distributed under the MIT License. See `LICENSE` for more information.

Repository note: this repository currently stores the license file as [`LICENCE`](./LICENCE).
