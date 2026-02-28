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

<h3 align="center">Sag Hallo zu Aura 👋</h3>

<p align="center">
Aura ist ein browserbasierter, Siri-ähnlicher Sprachassistent mit optimierter Latenz. Er nutzt Vercel Edge Functions, Whisper Spracherkennung, GPT-4o und ElevenLabs TTS-Streaming.
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

## Inhaltsverzeichnis

- [📌 Überblick](#überblick)
- [✨ Funktionen](#funktionen)
- [🎥 Demo](#demo)
- [🧠 Motivation](#motivation)
- [⏱️ Gedanken zur Latenz und Benutzererfahrung](#gedanken-zur-latenz-und-benutzererfahrung)
- [🏗️ Architektur](#architektur)
- [📁 Projektstruktur](#projektstruktur)
- [✅ Voraussetzungen](#voraussetzungen)
- [🧰 Installation](#installation)
- [⚙️ Konfiguration](#konfiguration)
- [🧪 Nutzung](#nutzung)
- [📦 API Beispiele](#api-beispiele)
- [🛠️ Entwicklungsnotizen](#entwicklungsnotizen)
- [🧯 Fehlerbehebung](#fehlerbehebung)
- [🗺️ Roadmap](#roadmap)
- [🤝 Mitwirken](#mitwirken)
- [❤️ Support](#%e2%9d%a4%ef%b8%8f-support)
- [📬 Kontakt](#kontakt)
- [⚠️ Haftungsausschluss](#haftungsausschluss)
- [📄 Lizenz](#lizenz)

## Überblick

Aura ist ein browserbasierter, Siri-ähnlicher Sprachassistent, der mit Next.js (App Router) und TypeScript gebaut wurde.

### Auf einen Blick

| Bereich | Details |
| --- | --- |
| Hauptziel | Schnelle, praktische Sprachinteraktion im Web mit geringer Latenz |
| Laufzeitmodell | Browser-Aufnahme + Server-API-Routen + Edge-Chat-Endpunkt |
| Spracherkennung | OpenAI Whisper (`whisper-1`) |
| Assistentenmodell | OpenAI GPT-4o |
| Text-zu-Sprache | ElevenLabs-Streaming-Wiedergabe im Browser |

Der Interaktionsablauf ist:

1. Mikrofon-Audio im Browser erfassen.
2. Sprache mit OpenAI Whisper (`whisper-1`) transkribieren.
3. Eine prägnante Antwort mit OpenAI GPT-4o generieren.
4. Das synthetisierte Audio per ElevenLabs zurück an den Nutzer streamen.

Das Projekt ist auf eine praxisnahe UX mit niedriger Latenz optimiert – mit visuellem Feedback während der Assistent zuhört oder „nachdenkt“.

### Visuelle Zusammenfassung

| Phase | Bedeutung |
| --- | --- |
| 🎙️ Aufnahme | Browser-Audioaufnahme + Zustände der UI entsprechend der Berechtigungen |
| 🧠 Verarbeitung | Whisper-Transkription + GPT-4o-Response-Generierung |
| 🔉 Ausgabe | ElevenLabs Streaming-Wiedergabe mit Status-Feedback |

## Funktionen

| Fähigkeit | Bedeutung |
| --- | --- |
| ✅ Siri-ähnlicher Browserassistent | Volle Sprach-Ein-/Ausgabe in einer einfachen Web-UI |
| ⚡ Niedrige Latenz im Workflow | Optimierter Ablauf aus Aufnahme, Transkription, Completion und Wiedergabe |
| 🧠 LLM + TTS-Stack | OpenAI Whisper, GPT-4o und ElevenLabs Streaming-Synthese |
| 🧩 Erweiterbare App-Architektur | Tauschen Sie Modell-Endpunkt oder Sprachprovider auf Projektebene aus |

Zusätzliche Implementierungsdetails:

| Fokusbereich | Aktuelles Verhalten |
| --- | --- |
| Framework | Next.js 13 App Router mit TypeScript |
| API-Laufzeit | Edge-runtime Chat-Endpunkt (`/api/chat`) |
| UX-Feedback | Toast-Benachrichtigungen für Mikrofonrecht, Aufnahme und Denkzustand |
| Interaktions-UI | Animierter Assistent-Button mit Streaming-TTS-Wiedergabe |
| Netzwerk | Optionaler OpenAI-Basis-URL-Override für Proxy-/Self-Hosting-Gateway-Setups |

## Demo

Testen Sie Aura hier: [https://voice.julianschoen.co](https://voice.julianschoen.co)

## Motivation

Sprachassistenten sind aus dem Alltag nicht mehr wegzudenken: auf Smartphones, im Auto, im Zuhause und darüber hinaus. Diese Erfahrung mit guter Reaktionsgeschwindigkeit ins Web zu bringen, war lange schwierig.

Bis vor kurzem lag das Hauptproblem webbasierter Sprachassistenten in der Latenz. Es dauerte zu lange, Audio zum Server zu senden, eine LLM-Vervollständigung zu erzeugen und Sprache zurückzustreamen. Fortschritte von OpenAI, ElevenLabs und Vercel machen es nun möglich, einen Sprachassistenten im Browser zu bauen, der schnell genug ist, um praktisch eingesetzt zu werden.

Dieses Repository soll ein zentraler Ort für Menschen sein, die ihren eigenen Sprachassistenten bauen möchten und die Kompromisse realer Implementierungen nachvollziehen wollen.

## Gedanken zur Latenz und Benutzererfahrung

Latenz ist der wichtigste Faktor für eine gute Sprach-UX. Aktuell gibt es drei Hauptfaktoren:

- Transkriptionszeit (Spracherkennung mit Whisper).
- Zeit für die Antwortgenerierung (im ursprünglichen Projektvermerk: GPT-4o Mini).
- Zeit für die Sprachsynthese-Übertragung (ElevenLabs TTS).

Aus praktischen Tests zeigt sich, dass die Sprachgenerierung meist am längsten dauert und am wenigsten vorhersehbar ist, besonders bei längeren Antworten.

Eine mögliche Gegenmaßnahme ist das Aufteilen der Antwort in mehrere Teile und deren sequentielles Streaming. So kann der Nutzer früher mit dem Hören beginnen, während der Rest noch erzeugt wird. Das ist noch nicht implementiert, aber ein vielversprechender Ansatz.

Ein weiterer zentraler Punkt ist die wahrgenommene Wartezeit. Selbst bei fixer Gesamtlatenz tolerieren Nutzende Verzögerungen besser, wenn sie sofort Feedback erhalten. Das Projekt zeigt derzeit während der Verarbeitung eine „Denkt“-Benachrichtigung, um die wahrgenommene Reaktionsfähigkeit zu verbessern.

## Architektur

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

Schlüsseldateien:

- `src/components/AssistantButton/AssistantButton.tsx`: Aufnahmezustand, Anfrage-Orchestrierung, Wiedergabe.
- `src/app/api/speechToText/route.ts`: base64-Audio -> `/tmp/input.webm` -> Whisper-Transkription.
- `src/app/api/chat/route.ts`: Chat Completion über OpenAI.
- `src/app/page.tsx`: Desktop-zentrierte Oberfläche und Mobile-Fallback-Hinweis.

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

| Anforderung | Details |
| --- | --- |
| Node.js | 18+ (empfohlen: Node.js 18.17+ oder 20 LTS für Next.js 13) |
| Paketmanager | npm (Projekt nutzt `package-lock.json`) |
| API-Zugang | OpenAI API Key |
| TTS-Zugang | ElevenLabs API Key und Voice ID |
| Client | Desktop-Browser mit Mikrofonzugriff (Mobile UX ist aktuell Desktop-zentriert) |

## Installation

1. Repository klonen:

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. Umgebungsvorlage kopieren und Werte setzen:

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL="" # Optional
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

5. App unter `http://localhost:3000` öffnen.

Annahme: Beim Testen von Mikrofonzugriff auf Nicht-Lokal-Domains ist HTTPS meist erforderlich.

6. Deployment auf Vercel:

Dieses Projekt folgt einem standardmäßigen Next.js-Deployment-Prozess. Verwenden Sie Vercels Standardeinstellungen und setzen Sie im Projekt dieselben Umgebungsvariablen.

## Konfiguration

Von diesem Projekt genutzte Umgebungsvariablen:

| Variable | Erforderlich | Beschreibung |
| --- | --- | --- |
| `OPENAI_API_KEY` | Ja | API-Schlüssel für Whisper-Transkription und GPT-Chat-Completion. |
| `OPENAI_BASE_URL` | Nein | Optionaler Override für die OpenAI-API-Basis-URL (Proxy/Gateway). |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Ja | ElevenLabs-API-Key für TTS-Anfragen im Browser. |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Ja | ElevenLabs Voice ID für TTS-Synthese. |

Hinweise:

- `NEXT_PUBLIC_*`-Variablen werden vom Next.js-Konventionsmodell auf der Client-Seite verfügbar gemacht.
- `speechToText` schreibt Audio zunächst temporär nach `/tmp/input.webm`, bevor die Transkription stattfindet.

## Nutzung

1. Öffnen Sie die App in einem Desktop-Browser.
2. Klicken Sie einmal auf den Assistenten-Orb und erteilen Sie Mikrofonberechtigungen.
3. Klicken Sie erneut, um die Aufnahme zu starten, dann erneut, um zu stoppen und zu senden.
4. Aura transkribiert die Eingabe, erzeugt eine Antwort und spielt synthetisierte Sprache ab.

Lokale Skripte:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## API Beispiele

Diese Beispiele sind hilfreich beim Debugging lokaler API-Routen.

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

Erwartete Antwortform:

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

Erwartete Antwortform:

```json
"Assistant response text"
```

## Entwicklungsnotizen

- Der Chat-Endpunkt ist für die Edge Runtime konfiguriert (`export const runtime = "edge"`).
- Die Whisper-Route läuft serverseitig und benötigt Dateisystemzugriff für temporäre Speicherung.
- Die UI zeigt derzeit einen mobilen Fallback-Hinweis statt vollständiger Mobile-Interaktion.
- Toast-Benachrichtigungen machen Berechtigungs-, Aufnahme- und Denkzustände sichtbar.
- Aktuelles Prompting fordert kurze Antworten (`Your answer has to be as concise as possible.`).
- Laufzeit-Logs, Nachvollziehbarkeit von Requests und Streaming-Verhalten sind aktuell in CI nicht getestet (kein automatisiertes Test-Setup im Repo).

## Fehlerbehebung

### 🎤 Meldung für Mikrofonberechtigung fehlt

- Stellen Sie sicher, dass Ihr Browser den Mikrofonzugriff für `localhost` erlaubt.
- Verwenden Sie HTTPS beim Testen auf Nicht-Localhost-Domains.

### 🔈 Kein Audio wird wiedergegeben

- Prüfen Sie `NEXT_PUBLIC_ELEVENLABS_API_KEY` und `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`.
- Prüfen Sie Browser-Autoplay-/AudioContext-Einschränkungen (eine Nutzerinteraktion ist erforderlich).

### 📡 API 500 von `/api/speechToText`

- Vergewissern Sie sich, dass `OPENAI_API_KEY` gesetzt ist.
- Prüfen Sie, dass die Eingabe gültiges Base64-kodiertes `webm`-Audio enthält.

### 📡 API 500 von `/api/chat`

- Vergewissern Sie sich, dass `OPENAI_API_KEY` und optional `OPENAI_BASE_URL` korrekt sind.
- Prüfen Sie die Modellverfügbarkeit für `gpt-4o` in Ihrem OpenAI-Account.

### ⏳ Hohe Latenz

- Die TTS-Synthesezeit dominiert meist die End-to-End-Latenz.
- Halten Sie Prompts kurz und überlegen Sie, lange Antworten aufzuteilen.

## Roadmap

Mögliche nächste Verbesserungen laut aktuellem Code und den Notizen:

- Mobile-First-Interaktion (ersetzt die aktuelle Desktop-Only-Einschränkung).
- Streaming von Teilantworten des Assistenten, um die wahrgenommene Latenz zu senken.
- Bessere Retry-/Fehler-UX bei Transkriptions- und TTS-Fehlern.
- Automatisierte Tests und CI-Prüfungen hinzufügen.
- Multilinguale Dokumentation unter [`/i18n`](./i18n/) erweitern.

## Mitwirken

Beiträge sind willkommen und sehr willkommen.

- Lesen Sie [CONTRIBUTING.md](./CONTRIBUTING.md) für den Ablauf und die Erwartungen.
- Lesen Sie [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md), bevor Sie mitmachen.
- Öffnen Sie Issues für Fehler oder Feature-Ideen:
  - Bug report: [Template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
  - Feature request: [Template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## Kontakt

Hi! Danke, dass Sie sich diese Bibliothek ansehen und nutzen. Wenn Sie Ihr Projekt besprechen möchten, Mentorship suchen, mich beauftragen möchten oder einfach nur chatten wollen, freue ich mich auf Ihre Nachricht.

Sie können mir eine E-Mail senden: `j.schoen@mail.com` oder mich auf Twitter kontaktieren: [@julianschoen](https://twitter.com/julianschoen)

Wenn Sie etwas zurückgeben möchten, habe ich ein Buy Me A Coffee Profil:

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

Vielen Dank und einen tollen Tag 👋

## Disclaimer

Voice Assistant ist eine experimentelle Anwendung und wird „wie besehen“ ohne jegliche ausdrückliche oder stillschweigende Gewährleistung bereitgestellt. Durch die Nutzung dieser Software akzeptieren Sie das volle Risiko ihrer Verwendung, einschließlich, aber nicht beschränkt auf Datenverlust, Systemausfälle oder sonstige aufkommende Probleme.

Die Entwickler und Beitragenden dieses Projekts übernehmen keine Verantwortung oder Haftung für Verluste, Schäden oder andere Folgen, die aus der Nutzung dieser Software entstehen können. Sie tragen allein die Verantwortung für Entscheidungen und Handlungen, die auf von Voice Assistant bereitgestellten Informationen beruhen.

Bitte beachten Sie, dass die Nutzung des GPT-4-Sprachmodells teuer sein kann, da die Token-Nutzung entsprechend Kosten verursacht. Durch die Nutzung dieses Projekts bestätigen Sie, dass Sie Ihren eigenen Tokenverbrauch und die damit verbundenen Kosten selbst überwachen und steuern. Es wird dringend empfohlen, die Nutzung der OpenAI API regelmäßig zu prüfen und bei Bedarf Limits oder Benachrichtigungen einzurichten, um unerwartete Gebühren zu vermeiden.

Durch die Nutzung von Voice Assistant erklären Sie sich damit einverstanden, Entwickler, Beitragende und verbundene Parteien von allen Ansprüchen, Schäden, Verlusten, Haftungsfällen, Kosten und Ausgaben (einschließlich angemessener Anwaltskosten) freizustellen, zu verteidigen und schadlos zu halten, die sich aus der Nutzung dieser Software oder aus der Verletzung dieser Bedingungen ergeben.

<!-- LICENSE -->

## Lizenz

Veröffentlicht unter der MIT-Lizenz. Weitere Informationen finden Sie in `LICENSE`.

Repository-Hinweis: Diese Repository speichert derzeit die Lizenzdatei als [`LICENCE`](./LICENCE).


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
