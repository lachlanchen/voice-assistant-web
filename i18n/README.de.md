[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


<a name="readme-top"></a>

<br />
<div align="center">

<h3 align="center">Sag Hallo zu Aura 👋</h3>

<p align="center">
Aura ist ein intelligenter Sprachassistent, optimiert für Antworten mit niedriger Latenz. Er nutzt Vercel Edge Functions, Whisper-Spracherkennung, GPT-4o und ElevenLabs-TTS-Streaming.
<br />
<br />
<a href="https://voice.julianschoen.co">Demo ansehen</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=">Bug melden</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=">Feature anfragen</a>
</p>

<p align="center">
<a href="https://github.com/ntegrals/aura-voice"><img alt="Repo" src="https://img.shields.io/badge/GitHub-ntegrals%2Faura--voice-181717?logo=github" /></a>
<a href="https://nextjs.org/"><img alt="Next.js" src="https://img.shields.io/badge/Next.js-13.4.13-black?logo=next.js" /></a>
<a href="https://www.typescriptlang.org/"><img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-5.1-3178C6?logo=typescript&logoColor=white" /></a>
<a href="https://openai.com/"><img alt="OpenAI" src="https://img.shields.io/badge/OpenAI-GPT--4o%20%2B%20Whisper-10A37F" /></a>
<a href="https://elevenlabs.io/"><img alt="ElevenLabs" src="https://img.shields.io/badge/ElevenLabs-TTS%20Streaming-222222" /></a>
<a href="https://vercel.com/"><img alt="Vercel Edge" src="https://img.shields.io/badge/Vercel-Edge%20Runtime-000000?logo=vercel" /></a>
<a href="./LICENCE"><img alt="Lizenz" src="https://img.shields.io/badge/License-MIT-22C55E.svg" /></a>
</p>

</div>

<a href="https://github.com/ntegrals/aura-voice">
<img src=".assets//header.png" alt="Logo">
</a>

## Inhaltsverzeichnis

- [Überblick](#überblick)
- [Features](#features)
- [Demo](#demo)
- [Motivation](#motivation)
- [Gedanken zu Latenz und Benutzererlebnis](#gedanken-zu-latenz-und-benutzererlebnis)
- [Architektur](#architektur)
- [Projektstruktur](#projektstruktur)
- [Voraussetzungen](#voraussetzungen)
- [Installation](#installation)
- [Konfiguration](#konfiguration)
- [Verwendung](#verwendung)
- [API-Beispiele](#api-beispiele)
- [Entwicklungshinweise](#entwicklungshinweise)
- [Fehlerbehebung](#fehlerbehebung)
- [Roadmap](#roadmap)
- [Mitwirken](#mitwirken)
- [Kontakt](#kontakt)
- [Haftungsausschluss](#haftungsausschluss)
- [Lizenz](#lizenz)

## Überblick

Aura ist ein browserbasierter, Siri-ähnlicher Sprachassistent, der mit Next.js (App Router) und TypeScript entwickelt wurde.

### Auf einen Blick

| Bereich | Details |
| --- | --- |
| Hauptziel | Schnelle, praktische Sprachinteraktion mit niedriger Latenz im Web |
| Laufzeitmodell | Browser-Aufnahme + Server-API-Routen + Edge-Chat-Endpunkt |
| Speech-to-Text | OpenAI Whisper (`whisper-1`) |
| Assistentenmodell | OpenAI GPT-4o |
| Text-to-Speech | ElevenLabs-Streaming-Wiedergabe im Browser |

Der Interaktionszyklus ist:

1. Mikrofon-Audio im Browser erfassen.
2. Sprache mit OpenAI Whisper (`whisper-1`) transkribieren.
3. Eine prägnante Antwort mit OpenAI GPT-4o erzeugen.
4. Synthetisiertes Audio per ElevenLabs an den Nutzer zurückstreamen.

Das Projekt ist auf eine praxisnahe UX mit niedriger Latenz optimiert, inklusive visuellem Feedback, während der Assistent zuhört oder nachdenkt.

## Features

✅ Ein Siri-ähnlicher Sprachassistent direkt im Browser  
✅ Optimiert für Antworten mit niedriger Latenz  
✅ Entwickelt mit OpenAI, Whisper-Spracherkennung und ElevenLabs

Zusätzliche Implementierungsdetails:

- Next.js 13 App Router mit TypeScript.
- Edge-Runtime-Chat-Endpunkt (`/api/chat`).
- Toast-basiertes Interaktionsfeedback (Mikrofonberechtigung, Zuhören, Nachdenken).
- Animierter Assistenten-Button mit Streaming-TTS-Wiedergabe.
- Optionale OpenAI-Base-URL-Überschreibung für Proxy-/Self-Hosted-Gateway-Setups.

## Demo

Du kannst Aura hier testen: [https://voice.julianschoen.co](https://voice.julianschoen.co)

## Motivation

Sprachassistenten sind ein fester Bestandteil des Alltags geworden: auf Smartphones, im Auto, zu Hause und mehr. Diese Erfahrung mit guter Reaktionsgeschwindigkeit ins Web zu bringen, war historisch schwierig.

Bis vor Kurzem war Latenz das Hauptproblem von Sprachassistenten im Web. Das Senden von Audio an den Server, das Erzeugen einer LLM-Antwort und das Zurückstreamen von Sprache dauerten zu lange. Jüngste Fortschritte bei OpenAI, ElevenLabs und Vercel ermöglichen es, einen Sprachassistenten zu bauen, der im Web schnell genug für die Praxis ist.

Dieses Repository soll eine zentrale Anlaufstelle für alle sein, die ihren eigenen Sprachassistenten bauen und die Trade-offs realer Implementierungen verstehen wollen.

## Gedanken zu Latenz und Benutzererlebnis

Latenz ist der wichtigste Faktor für eine gute Voice-UX. Aktuell gibt es drei Hauptbeiträge:

- Transkriptionszeit (Whisper-Spracherkennung).
- Zeit für die Antwortgenerierung (GPT-4o Mini in den ursprünglichen Projektnotizen).
- Streaming-Zeit der Sprachsynthese (ElevenLabs TTS).

Aus praktischen Testnotizen geht hervor, dass die Spracherzeugung in der Regel am meisten Zeit kostet und am wenigsten vorhersagbar ist, insbesondere bei längeren Antworten.

Eine mögliche Gegenmaßnahme ist, die Antwort in mehrere Teile aufzuteilen und nacheinander zu streamen. So kann der Nutzer früher mit dem Zuhören beginnen, während der Rest noch erzeugt wird. Das ist aktuell noch nicht implementiert, aber ein vielversprechender Ansatz.

Ein weiteres Schlüsselkonzept ist die wahrgenommene Wartezeit. Selbst wenn die Gesamtlatenz unverändert ist, tolerieren Nutzer Verzögerungen besser, wenn sie sofortiges Feedback erhalten. Das Projekt enthält derzeit eine "thinking"-Benachrichtigung während der Verarbeitung, um die wahrgenommene Reaktionsgeschwindigkeit zu verbessern.

## Architektur

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

Wichtige Dateien:

- `src/components/AssistantButton/AssistantButton.tsx`: Aufnahmestatus, Request-Orchestrierung, Wiedergabe.
- `src/app/api/speechToText/route.ts`: base64-Audio -> `/tmp/input.webm` -> Whisper-Transkription.
- `src/app/api/chat/route.ts`: Chat-Completion via OpenAI.
- `src/app/page.tsx`: Desktop-First-Oberfläche und Mobile-Fallback-Nachricht.

## Projektstruktur

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

## Voraussetzungen

- Node.js 18+ (empfohlen: Node.js 18.17+ oder 20 LTS für Next.js 13).
- npm (das Projekt nutzt `package-lock.json`).
- OpenAI API key.
- ElevenLabs API key und Voice ID.
- Ein Desktop-Browser mit Mikrofonzugriff (die mobile UX ist aktuell designbedingt eingeschränkt).

## Installation

1. Repository klonen:

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. API-Keys von [https://openai.com/](https://openai.com/) und [https://elevenlabs.com/](https://elevenlabs.com/) holen.

Die Datei `.env.example` nach `.env.local` kopieren und deine Keys eintragen:

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL=(Optional)
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. Abhängigkeiten installieren:

```sh
npm install
```

4. App lokal starten:

```sh
npm run dev
```

5. Auf Vercel deployen:

Dieses Projekt ist mit dem standardmäßigen Vercel-Deployment-Flow für Next.js kompatibel.

## Konfiguration

Von diesem Projekt verwendete Umgebungsvariablen:

| Variable | Erforderlich | Beschreibung |
| --- | --- | --- |
| `OPENAI_API_KEY` | Ja | API key für Whisper-Transkription und GPT-Chat-Completion. |
| `OPENAI_BASE_URL` | Nein | Optionale Überschreibung der OpenAI-API-Basis-URL (Proxy/Gateway). |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Ja | ElevenLabs API key, der für die browserseitige TTS-Anfrage genutzt wird. |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Ja | ElevenLabs Voice ID für TTS-Synthese. |

Hinweise:

- `NEXT_PUBLIC_*`-Variablen werden gemäß Next.js-Konventionen für den Client verfügbar gemacht.
- `speechToText` schreibt derzeit temporäres Audio nach `/tmp/input.webm`, bevor transkribiert wird.

## Verwendung

1. App in einem Desktop-Browser öffnen.
2. Einmal auf die Assistenten-Kugel klicken und Mikrofonberechtigungen gewähren.
3. Erneut klicken, um die Aufnahme zu starten, dann noch einmal klicken, um zu stoppen und zu senden.
4. Aura transkribiert deine Eingabe, erzeugt eine Antwort und spielt anschließend synthetisierte Sprache ab.

Lokale Skripte:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## API-Beispiele

Diese Beispiele sind nützlich zum Debuggen lokaler API-Routen.

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

Erwartete Antwortstruktur:

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

Erwartete Antwortstruktur:

```json
"Assistant response text"
```

## Entwicklungshinweise

- Die Chat-Route ist für Edge Runtime konfiguriert (`export const runtime = "edge"`).
- Die Whisper-Route läuft serverseitig und hängt für temporäre Speicherung vom Dateisystemzugriff ab.
- Die UI zeigt aktuell eine Mobile-Fallback-Nachricht statt einer vollständigen mobilen Interaktion.
- Toast-Benachrichtigungen zeigen die Zustände Berechtigung/Zuhören/Nachdenken.
- Das aktuelle Prompt-Shaping fordert prägnante Antworten (`Your answer has to be as consise as possible.`).

## Fehlerbehebung

### Mikrofon-Berechtigungsabfrage erscheint nicht

- Stelle sicher, dass dein Browser Mikrofonzugriff für `localhost` erlaubt.
- Nutze HTTPS beim Testen auf Nicht-`localhost`-Domains.

### Keine Audio-Wiedergabe

- Prüfe `NEXT_PUBLIC_ELEVENLABS_API_KEY` und `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`.
- Prüfe Browser-Beschränkungen für Autoplay/AudioContext (Nutzerinteraktion ist erforderlich).

### API 500 von `/api/speechToText`

- Prüfe, ob `OPENAI_API_KEY` gesetzt ist.
- Stelle sicher, dass die Eingabe gültiges base64-kodiertes `webm`-Audio enthält.

### API 500 von `/api/chat`

- Prüfe, ob `OPENAI_API_KEY` und optional `OPENAI_BASE_URL` korrekt sind.
- Prüfe die Modellverfügbarkeit für `gpt-4o` in deinem OpenAI-Konto.

### Hohe Latenz

- TTS-Synthesezeit dominiert normalerweise die Ende-zu-Ende-Latenz.
- Halte Prompts kurz und erwäge, lange Antworten aufzuteilen.

## Roadmap

Potenzielle nächste Verbesserungen, abgeleitet aus aktuellem Code und Notizen:

- Mobile-First-Interaktionssupport (ersetzt die aktuelle Desktop-Only-Begrenzung).
- Streaming partieller Assistenten-Antworten zur Reduktion der wahrgenommenen Latenz.
- Bessere Retry-/Error-UX bei Transkriptions- und TTS-Fehlern.
- Automatisierte Tests und CI-Checks ergänzen.
- Mehrsprachige Dokumentation unter [`/i18n`](./i18n/) erweitern.

## Mitwirken

Beiträge sind willkommen und geschätzt.

- Lies [CONTRIBUTING.md](./CONTRIBUTING.md) für Workflow und Erwartungen.
- Lies [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md), bevor du mitwirkst.
- Eröffne Issues für Bugs oder Feature-Ideen:
- Bug report: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- Feature request: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## Kontakt

Hi! Danke, dass du diese Library ansiehst und nutzt. Wenn du dein Projekt besprechen möchtest, Mentoring brauchst, eine Zusammenarbeit erwägst oder einfach chatten willst, freue ich mich auf den Austausch.

Du kannst mir eine E-Mail senden: `j.schoen@mail.com` oder mir auf Twitter schreiben: [@julianschoen](https://twitter.com/julianschoen)

Wenn du etwas zurückgeben möchtest, habe ich einen Buy Me A Coffee Account:

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

Danke und hab einen großartigen Tag 👋

## Haftungsausschluss

Voice Assistant ist eine experimentelle Anwendung und wird "wie besehen" ohne jegliche ausdrückliche oder stillschweigende Gewähr bereitgestellt. Mit der Nutzung dieser Software erklärst du dich damit einverstanden, alle mit der Nutzung verbundenen Risiken zu tragen, einschließlich, aber nicht beschränkt auf Datenverlust, Systemausfälle oder andere Probleme, die auftreten können.

Die Entwickler und Mitwirkenden dieses Projekts übernehmen keine Verantwortung oder Haftung für Verluste, Schäden oder sonstige Folgen, die durch die Nutzung dieser Software entstehen können. Du bist allein verantwortlich für alle Entscheidungen und Handlungen, die auf Basis der von Voice Assistant bereitgestellten Informationen getroffen werden.

Bitte beachte, dass die Nutzung des GPT-4-Sprachmodells aufgrund des Token-Verbrauchs teuer sein kann. Durch die Nutzung dieses Projekts bestätigst du, dass du selbst für die Überwachung und Verwaltung deines Token-Verbrauchs und der damit verbundenen Kosten verantwortlich bist. Es wird dringend empfohlen, deine OpenAI-API-Nutzung regelmäßig zu prüfen und notwendige Limits oder Alerts einzurichten, um unerwartete Kosten zu vermeiden.

Mit der Nutzung von Voice Assistant erklärst du dich einverstanden, die Entwickler, Mitwirkenden und alle verbundenen Parteien von sämtlichen Ansprüchen, Schäden, Verlusten, Verbindlichkeiten, Kosten und Aufwendungen (einschließlich angemessener Anwaltsgebühren) freizustellen, zu verteidigen und schadlos zu halten, die aus deiner Nutzung dieser Software oder aus einem Verstoß gegen diese Bedingungen entstehen.

<!-- LICENSE -->

## Lizenz

Veröffentlicht unter der MIT-Lizenz. Weitere Informationen unter `LICENSE`.

Hinweis zum Repository: Dieses Repository speichert die Lizenzdatei derzeit als [`LICENCE`](./LICENCE).
