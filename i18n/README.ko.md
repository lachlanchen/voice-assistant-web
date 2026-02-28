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

<h3 align="center">Aura를 만나보세요 👋</h3>

<p align="center">
Aura는 저지연 응답에 맞춰 최적화된 브라우저 기반 Siri형 음성 비서입니다. Vercel Edge Functions, OpenAI Whisper, GPT-4o, ElevenLabs TTS 스트리밍을 사용합니다.
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

## 목차

- [📌 개요](#overview)
- [✨ 기능](#features)
- [🎥 데모](#demo)
- [🧠 제작 동기](#motivation)
- [⏱️ 지연 시간과 사용자 경험에 대한 생각](#thoughts-on-latency-and-user-experience)
- [🏗️ 아키텍처](#architecture)
- [📁 프로젝트 구조](#project-structure)
- [✅ 필수 조건](#prerequisites)
- [🧰 설치](#installation)
- [⚙️ 설정](#configuration)
- [🧪 사용법](#usage)
- [📦 API 예시](#api-examples)
- [🛠️ 개발 노트](#development-notes)
- [🧯 문제 해결](#troubleshooting)
- [🗺️ 로드맵](#roadmap)
- [❤️ Support](#%e2%9d%a4%ef%b8%8f-support)
- [🤝 기여 가이드](#contributing)
- [📬 문의](#contact)
- [⚠️ 면책 조항](#disclaimer)
- [📄 라이선스](#license)

<a name="overview"></a>
## 개요

Aura는 Next.js (App Router)와 TypeScript로 만든 브라우저 기반 Siri형 음성 비서입니다.

### 한눈에 보기

| 항목 | 상세 |
| --- | --- |
| 주요 목표 | 웹에서 빠르고 실용적인 저지연 음성 상호작용 |
| 런타임 모델 | 브라우저 캡처 + 서버 API 라우트 + Edge 채팅 엔드포인트 |
| 음성-텍스트 변환(STT) | OpenAI Whisper (`whisper-1`) |
| 음성 비서 모델 | OpenAI GPT-4o |
| 텍스트-음성 변환(TTS) | 브라우저에서 ElevenLabs 스트리밍 재생 |

상호작용 루프는 다음과 같습니다.

1. 브라우저에서 마이크 오디오를 수집합니다.
2. OpenAI Whisper (`whisper-1`)로 음성을 텍스트로 전사합니다.
3. OpenAI GPT-4o로 간결한 응답을 생성합니다.
4. ElevenLabs를 사용해 합성 오디오를 스트리밍으로 사용자에게 재생합니다.

이 프로젝트는 실용적인 저지연 UX를 중심으로 설계되었으며, 비서가 듣거나 생각하는 동안 시각적 피드백을 제공합니다.

### 시각적 요약

| 단계 | 의도 |
| --- | --- |
| 🎙️ 수집 | 브라우저 오디오 캡처 + 권한 상태를 반영한 UI |
| 🧠 처리 | Whisper 전사 + GPT-4o 응답 생성 |
| 🔉 전달 | ElevenLabs 스트리밍 재생과 상태 피드백 |

<a name="features"></a>
## 기능

| 항목 | 의미 |
| --- | --- |
| ✅ Siri형 브라우저 비서 | 간단한 웹 UI에서 음성 입출력 전체 플로우 제공 |
| ⚡ 저지연 워크플로우 | 캡처, 전사, 응답 생성, 재생 루프 최적화 |
| 🧠 LLM + TTS 스택 | OpenAI Whisper, GPT-4o, ElevenLabs 스트리밍 합성 |
| 🧩 확장 가능한 앱 구조 | 프로젝트 수준 변경으로 모델 엔드포인트 또는 음성 제공자를 교체 가능 |

추가 구현 상세:

| 포커스 영역 | 현재 동작 |
| --- | --- |
| 프레임워크 | TypeScript와 Next.js 13 App Router |
| API 런타임 | Edge 런타임 채팅 엔드포인트 (`/api/chat`) |
| UX 피드백 | 마이크 권한, 청취, 생각 상태에 대한 토스트 업데이트 |
| 상호작용 UI | 스트리밍 TTS 재생과 함께 애니메이션 assistant 버튼 |
| 네트워크 | 프록시/자가호스팅 게이트웨이용 OpenAI base URL 오버라이드 옵션 |

<a name="demo"></a>
## 데모

여기에서 Aura를 직접 테스트해 보세요: [https://voice.julianschoen.co](https://voice.julianschoen.co)

<a name="motivation"></a>
## 제작 동기

음성 비서는 이미 일상에서 중요한 역할을 합니다. 스마트폰, 차량, 집, 그리고 그 외 다양한 환경에서 사용되죠. 이런 경험을 웹으로 옮기고 반응성을 높이는 일은 오랫동안 쉽지 않았습니다.

최근까지 웹에서 음성 비서를 사용하기 가장 큰 문제는 지연 시간입니다. 오디오를 서버로 보내고 LLM 응답을 생성한 뒤 다시 음성으로 돌려받는 데 시간이 오래 걸렸기 때문입니다. OpenAI, ElevenLabs, Vercel의 최신 발전 덕분에 이제 웹에서도 실용적으로 빠른 음성 비서를 구현할 수 있게 되었습니다.

이 저장소는 자신의 음성 비서를 직접 만들고 실제 구현에서 생기는 트레이드오프를 이해하려는 사람들을 위한 출발점이 되길 목표로 합니다.

<a name="thoughts-on-latency-and-user-experience"></a>
## 지연 시간과 사용자 경험에 대한 생각

좋은 음성 UX에서 지연 시간은 가장 중요한 요소입니다. 현재는 크게 세 가지가 주요 원인입니다.

- 전사 시간 (Whisper 음성 인식)
- 응답 생성 시간 (원문에서는 GPT-4o Mini로 기재됨)
- 음성 합성 스트리밍 시간 (ElevenLabs TTS)

실사용 테스트에서 음성 생성이 보통 가장 많은 시간을 차지하며, 특히 긴 응답에서는 예측이 가장 어려운 구간으로 나타났습니다.

가능한 완화 전략은 응답을 여러 조각으로 나눠 순차적으로 스트리밍하는 것입니다. 이렇게 하면 전체 생성이 끝나기 전에도 사용자에게 일부를 먼저 들려줄 수 있습니다. 아직 구현되지는 않았지만 유망한 방향입니다.

또 다른 핵심은 지각적 대기 시간입니다. 총 지연 시간이 같아도, 처리 중 즉시 피드백이 있으면 사용자가 훨씬 참기 쉽습니다. 이 프로젝트는 현재 처리 중 "생각 중" 알림을 제공해 이를 개선하려고 합니다.

<a name="architecture"></a>
## 아키텍처

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

핵심 파일:

- `src/components/AssistantButton/AssistantButton.tsx`: 녹음 상태, 요청 오케스트레이션, 재생 처리.
- `src/app/api/speechToText/route.ts`: base64 오디오 -> `/tmp/input.webm` -> Whisper 전사.
- `src/app/api/chat/route.ts`: OpenAI 기반 채팅 완성(Chat completion) 처리.
- `src/app/page.tsx`: 데스크톱 우선 인터페이스 및 모바일 대체 메시지.

<a name="project-structure"></a>
## 프로젝트 구조

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

<a name="prerequisites"></a>
## 필수 조건

| 요구사항 | 내용 |
| --- | --- |
| Node.js | 18+ (권장: Node.js 18.17+ 또는 Next.js 13 기준 20 LTS) |
| 패키지 매니저 | npm (`package-lock.json` 사용) |
| API 접근 | OpenAI API 키 |
| TTS 접근 | ElevenLabs API 키 및 Voice ID |
| 클라이언트 | 마이크 접근이 가능한 데스크톱 브라우저 (현재 모바일 UX는 데스크톱 우선) |

<a name="installation"></a>
## 설치

1. 저장소를 클론합니다:

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. 환경변수 템플릿을 복사하고 값을 편집합니다:

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL="" # Optional
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. 의존성 설치:

```sh
npm install
```

4. 로컬 실행:

```sh
npm run dev
```

5. `http://localhost:3000`에서 앱을 엽니다.

참고: 로컬이 아닌 도메인에서 마이크 접근을 테스트할 때는 보통 HTTPS가 필요합니다.

6. Vercel에 배포:

이 프로젝트는 표준 Next.js 배포 흐름을 따릅니다. Vercel의 기본 가져오기(import) 설정을 사용하고, 동일한 환경변수를 프로젝트에 설정하세요.

<a name="configuration"></a>
## 설정

프로젝트에서 사용하는 환경 변수:

| 변수 | 필수 여부 | 설명 |
| --- | --- | --- |
| `OPENAI_API_KEY` | 예 | Whisper 전사와 GPT 채팅 완성에 사용하는 API 키 |
| `OPENAI_BASE_URL` | 아니오 | OpenAI API base URL 대체 경로(프록시/게이트웨이용) |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | 예 | 브라우저 측 TTS 요청에서 사용하는 ElevenLabs API 키 |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | 예 | TTS 합성에 사용할 ElevenLabs Voice ID |

참고사항:

- `NEXT_PUBLIC_*` 변수는 Next.js 컨벤션에 따라 클라이언트에 노출됩니다.
- `speechToText`는 현재 전사 전에 임시 오디오를 `/tmp/input.webm`에 저장합니다.

<a name="usage"></a>
## 사용법

1. 데스크톱 브라우저에서 앱을 엽니다.
2. assistant 구슬(orb)을 한 번 클릭하고 마이크 권한을 허용합니다.
3. 다시 클릭해 녹음을 시작한 뒤, 한 번 더 클릭해 중지 및 전송을 합니다.
4. Aura가 입력한 내용을 전사하고 응답을 생성한 뒤 합성 음성을 재생합니다.

로컬 스크립트:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

<a name="api-examples"></a>
## API 예시

다음 예시는 로컬 API 라우트를 디버깅할 때 유용합니다.

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

예상 응답 형식:

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

예상 응답 형식:

```json
"Assistant response text"
```

<a name="development-notes"></a>
## 개발 노트

- Chat 라우트는 Edge 런타임으로 구성되어 있습니다 (`export const runtime = "edge"`).
- Whisper 라우트는 서버 측에서 실행되며 임시 저장을 위해 파일 시스템 접근이 필요합니다.
- 현재 UI는 모바일 전체 상호작용 대신 모바일 대체 메시지를 제공합니다.
- 토스트 알림을 통해 마이크 권한, 청취, 사고(생각) 상태를 표시합니다.
- 현재 프롬프트 구성은 간결한 답변을 요구합니다 (`Your answer has to be as concise as possible.`).
- 런타임 로그, 요청 추적성(request traceability), 스트리밍 동작은 현재 CI에서 검증되지 않았습니다(레포지토리에 자동 테스트 스위트가 없음).

<a name="troubleshooting"></a>
## 문제 해결

### 🎤 마이크 권한 프롬프트가 나타나지 않음

- 브라우저가 `localhost`에서 마이크 접근을 허용하는지 확인하세요.
- 비로컬 도메인에서는 HTTPS를 사용하세요.

### 🔈 오디오 재생이 되지 않음

- `NEXT_PUBLIC_ELEVENLABS_API_KEY`와 `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`를 확인하세요.
- 브라우저의 자동재생/audio-context 제약 조건(사용자 상호작용 필요)을 확인하세요.

### 📡 `/api/speechToText`에서 API 500 오류

- `OPENAI_API_KEY`가 설정되어 있는지 확인하세요.
- 입력 데이터가 유효한 base64 인코딩 `webm` 오디오인지 확인하세요.

### 📡 `/api/chat`에서 API 500 오류

- `OPENAI_API_KEY`와 선택 항목인 `OPENAI_BASE_URL`가 정확한지 확인하세요.
- OpenAI 계정에서 `gpt-4o` 모델이 사용 가능한지 확인하세요.

### ⏳ 지연 시간 높음

- TTS 합성 시간은 보통 전체 지연 시간에서 가장 큰 비중을 차지합니다.
- 프롬프트를 간결하게 유지하고 긴 응답은 분할을 고려하세요.

<a name="roadmap"></a>
## 로드맵

현재 코드와 노트에서 추정되는 다음 개선 항목:

- 모바일 우선 상호작용 지원 (현재 데스크톱 전용 제약 교체)
- 부분 응답 스트리밍으로 지각적 지연 시간 감소
- 전사 및 TTS 실패 시 재시도/오류 UX 개선
- 자동화 테스트 및 CI 점검 추가
- [`/i18n`](./i18n/) 아래 다국어 문서 확장

## 기여 가이드

기여는 언제나 환영하며, 감사히 받습니다.

- 작업 방식과 기대사항은 [CONTRIBUTING.md](./CONTRIBUTING.md)를 읽어 주세요.
- 참여하기 전에 [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md)를 읽어 주세요.
- 버그나 기능 아이디어는 이슈를 열어주세요.
- 버그 보고: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- 기능 요청: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

<a name="contact"></a>
## 문의

안녕하세요! 이 라이브러리를 확인하고 사용해 주셔서 감사합니다. 프로젝트에 대해 이야기하고 싶거나 멘토링이 필요하거나 고용 제안을 고려 중이거나, 그냥 인사하고 싶으시다면 언제든 편하게 연락주세요.

이메일로 연락할 수 있습니다: `j.schoen@mail.com` 또는 트위터에서 메시지 보내기: [@julianschoen](https://twitter.com/julianschoen)

기부를 고려해 주신다면 Buy Me A Coffee 계정이 있습니다:

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

좋은 하루 보내세요 👋

<a name="disclaimer"></a>
## 면책 조항

Voice Assistant는 실험적인 애플리케이션이며, 명시적이든 묵시적이든 어떠한 보증 없이 "있는 그대로" 제공됩니다. 이 소프트웨어를 사용하면 데이터 손실, 시스템 장애, 기타 발생 가능 이슈를 포함해 사용과 관련된 모든 위험을 스스로 부담한다는 데 동의하는 것입니다.

이 프로젝트의 개발자와 기여자들은 이 소프트웨어 사용으로 인해 발생한 손실, 손해, 기타 결과에 대해 어떠한 책임도지지 않습니다. Voice Assistant가 제공한 정보를 바탕으로 한 판단과 행동의 책임은 전적으로 사용자에게 있습니다.

GPT-4 언어 모델은 토큰 사용량으로 인해 비용이 높을 수 있습니다. 이 프로젝트를 사용하면 사용량과 비용을 스스로 모니터링하고 관리할 책임이 있음을 인정한 것입니다. 예기치 못한 과금 방지를 위해 OpenAI API 사용량을 정기적으로 확인하고 필요한 한도/알림을 설정하는 것을 강력히 권장합니다.

Voice Assistant를 사용함으로써 사용자는 본 소프트웨어의 사용 또는 본 약관 위반으로 인해 발생하는 모든 청구, 손해, 손실, 책임, 비용 및 지출(합리적인 변호사 비용 포함)로부터 개발자, 기여자, 관련 당사자를 면책하고 방어하며 무해하게 유지할 것에 동의합니다.

<!-- LICENSE -->

<a name="license"></a>
## 라이선스

MIT 라이선스 하에 배포됩니다. 자세한 내용은 `LICENSE`를 확인하세요.

참고: 이 저장소는 라이선스 파일을 [`LICENCE`](./LICENCE)로 저장합니다.


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
