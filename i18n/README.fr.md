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

<h3 align="center">Salut, voici Aura 👋</h3>

<p align="center">
Aura est un assistant vocal de type Siri, fonctionnant dans le navigateur, optimisé pour des réponses à faible latence. Il utilise Vercel Edge Functions, la reconnaissance vocale Whisper, GPT-4o et le streaming TTS d'ElevenLabs.
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

## Table des matières

- [📌 Vue d'ensemble](#overview)
- [✨ Fonctionnalités](#features)
- [🎥 Démo](#demo)
- [🧠 Motivation](#motivation)
- [⏱️ Réflexions sur la latence et l'expérience utilisateur](#latence-et-experience-utilisateur)
- [🏗️ Architecture](#architecture)
- [📁 Structure du projet](#project-structure)
- [✅ Prérequis](#prerequisites)
- [🧰 Installation](#installation)
- [⚙️ Configuration](#configuration)
- [🧪 Utilisation](#utilisation)
- [📦 Exemples d'API](#api-examples)
- [🛠️ Notes de développement](#development-notes)
- [🧯 Dépannage](#troubleshooting)
- [🗺️ Feuille de route](#roadmap)
- [🤝 Contribution](#contributing)
- [❤️ Support](#support)
- [📬 Contact](#contact)
- [⚠️ Avertissement](#disclaimer)
- [📄 Licence](#license)

## Vue d'ensemble <a id="overview"></a>

Aura est un assistant vocal de type Siri, basé sur le navigateur et construit avec Next.js (App Router) et TypeScript.

### En bref

| Domaine | Détails |
| --- | --- |
| Objectif principal | Interaction vocale rapide, pratique et à faible latence sur le web |
| Modèle d'exécution | Capture dans le navigateur + routes API serveur + endpoint de chat Edge |
| Reconnaissance vocale | OpenAI Whisper (`whisper-1`) |
| Modèle d'assistant | OpenAI GPT-4o |
| Synthèse vocale | Lecture en streaming ElevenLabs dans le navigateur |

La boucle d'interaction est :

1. Capturer l'audio du microphone dans le navigateur.
2. Transcrire la parole avec OpenAI Whisper (`whisper-1`).
3. Générer une réponse concise avec OpenAI GPT-4o.
4. Renvoyer l'audio synthétique en streaming vers l'utilisateur via ElevenLabs.

Le projet est optimisé autour d'une expérience UX à faible latence, avec un retour visuel pendant l'écoute ou la réflexion de l'assistant.

### Résumé visuel

| Étape | Intention |
| --- | --- |
| 🎙️ Capture | Capture audio navigateur + états d'interface selon la permission |
| 🧠 Traitement | Transcription Whisper + génération de réponse GPT-4o |
| 🔉 Livraison | Lecture streaming ElevenLabs avec retour d'état |

## Fonctionnalités <a id="features"></a>

| Fonction | Signification |
| --- | --- |
| ✅ Assistant navigateur type Siri | Interaction complète voix vers voix dans une interface web simple |
| ⚡ Parcours à faible latence | Capture, transcription, completion et lecture optimisées |
| 🧠 Stack LLM + TTS | OpenAI Whisper, GPT-4o et synthèse streaming ElevenLabs |
| 🧩 Architecture d'application extensible | Remplacer l'endpoint du modèle ou le fournisseur de voix avec des changements au niveau projet |

Détails d'implémentation supplémentaires :

| Axe | Comportement actuel |
| --- | --- |
| Framework | Next.js 13 App Router avec TypeScript |
| Runtime API | Endpoint de chat en runtime Edge (`/api/chat`) |
| Retour UX | Notifications toast pour les états de permission micro, écoute et traitement |
| Interface d'interaction | Bouton assistant animé avec lecture TTS en streaming |
| Réseau | Remplacement facultatif de l'URL de base OpenAI pour des configurations proxy/self-hosted |

## Démo <a id="demo"></a>

Vous pouvez tester Aura ici : [https://voice.julianschoen.co](https://voice.julianschoen.co)

## Motivation <a id="motivation"></a>

Les assistants vocaux font désormais partie du quotidien : téléphones, voitures, maisons et plus encore. Reproduire cette expérience sur le web avec une bonne réactivité a été historiquement difficile.

Jusqu'à récemment, le principal problème des assistants vocaux sur le web était la latence. Il fallait trop de temps pour envoyer l'audio au serveur, générer une completion LLM et renvoyer la parole. Les progrès récents d'OpenAI, ElevenLabs et Vercel ont permis de construire un assistant vocal suffisamment rapide pour être pratique sur le web.

Ce dépôt vise à être une référence pour les personnes qui souhaitent créer leur propre assistant vocal et comprendre les compromis des implémentations réelles.

## Réflexions sur la latence et l'expérience utilisateur <a id="latence-et-experience-utilisateur"></a>

La latence est le facteur le plus important pour une bonne UX vocale. Actuellement, trois grandes sources contribuent :

- Temps de transcription (reconnaissance vocale Whisper).
- Temps de génération de réponse (GPT-4o Mini dans les notes du projet original).
- Temps de streaming de la synthèse vocale (ElevenLabs TTS).

D'après les notes de tests pratiques, la génération vocale prend généralement le plus de temps et est la moins prévisible, notamment pour les réponses longues.

Une stratégie d'atténuation consiste à découper la réponse en plusieurs parties et à les streamer successivement. Cela permet à l'utilisateur de commencer à écouter plus tôt tandis que le reste est encore en cours de génération. Ce n'est pas encore implémenté, mais c'est une piste prometteuse.

Un autre concept clé est le temps d'attente perçu. Même quand la latence totale reste fixe, les utilisateurs tolèrent mieux les délais lorsqu'ils reçoivent un retour immédiat. Le projet inclut actuellement une notification de "réflexion" pendant le traitement pour améliorer la réactivité perçue.

## Architecture <a id="architecture"></a>

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

Fichiers principaux :

- `src/components/AssistantButton/AssistantButton.tsx`: état d'enregistrement, orchestration des requêtes, lecture.
- `src/app/api/speechToText/route.ts`: audio base64 -> `/tmp/input.webm` -> transcription Whisper.
- `src/app/api/chat/route.ts`: completion de chat via OpenAI.
- `src/app/page.tsx`: interface desktop-first et message de secours mobile.

## Structure du projet <a id="project-structure"></a>

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

## Prérequis <a id="prerequisites"></a>

| Besoin | Détails |
| --- | --- |
| Node.js | 18+ (recommandé : Node.js 18.17+ ou Node.js 20 LTS pour Next.js 13) |
| Gestionnaire de paquets | npm (le projet utilise `package-lock.json`) |
| Accès API | Clé API OpenAI |
| Accès TTS | Clé API ElevenLabs et ID de voix |
| Client | Navigateur desktop avec accès micro (l'UX mobile est actuellement orientée desktop) |

## Installation <a id="installation"></a>

1. Cloner le dépôt :

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. Copier le modèle d'environnement et modifier les valeurs :

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL="" # Optional
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. Installer les dépendances :

```sh
npm install
```

4. Lancer l'application en local :

```sh
npm run dev
```

5. Ouvrir l'application sur `http://localhost:3000`.

Hypothèse : si vous testez l'accès au micro sur des domaines non locaux, le HTTPS est généralement requis.

6. Déployer sur Vercel :

Ce projet suit un flux de déploiement Next.js standard. Utilisez les paramètres d'import par défaut de Vercel et définissez les mêmes variables d'environnement dans votre projet.

## Configuration <a id="configuration"></a>

Variables d'environnement utilisées par ce projet :

| Variable | Obligatoire | Description |
| --- | --- | --- |
| `OPENAI_API_KEY` | Oui | Clé API utilisée pour la transcription Whisper et la completion de chat GPT. |
| `OPENAI_BASE_URL` | Non | Remplacement optionnel de l'URL de base de l'API OpenAI (proxy/gateway). |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Oui | Clé API ElevenLabs utilisée dans la demande TTS côté navigateur. |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Oui | ID de voix ElevenLabs pour la synthèse TTS. |

Notes :

- Les variables `NEXT_PUBLIC_*` sont exposées au client par convention Next.js.
- `speechToText` écrit actuellement un fichier audio temporaire dans `/tmp/input.webm` avant la transcription.

## Utilisation <a id="utilisation"></a>

1. Ouvrir l'application dans un navigateur desktop.
2. Cliquer une fois sur l'orbe d'assistant et accorder la permission microphone.
3. Cliquer à nouveau pour démarrer l'enregistrement, puis à nouveau pour arrêter et envoyer.
4. Aura transcrit votre entrée, génère une réponse, puis lit la voix synthétique.

Scripts locaux :

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## Exemples d'API <a id="api-examples"></a>

Ces exemples sont utiles pour déboguer les routes API locales.

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

Format de réponse attendu :

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

Forme de réponse attendue :

```json
"Assistant response text"
```

## Notes de développement <a id="development-notes"></a>

- La route chat est configurée pour le runtime Edge (`export const runtime = "edge"`).
- La route Whisper s'exécute côté serveur et dépend de l'accès au système de fichiers pour le stockage temporaire.
- L'interface affiche actuellement un message de fallback mobile plutôt qu'une interaction mobile complète.
- Les notifications toast sont utilisées pour afficher les états de permission, d'écoute et de réflexion.
- Le prompt actuel demande des réponses concises (`Your answer has to be as concise as possible.`).
- Les logs runtime, la traçabilité des requêtes et le comportement streaming ne sont pas encore testés en CI (pas de suite de tests automatisée dans le dépôt).

## Dépannage <a id="troubleshooting"></a>

### 🎤 Le pop-up de permission micro n'apparaît pas

- Vérifiez que votre navigateur autorise l'accès au microphone pour `localhost`.
- Utilisez HTTPS lors de tests sur des domaines non localhost.

### 🔈 Aucune lecture audio

- Vérifiez `NEXT_PUBLIC_ELEVENLABS_API_KEY` et `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`.
- Vérifiez les restrictions de lecture automatique/audio-context du navigateur (une interaction utilisateur est requise).

### 📡 Erreur 500 de l'API `/api/speechToText`

- Vérifiez que `OPENAI_API_KEY` est bien défini.
- Confirmez que l'entrée contient un audio `webm` valide encodé en base64.

### 📡 Erreur 500 de l'API `/api/chat`

- Vérifiez que `OPENAI_API_KEY` et éventuellement `OPENAI_BASE_URL` sont corrects.
- Vérifiez la disponibilité du modèle `gpt-4o` dans votre compte OpenAI.

### ⏳ Haute latence

- Le temps de synthèse TTS domine généralement la latence de bout en bout.
- Gardez les prompts concis et envisagez de découper les réponses longues.

## Feuille de route <a id="roadmap"></a>

Améliorations potentielles déduites du code actuel et des notes :

- Prise en charge d'interaction orientée mobile (remplacement du filtrage desktop-only actuel).
- Diffusion partielle des réponses de l'assistant en streaming pour réduire la latence perçue.
- Meilleure UX de retry/erreur autour des échecs de transcription et de TTS.
- Ajout de tests automatisés et de contrôles CI.
- Extension de la documentation multilingue sous [`/i18n`](./i18n/).

## Contribution <a id="contributing"></a>

Les contributions sont les bienvenues et appréciées.

- Consultez [CONTRIBUTING.md](./CONTRIBUTING.md) pour le flux de travail et les attentes.
- Consultez [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) avant de participer.
- Ouvrez un ticket pour les bugs ou idées de fonctionnalités :
- Rapport de bug : [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- Demande de fonctionnalité : [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## Contact <a id="contact"></a>

Bonjour ! Merci d'avoir regardé et utilisé cette bibliothèque. Si vous êtes intéressé par une discussion sur votre projet, que vous cherchez un mentorat, souhaitez m'engager, ou simplement discuter, je suis heureux de vous parler.

Vous pouvez m'envoyer un e-mail : `j.schoen@mail.com` ou me contacter sur Twitter : [@julianschoen](https://twitter.com/julianschoen)

Si vous souhaitez offrir un soutien, j'ai un compte Buy Me A Coffee :

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

Merci et bonne journée 👋

## Disclaimer <a id="disclaimer"></a>

Voice Assistant est une application expérimentale et est fournie « en l'état », sans aucune garantie, explicite ou implicite. En utilisant ce logiciel, vous acceptez d'assumer tous les risques liés à son utilisation, notamment, sans limitation, la perte de données, la défaillance du système ou d'autres problèmes pouvant survenir.

Les développeurs et contributeurs de ce projet n'acceptent aucune responsabilité pour les pertes, dommages ou conséquences pouvant découler de l'utilisation de ce logiciel. Vous êtes seul responsable des décisions et actions prises sur la base des informations fournies par Voice Assistant.

Veuillez noter que l'utilisation du modèle GPT-4 peut être coûteuse en raison de la consommation de tokens. En utilisant ce projet, vous reconnaissez être responsable de surveiller et de gérer votre propre consommation de tokens et vos coûts associés. Il est vivement recommandé de consulter régulièrement votre usage de l'API OpenAI et de mettre en place les limites ou alertes nécessaires pour éviter des frais inattendus.

En utilisant Voice Assistant, vous acceptez d'indemniser, de défendre et d'exonérer les développeurs, contributeurs et toute partie affiliée de toute réclamation, dommage, perte, responsabilité, coût et dépense (y compris les honoraires raisonnables d'avocats) découlant de votre utilisation de ce logiciel ou de la violation de ces conditions.

<!-- LICENSE -->

## License <a id="license"></a>

Distributed under the MIT License. See `LICENSE` for more information.

Repository note: this repository currently stores the license file as [`LICENCE`](./LICENCE).
