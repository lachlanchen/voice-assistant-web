[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


<a name="readme-top"></a>

<br />
<div align="center">

<h3 align="center">Aura에게 인사해 보세요 👋</h3>

<p align="center">
Aura는 저지연 응답에 최적화된 스마트 음성 비서입니다. Vercel Edge Functions, Whisper 음성 인식, GPT-4o, ElevenLabs TTS 스트리밍을 사용합니다.
<br />
<br />
<a href="https://voice.julianschoen.co">데모 보기</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=">버그 제보</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=">기능 요청</a>
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

- [개요](#overview)
- [기능](#features)
- [데모](#demo)
- [동기](#motivation)
- [지연 시간과 사용자 경험에 대한 생각](#thoughts-on-latency-and-user-experience)
- [아키텍처](#architecture)
- [프로젝트 구조](#project-structure)
- [사전 요구사항](#prerequisites)
- [설치](#installation)
- [설정](#configuration)
- [사용 방법](#usage)
- [API 예시](#api-examples)
- [개발 노트](#development-notes)
- [문제 해결](#troubleshooting)
- [로드맵](#roadmap)
- [기여](#contributing)
- [연락처](#contact)
- [면책 조항](#disclaimer)
- [라이선스](#license)

## Overview

Aura는 Next.js(App Router)와 TypeScript로 구축된 브라우저 기반 Siri 스타일 음성 비서입니다.

### At a glance

| 영역 | 상세 |
| --- | --- |
| 주요 목표 | 웹에서 빠르고 실용적인 저지연 음성 상호작용 |
| 런타임 모델 | 브라우저 캡처 + 서버 API 라우트 + Edge 채팅 엔드포인트 |
| 음성-텍스트 변환 | OpenAI Whisper (`whisper-1`) |
| 비서 모델 | OpenAI GPT-4o |
| 텍스트-음성 변환 | 브라우저에서 ElevenLabs 스트리밍 재생 |

상호작용 루프는 다음과 같습니다.

1. 브라우저에서 마이크 오디오를 캡처합니다.
2. OpenAI Whisper (`whisper-1`)로 음성을 전사합니다.
3. OpenAI GPT-4o로 간결한 답변을 생성합니다.
4. ElevenLabs를 사용해 합성 음성을 사용자에게 스트리밍합니다.

이 프로젝트는 비서가 듣거나 생각하는 동안 시각적 피드백을 제공하여, 실용적인 저지연 UX에 최적화되어 있습니다.

## Features

✅ 브라우저 안에서 동작하는 Siri 스타일 음성 비서  
✅ 저지연 응답에 최적화  
✅ OpenAI, Whisper 음성 인식, ElevenLabs 기반

추가 구현 세부사항:

- TypeScript 기반 Next.js 13 App Router.
- Edge 런타임 채팅 엔드포인트 (`/api/chat`).
- 토스트 기반 상호작용 피드백(마이크 권한, 듣는 중, 생각 중).
- 스트리밍 TTS 재생이 포함된 애니메이션 비서 버튼.
- 프록시/셀프호스팅 게이트웨이 구성을 위한 선택적 OpenAI base URL 오버라이드.

## Demo

여기에서 Aura를 테스트할 수 있습니다: [https://voice.julianschoen.co](https://voice.julianschoen.co)

## Motivation

음성 비서는 이제 휴대폰, 자동차, 집 등 일상 전반에 깊이 자리 잡았습니다. 하지만 웹에서 이 경험을 충분한 반응성과 함께 제공하는 일은 역사적으로 쉽지 않았습니다.

최근까지도 웹 음성 비서의 핵심 문제는 지연 시간이었습니다. 오디오를 서버로 전송하고, LLM 응답을 생성하고, 다시 음성을 스트리밍해 돌려받기까지 너무 오래 걸렸습니다. OpenAI, ElevenLabs, Vercel의 최근 발전 덕분에 웹에서도 실용적으로 빠른 음성 비서를 구축할 수 있게 되었습니다.

이 저장소는 자신만의 음성 비서를 만들고 실제 구현에서의 트레이드오프를 이해하려는 사람들을 위한 핵심 참고처가 되는 것을 목표로 합니다.

## Thoughts on latency and user experience

좋은 음성 UX에서 가장 중요한 요소는 지연 시간입니다. 현재 크게 세 가지 요인이 영향을 줍니다.

- 전사 시간(Whisper 음성 인식).
- 응답 생성 시간(원본 프로젝트 노트 기준 GPT-4o Mini).
- 음성 합성 스트리밍 시간(ElevenLabs TTS).

실제 테스트 노트에 따르면, 특히 응답이 길어질수록 음성 생성 단계가 가장 오래 걸리고 예측 가능성이 가장 낮습니다.

한 가지 완화 전략은 응답을 여러 부분으로 나누어 순차적으로 스트리밍하는 것입니다. 이렇게 하면 나머지 부분이 생성되는 동안에도 사용자는 먼저 듣기 시작할 수 있습니다. 아직 구현되지는 않았지만, 유망한 방향입니다.

또 다른 핵심 개념은 체감 대기 시간입니다. 총 지연 시간이 같더라도 즉각적인 피드백을 받으면 사용자는 지연을 더 잘 받아들입니다. 이 프로젝트는 현재 처리 중에 "thinking" 알림을 표시해 체감 반응성을 개선합니다.

## Architecture

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

핵심 파일:

- `src/components/AssistantButton/AssistantButton.tsx`: 녹음 상태, 요청 오케스트레이션, 재생.
- `src/app/api/speechToText/route.ts`: base64 audio -> `/tmp/input.webm` -> Whisper 전사.
- `src/app/api/chat/route.ts`: OpenAI를 통한 채팅 완성.
- `src/app/page.tsx`: 데스크톱 우선 인터페이스 및 모바일 폴백 메시지.

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

- Node.js 18+ (권장: Next.js 13용 Node.js 18.17+ 또는 20 LTS).
- npm (이 프로젝트는 `package-lock.json`을 사용).
- OpenAI API 키.
- ElevenLabs API 키 및 voice ID.
- 마이크 접근이 가능한 데스크톱 브라우저(모바일 UX는 현재 설계상 제한됨).

## Installation

1. 저장소를 클론합니다:

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. [https://openai.com/](https://openai.com/) 및 [https://elevenlabs.com/](https://elevenlabs.com/)에서 API 키를 발급받습니다.

`.env.example` 파일을 `.env.local`로 복사한 뒤 키를 추가하세요:

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL=(Optional)
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. 의존성을 설치합니다:

```sh
npm install
```

4. 로컬에서 앱을 실행합니다:

```sh
npm run dev
```

5. Vercel에 배포합니다:

이 프로젝트는 Next.js의 표준 Vercel 배포 플로우와 호환됩니다.

## Configuration

이 프로젝트에서 사용하는 환경 변수:

| Variable | Required | Description |
| --- | --- | --- |
| `OPENAI_API_KEY` | Yes | Whisper 전사 및 GPT 채팅 완성에 사용하는 API 키입니다. |
| `OPENAI_BASE_URL` | No | OpenAI API base URL에 대한 선택적 오버라이드(프록시/게이트웨이). |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Yes | 브라우저 측 TTS 요청에서 사용하는 ElevenLabs API 키입니다. |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Yes | TTS 합성에 사용하는 ElevenLabs voice ID입니다. |

참고:

- `NEXT_PUBLIC_*` 변수는 Next.js 규칙에 따라 클라이언트에 노출됩니다.
- `speechToText`는 현재 전사 전에 임시 오디오를 `/tmp/input.webm`에 기록합니다.

## Usage

1. 데스크톱 브라우저에서 앱을 엽니다.
2. 비서 오브를 한 번 클릭하고 마이크 권한을 허용합니다.
3. 다시 클릭해 녹음을 시작하고, 한 번 더 클릭해 중지 및 전송합니다.
4. Aura가 입력을 전사하고 응답을 생성한 뒤 합성 음성을 재생합니다.

로컬 스크립트:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## API Examples

이 예시는 로컬 API 라우트 디버깅에 유용합니다.

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

예상 응답 형태:

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

예상 응답 형태:

```json
"Assistant response text"
```

## Development Notes

- Chat 라우트는 Edge 런타임으로 설정되어 있습니다 (`export const runtime = "edge"`).
- Whisper 라우트는 서버 측에서 실행되며 임시 저장을 위한 파일 시스템 접근이 필요합니다.
- UI는 현재 완전한 모바일 상호작용 대신 모바일 폴백 메시지를 제공합니다.
- 권한/듣는 중/생각 중 상태를 표시하기 위해 토스트 알림을 사용합니다.
- 현재 프롬프트 형태는 간결한 답변을 요구합니다 (`Your answer has to be as consise as possible.`).

## Troubleshooting

### 마이크 권한 프롬프트가 나타나지 않음

- 브라우저에서 `localhost`에 대한 마이크 접근을 허용했는지 확인하세요.
- `localhost`가 아닌 도메인에서 테스트할 때는 HTTPS를 사용하세요.

### 오디오가 재생되지 않음

- `NEXT_PUBLIC_ELEVENLABS_API_KEY` 및 `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`를 확인하세요.
- 브라우저 자동 재생/AudioContext 제한을 확인하세요(사용자 상호작용이 필요함).

### `/api/speechToText`에서 API 500 발생

- `OPENAI_API_KEY`가 설정되어 있는지 확인하세요.
- 입력이 유효한 base64 인코딩 `webm` 오디오인지 검증하세요.

### `/api/chat`에서 API 500 발생

- `OPENAI_API_KEY`와 선택적 `OPENAI_BASE_URL`이 올바른지 확인하세요.
- OpenAI 계정에서 `gpt-4o` 모델 사용 가능 여부를 확인하세요.

### 지연 시간이 높음

- 일반적으로 TTS 합성 시간이 전체 지연 시간의 대부분을 차지합니다.
- 프롬프트를 간결하게 유지하고 긴 응답은 분할을 고려하세요.

## Roadmap

현재 코드와 노트에서 유추한 잠재적 개선 사항:

- 모바일 우선 상호작용 지원(현재 데스크톱 전용 제한 대체).
- 체감 지연 시간을 줄이기 위한 부분 응답 스트리밍.
- 전사 및 TTS 실패 상황에서 더 나은 재시도/오류 UX.
- 자동화 테스트 및 CI 검사 추가.
- [`/i18n`](./i18n/) 아래 다국어 문서 확장.

## Contributing

기여는 언제나 환영하며 감사히 받습니다.

- 워크플로우와 기대 사항은 [CONTRIBUTING.md](./CONTRIBUTING.md)를 읽어주세요.
- 참여 전에 [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)를 읽어주세요.
- 버그나 기능 아이디어는 이슈를 열어주세요:
- 버그 리포트: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- 기능 요청: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## Contact

안녕하세요! 이 라이브러리를 확인하고 사용해 주셔서 감사합니다. 프로젝트 논의, 멘토링, 채용 제안, 혹은 가벼운 대화를 원하시면 언제든지 환영합니다.

이메일: `j.schoen@mail.com` 또는 Twitter: [@julianschoen](https://twitter.com/julianschoen)로 연락하실 수 있습니다.

도움을 보태고 싶다면 Buy Me A Coffee 계정도 있습니다:

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

감사합니다. 멋진 하루 보내세요 👋

## Disclaimer

Voice Assistant는 실험적 애플리케이션이며, 명시적 또는 묵시적 보증 없이 "있는 그대로" 제공됩니다. 이 소프트웨어를 사용함으로써 데이터 손실, 시스템 장애 또는 발생 가능한 기타 문제를 포함한 모든 사용 위험을 감수하는 데 동의하는 것으로 간주됩니다.

이 프로젝트의 개발자와 기여자는 본 소프트웨어 사용으로 인해 발생할 수 있는 어떠한 손실, 손해 또는 기타 결과에 대해서도 책임을 지지 않습니다. Voice Assistant가 제공하는 정보를 바탕으로 내리는 모든 결정과 행동의 책임은 전적으로 사용자 본인에게 있습니다.

GPT-4 언어 모델 사용은 토큰 사용량으로 인해 비용이 많이 들 수 있습니다. 이 프로젝트를 사용함으로써 본인의 토큰 사용량과 관련 비용을 직접 모니터링하고 관리할 책임이 있음을 인정합니다. 예상치 못한 과금을 방지하기 위해 OpenAI API 사용량을 정기적으로 확인하고 필요한 한도 또는 알림을 설정할 것을 강력히 권장합니다.

Voice Assistant를 사용함으로써, 본 소프트웨어 사용 또는 본 약관 위반으로 인해 발생하는 모든 청구, 손해, 손실, 책임, 비용 및 지출(합리적인 변호사 수임료 포함)에 대해 개발자, 기여자 및 관련 당사자를 면책하고 방어하며 피해가 없도록 하는 데 동의합니다.

<!-- LICENSE -->

## License

MIT 라이선스에 따라 배포됩니다. 자세한 내용은 `LICENSE`를 참고하세요.

저장소 참고: 이 저장소는 현재 라이선스 파일을 [`LICENCE`](./LICENCE)로 저장하고 있습니다.
