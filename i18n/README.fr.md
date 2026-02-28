[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


<a name="readme-top"></a>

<br />
<div align="center">

<h3 align="center">Dites bonjour à Aura 👋</h3>

<p align="center">
Aura est un assistant vocal intelligent optimisé pour des réponses à faible latence. Il utilise les Edge Functions de Vercel, la reconnaissance vocale Whisper, GPT-4o et le streaming TTS d'ElevenLabs.
<br />
<br />
<a href="https://voice.julianschoen.co">Voir la démo</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=">Signaler un bug</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=">Demander une fonctionnalité</a>
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

- [Vue d'ensemble](#vue-densemble)
- [Fonctionnalités](#fonctionnalités)
- [Démo](#démo)
- [Motivation](#motivation)
- [Réflexions sur la latence et l'expérience utilisateur](#réflexions-sur-la-latence-et-lexpérience-utilisateur)
- [Architecture](#architecture)
- [Structure du projet](#structure-du-projet)
- [Prérequis](#prérequis)
- [Installation](#installation)
- [Configuration](#configuration)
- [Utilisation](#utilisation)
- [Exemples d'API](#exemples-dapi)
- [Notes de développement](#notes-de-développement)
- [Dépannage](#dépannage)
- [Feuille de route](#feuille-de-route)
- [Contribution](#contribution)
- [Contact](#contact)
- [Avertissement](#avertissement)
- [Licence](#licence)

## Vue d'ensemble

Aura est un assistant vocal de type Siri, basé navigateur, construit avec Next.js (App Router) et TypeScript.

### En un coup d'œil

| Domaine | Détails |
| --- | --- |
| Objectif principal | Interaction vocale web rapide, pratique et à faible latence |
| Modèle d'exécution | Capture navigateur + routes API serveur + endpoint chat Edge |
| Speech-to-text | OpenAI Whisper (`whisper-1`) |
| Modèle assistant | OpenAI GPT-4o |
| Text-to-speech | Lecture en streaming ElevenLabs dans le navigateur |

La boucle d'interaction est la suivante:

1. Capturer l'audio du microphone dans le navigateur.
2. Transcrire la voix avec OpenAI Whisper (`whisper-1`).
3. Générer une réponse concise avec OpenAI GPT-4o.
4. Diffuser l'audio synthétisé vers l'utilisateur avec ElevenLabs.

Le projet est optimisé pour une UX pratique à faible latence, avec un retour visuel pendant que l'assistant écoute ou réfléchit.

## Fonctionnalités

✅ Un assistant vocal de type Siri directement dans votre navigateur  
✅ Optimisé pour des réponses à faible latence  
✅ Construit avec OpenAI, la reconnaissance vocale Whisper et ElevenLabs

Détails d'implémentation supplémentaires:

- Next.js 13 App Router avec TypeScript.
- Endpoint de chat Edge runtime (`/api/chat`).
- Retour d'interaction via notifications toast (permission micro, écoute, réflexion).
- Bouton assistant animé avec lecture TTS en streaming.
- Remplacement optionnel de l'URL de base OpenAI pour les configurations proxy/passerelle auto-hébergée.

## Démo

Vous pouvez tester Aura ici: [https://voice.julianschoen.co](https://voice.julianschoen.co)

## Motivation

Les assistants vocaux sont devenus une partie intégrante du quotidien: téléphones, voitures, maisons, et plus encore. Reproduire cette expérience sur le web avec une bonne réactivité a longtemps été difficile.

Jusqu'à récemment, le principal problème des assistants vocaux sur le web était la latence. Il fallait trop de temps pour envoyer l'audio au serveur, générer une complétion LLM et renvoyer l'audio en streaming. Les avancées récentes d'OpenAI, ElevenLabs et Vercel ont rendu possible la création d'un assistant vocal suffisamment rapide pour un usage pratique sur le web.

Ce dépôt vise à devenir une référence pour celles et ceux qui veulent créer leur propre assistant vocal et comprendre les compromis des implémentations réelles.

## Réflexions sur la latence et l'expérience utilisateur

La latence est le facteur le plus important pour une bonne UX vocale. Actuellement, il y a trois contributeurs majeurs:

- Temps de transcription (reconnaissance vocale Whisper).
- Temps de génération de réponse (GPT-4o Mini dans les notes du projet d'origine).
- Temps de streaming de synthèse vocale (ElevenLabs TTS).

D'après les notes de tests pratiques, la génération vocale est généralement l'étape la plus longue et la moins prévisible, en particulier pour les réponses longues.

Une stratégie d'atténuation possible consiste à découper la réponse en plusieurs parties et à les diffuser l'une après l'autre. Cela permet à l'utilisateur de commencer à écouter plus tôt pendant que le reste est encore en cours de génération. Ce n'est pas encore implémenté, mais c'est une direction prometteuse.

Un autre concept clé est le temps d'attente perçu. Même lorsque la latence totale est fixe, les utilisateurs tolèrent mieux les délais lorsqu'ils reçoivent un retour immédiat. Le projet inclut actuellement une notification « réflexion » pendant le traitement afin d'améliorer la réactivité perçue.

## Architecture

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

Fichiers clés:

- `src/components/AssistantButton/AssistantButton.tsx`: état d'enregistrement, orchestration des requêtes, lecture audio.
- `src/app/api/speechToText/route.ts`: audio base64 -> `/tmp/input.webm` -> transcription Whisper.
- `src/app/api/chat/route.ts`: complétion de chat via OpenAI.
- `src/app/page.tsx`: interface orientée desktop et message de repli pour mobile.

## Structure du projet

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

## Prérequis

- Node.js 18+ (recommandé: Node.js 18.17+ ou 20 LTS pour Next.js 13).
- npm (le projet utilise `package-lock.json`).
- Clé API OpenAI.
- Clé API ElevenLabs et ID de voix.
- Un navigateur desktop avec accès au microphone (l'UX mobile est actuellement limitée par conception).

## Installation

1. Cloner le dépôt:

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. Récupérer les clés API depuis [https://openai.com/](https://openai.com/) et [https://elevenlabs.com/](https://elevenlabs.com/).

Copiez le fichier `.env.example` vers `.env.local` et ajoutez vos clés:

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL=(Optional)
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. Installer les dépendances:

```sh
npm install
```

4. Lancer l'application en local:

```sh
npm run dev
```

5. Déployer sur Vercel:

Ce projet est compatible avec le flux de déploiement standard de Vercel pour Next.js.

## Configuration

Variables d'environnement utilisées par ce projet:

| Variable | Obligatoire | Description |
| --- | --- | --- |
| `OPENAI_API_KEY` | Oui | Clé API utilisée pour la transcription Whisper et la complétion de chat GPT. |
| `OPENAI_BASE_URL` | Non | Remplacement optionnel de l'URL de base de l'API OpenAI (proxy/passerelle). |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Oui | Clé API ElevenLabs utilisée dans la requête TTS côté navigateur. |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Oui | ID de voix ElevenLabs pour la synthèse TTS. |

Notes:

- Les variables `NEXT_PUBLIC_*` sont exposées au client selon les conventions Next.js.
- `speechToText` écrit actuellement l'audio temporaire dans `/tmp/input.webm` avant transcription.

## Utilisation

1. Ouvrez l'application dans un navigateur desktop.
2. Cliquez une fois sur l'orbe de l'assistant et accordez les permissions micro.
3. Cliquez à nouveau pour démarrer l'enregistrement, puis cliquez encore pour arrêter et envoyer.
4. Aura transcrit votre entrée, génère une réponse, puis lit la voix synthétisée.

Scripts locaux:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## Exemples d'API

Ces exemples sont utiles pour déboguer les routes API locales.

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

Format de réponse attendu:

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

Format de réponse attendu:

```json
"Assistant response text"
```

## Notes de développement

- La route de chat est configurée pour l'Edge runtime (`export const runtime = "edge"`).
- La route Whisper s'exécute côté serveur et dépend de l'accès au système de fichiers pour le stockage temporaire.
- L'UI fournit actuellement un message de repli mobile au lieu d'une interaction mobile complète.
- Les notifications toast sont utilisées pour afficher les états permission/écoute/réflexion.
- La formulation actuelle du prompt demande des réponses concises (`Your answer has to be as consise as possible.`).

## Dépannage

### La demande de permission micro n'apparaît pas

- Assurez-vous que votre navigateur autorise l'accès au microphone pour `localhost`.
- Utilisez HTTPS lors des tests sur des domaines non-localhost.

### Aucun son en lecture

- Vérifiez `NEXT_PUBLIC_ELEVENLABS_API_KEY` et `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`.
- Vérifiez les restrictions de lecture automatique/audio-context du navigateur (une interaction utilisateur est nécessaire).

### API 500 depuis `/api/speechToText`

- Confirmez que `OPENAI_API_KEY` est défini.
- Validez que l'entrée contient un audio `webm` encodé en base64 valide.

### API 500 depuis `/api/chat`

- Confirmez que `OPENAI_API_KEY` et `OPENAI_BASE_URL` (optionnel) sont corrects.
- Vérifiez la disponibilité du modèle `gpt-4o` dans votre compte OpenAI.

### Latence élevée

- Le temps de synthèse TTS domine généralement la latence de bout en bout.
- Gardez les prompts concis et envisagez de découper les réponses longues.

## Feuille de route

Améliorations potentielles déduites du code actuel et des notes:

- Support d'interaction mobile-first (remplacer le blocage actuel orienté desktop).
- Streaming de réponses partielles de l'assistant pour réduire la latence perçue.
- Meilleure UX de reprise/erreur autour des échecs de transcription et TTS.
- Ajouter des tests automatisés et des vérifications CI.
- Étendre la documentation multilingue sous [`/i18n`](./i18n/).

## Contribution

Les contributions sont les bienvenues et appréciées.

- Lisez [CONTRIBUTING.md](./CONTRIBUTING.md) pour le workflow et les attentes.
- Lisez [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) avant de participer.
- Ouvrez des issues pour les bugs ou idées de fonctionnalités:
- Rapport de bug: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- Demande de fonctionnalité: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## Contact

Bonjour! Merci d'avoir consulté et utilisé cette bibliothèque. Si vous souhaitez discuter de votre projet, avez besoin de mentorat, envisagez de m'embaucher, ou voulez simplement échanger, je serai ravi de parler avec vous.

Vous pouvez m'envoyer un e-mail: `j.schoen@mail.com` ou m'écrire sur Twitter: [@julianschoen](https://twitter.com/julianschoen)

Si vous souhaitez offrir un petit soutien, j'ai un compte Buy Me A Coffee:

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

Merci et excellente journée 👋

## Avertissement

Voice Assistant est une application expérimentale et est fournie « telle quelle » sans aucune garantie, expresse ou implicite. En utilisant ce logiciel, vous acceptez d'assumer tous les risques associés à son utilisation, y compris, sans s'y limiter, la perte de données, les pannes système, ou tout autre problème pouvant survenir.

Les développeurs et contributeurs de ce projet n'acceptent aucune responsabilité ni obligation pour toute perte, tout dommage, ou toute autre conséquence pouvant résulter de l'utilisation de ce logiciel. Vous êtes seul responsable de toute décision et action prise sur la base des informations fournies par Voice Assistant.

Veuillez noter que l'utilisation du modèle de langage GPT-4 peut être coûteuse en raison de l'usage de tokens. En utilisant ce projet, vous reconnaissez qu'il vous incombe de surveiller et de gérer votre propre consommation de tokens ainsi que les coûts associés. Il est fortement recommandé de vérifier régulièrement votre consommation API OpenAI et de configurer les limites ou alertes nécessaires pour éviter des frais inattendus.

En utilisant Voice Assistant, vous acceptez d'indemniser, de défendre et de dégager de toute responsabilité les développeurs, contributeurs et toutes les parties affiliées contre toute réclamation, tout dommage, toute perte, toute responsabilité, tout coût et toute dépense (y compris les honoraires raisonnables d'avocats) découlant de votre utilisation de ce logiciel ou de votre violation des présentes conditions.

<!-- LICENSE -->

## Licence

Distribué sous licence MIT. Voir `LICENSE` pour plus d'informations.

Note du dépôt: ce dépôt stocke actuellement le fichier de licence sous [`LICENCE`](./LICENCE).
