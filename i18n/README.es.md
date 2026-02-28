[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


<a name="readme-top"></a>

<br />
<div align="center">

<h3 align="center">Dale la bienvenida a Aura 👋</h3>

<p align="center">
Aura es un asistente de voz inteligente optimizado para respuestas de baja latencia. Usa Vercel Edge Functions, reconocimiento de voz Whisper, GPT-4o y streaming TTS de ElevenLabs.
<br />
<br />
<a href="https://voice.julianschoen.co">Ver demo</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=">Reportar error</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=">Solicitar funcionalidad</a>
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

## Tabla de contenidos

- [Descripción general](#descripción-general)
- [Características](#características)
- [Demo](#demo)
- [Motivación](#motivación)
- [Reflexiones sobre latencia y experiencia de usuario](#reflexiones-sobre-latencia-y-experiencia-de-usuario)
- [Arquitectura](#arquitectura)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Requisitos previos](#requisitos-previos)
- [Instalación](#instalación)
- [Configuración](#configuración)
- [Uso](#uso)
- [Ejemplos de API](#ejemplos-de-api)
- [Notas de desarrollo](#notas-de-desarrollo)
- [Resolución de problemas](#resolución-de-problemas)
- [Hoja de ruta](#hoja-de-ruta)
- [Contribuir](#contribuir)
- [Contacto](#contacto)
- [Descargo de responsabilidad](#descargo-de-responsabilidad)
- [Licencia](#licencia)

## Descripción general

Aura es un asistente de voz en el navegador, similar a Siri, creado con Next.js (App Router) y TypeScript.

### Resumen rápido

| Área | Detalles |
| --- | --- |
| Objetivo principal | Interacción de voz web rápida, práctica y de baja latencia |
| Modelo de ejecución | Captura en navegador + rutas API en servidor + endpoint de chat en Edge |
| Voz a texto | OpenAI Whisper (`whisper-1`) |
| Modelo del asistente | OpenAI GPT-4o |
| Texto a voz | Reproducción en streaming de ElevenLabs en el navegador |

El ciclo de interacción es:

1. Capturar audio del micrófono en el navegador.
2. Transcribir la voz con OpenAI Whisper (`whisper-1`).
3. Generar una respuesta concisa con OpenAI GPT-4o.
4. Transmitir audio sintetizado de vuelta al usuario mediante ElevenLabs.

El proyecto está optimizado para una UX práctica de baja latencia, con retroalimentación visual mientras el asistente está escuchando o pensando.

## Características

✅ Un asistente de voz tipo Siri dentro de tu navegador  
✅ Optimizado para respuestas de baja latencia  
✅ Construido con OpenAI, reconocimiento de voz Whisper y ElevenLabs

Detalles adicionales de implementación:

- Next.js 13 App Router con TypeScript.
- Endpoint de chat en Edge runtime (`/api/chat`).
- Feedback de interacción con toasts (permiso de micrófono, escuchando, pensando).
- Botón animado del asistente con reproducción TTS en streaming.
- Override opcional de la base URL de OpenAI para configuraciones con proxy/gateway autoalojado.

## Demo

Puedes probar Aura aquí: [https://voice.julianschoen.co](https://voice.julianschoen.co)

## Motivación

Los asistentes de voz se han vuelto parte integral de la vida diaria: teléfonos, coches, hogares y más. Llevar esa experiencia a la web con buena capacidad de respuesta históricamente ha sido difícil.

Hasta hace poco, el principal problema de los asistentes de voz en la web era la latencia. Tardaba demasiado enviar audio al servidor, generar una respuesta con un LLM y volver a transmitir voz. Avances recientes de OpenAI, ElevenLabs y Vercel hicieron posible construir un asistente de voz lo bastante rápido como para que sea práctico en la web.

Este repositorio busca ser un lugar de referencia para quienes quieren construir su propio asistente de voz y entender los tradeoffs en implementaciones reales.

## Reflexiones sobre latencia y experiencia de usuario

La latencia es el factor más importante para una buena UX de voz. Actualmente hay tres contribuyentes principales:

- Tiempo de transcripción (reconocimiento de voz Whisper).
- Tiempo de generación de respuesta (GPT-4o Mini en las notas originales del proyecto).
- Tiempo de streaming de síntesis de voz (TTS de ElevenLabs).

Según notas de pruebas prácticas, la generación de voz suele tardar más y es la menos predecible, especialmente para respuestas largas.

Una posible estrategia de mitigación es dividir la respuesta en varias partes y transmitirlas una tras otra. Esto permite que el usuario empiece a escuchar antes, mientras el resto aún se está generando. Todavía no está implementado, pero es una dirección prometedora.

Otro concepto clave es el tiempo de espera percibido. Incluso cuando la latencia total es fija, los usuarios toleran mejor la espera si reciben feedback inmediato. El proyecto actualmente incluye una notificación de "thinking" durante el procesamiento para mejorar la sensación de respuesta.

## Arquitectura

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

Archivos clave:

- `src/components/AssistantButton/AssistantButton.tsx`: estado de grabación, orquestación de solicitudes y reproducción.
- `src/app/api/speechToText/route.ts`: audio base64 -> `/tmp/input.webm` -> transcripción con Whisper.
- `src/app/api/chat/route.ts`: chat completion vía OpenAI.
- `src/app/page.tsx`: interfaz orientada a escritorio y mensaje alternativo para móvil.

## Estructura del proyecto

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

## Requisitos previos

- Node.js 18+ (recomendado: Node.js 18.17+ o 20 LTS para Next.js 13).
- npm (el proyecto usa `package-lock.json`).
- Clave API de OpenAI.
- Clave API y voice ID de ElevenLabs.
- Un navegador de escritorio con acceso a micrófono (la UX móvil actualmente está limitada por diseño).

## Instalación

1. Clona el repositorio:

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. Obtén las API keys en [https://openai.com/](https://openai.com/) y [https://elevenlabs.com/](https://elevenlabs.com/).

Copia el archivo `.env.example` a `.env.local` y agrega tus claves:

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL=(Optional)
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. Instala las dependencias:

```sh
npm install
```

4. Ejecuta la app en local:

```sh
npm run dev
```

5. Despliega en Vercel:

Este proyecto es compatible con el flujo de despliegue estándar de Vercel para Next.js.

## Configuración

Variables de entorno utilizadas por este proyecto:

| Variable | Requerida | Descripción |
| --- | --- | --- |
| `OPENAI_API_KEY` | Sí | API key usada para la transcripción con Whisper y el chat completion con GPT. |
| `OPENAI_BASE_URL` | No | Override opcional de la URL base de la API de OpenAI (proxy/gateway). |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Sí | API key de ElevenLabs usada en la solicitud TTS del lado del navegador. |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Sí | Voice ID de ElevenLabs para la síntesis TTS. |

Notas:

- Las variables `NEXT_PUBLIC_*` se exponen al cliente según las convenciones de Next.js.
- `speechToText` actualmente escribe audio temporal en `/tmp/input.webm` antes de transcribir.

## Uso

1. Abre la app en un navegador de escritorio.
2. Haz clic una vez en el orbe del asistente y concede permisos de micrófono.
3. Haz clic de nuevo para comenzar a grabar y luego otra vez para detener y enviar.
4. Aura transcribe tu entrada, genera una respuesta y luego reproduce voz sintetizada.

Scripts locales:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## Ejemplos de API

Estos ejemplos son útiles para depurar rutas API locales.

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

Forma de respuesta esperada:

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

Forma de respuesta esperada:

```json
"Assistant response text"
```

## Notas de desarrollo

- La ruta de chat está configurada para Edge runtime (`export const runtime = "edge"`).
- La ruta de Whisper se ejecuta en servidor y depende de acceso al sistema de archivos para almacenamiento temporal.
- Actualmente la UI muestra un mensaje alternativo en móvil en lugar de interacción móvil completa.
- Se usan notificaciones tipo toast para exponer estados de permiso/escucha/procesamiento.
- El shaping actual del prompt pide respuestas concisas (`Your answer has to be as consise as possible.`).

## Resolución de problemas

### No aparece la solicitud de permiso del micrófono

- Asegúrate de que tu navegador permita acceso al micrófono para `localhost`.
- Usa HTTPS al probar en dominios que no sean localhost.

### No hay reproducción de audio

- Verifica `NEXT_PUBLIC_ELEVENLABS_API_KEY` y `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`.
- Comprueba restricciones de autoplay/audio-context del navegador (se requiere interacción del usuario).

### API 500 desde `/api/speechToText`

- Confirma que `OPENAI_API_KEY` esté configurada.
- Valida que la entrada contenga audio `webm` en base64 válido.

### API 500 desde `/api/chat`

- Confirma que `OPENAI_API_KEY` y el opcional `OPENAI_BASE_URL` sean correctos.
- Revisa la disponibilidad del modelo `gpt-4o` en tu cuenta de OpenAI.

### Latencia alta

- El tiempo de síntesis TTS suele dominar la latencia end-to-end.
- Mantén prompts concisos y considera dividir respuestas largas.

## Hoja de ruta

Posibles próximas mejoras inferidas del código y las notas actuales:

- Soporte de interacción mobile-first (reemplazar la limitación actual solo-escritorio).
- Streaming de respuestas parciales del asistente para reducir latencia percibida.
- Mejor UX de reintentos/errores en fallos de transcripción y TTS.
- Añadir pruebas automatizadas y checks de CI.
- Ampliar la documentación multilingüe en [`/i18n`](./i18n/).

## Contribuir

Las contribuciones son bienvenidas y se agradecen.

- Lee [CONTRIBUTING.md](./CONTRIBUTING.md) para conocer el flujo y las expectativas.
- Lee [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) antes de participar.
- Abre issues para bugs o ideas de funcionalidades:
- Reporte de bug: [plantilla](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- Solicitud de funcionalidad: [plantilla](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## Contacto

¡Hola! Gracias por revisar y usar esta librería. Si te interesa hablar sobre tu proyecto, necesitas mentoría, estás pensando en contratarme o simplemente quieres conversar, encantado de hablar.

Puedes enviarme un email: `j.schoen@mail.com` o escribirme en Twitter: [@julianschoen](https://twitter.com/julianschoen)

Si quieres devolver algo, tengo una cuenta de Buy Me A Coffee:

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

Gracias y que tengas un día increíble 👋

## Descargo de responsabilidad

Voice Assistant es una aplicación experimental y se proporciona "tal cual", sin ninguna garantía, expresa o implícita. Al usar este software, aceptas asumir todos los riesgos asociados con su uso, incluidos, entre otros, pérdida de datos, fallos del sistema o cualquier otro problema que pueda surgir.

Los desarrolladores y contribuidores de este proyecto no aceptan ninguna responsabilidad por pérdidas, daños u otras consecuencias que puedan ocurrir como resultado del uso de este software. Eres el único responsable de cualquier decisión y acción tomada en base a la información proporcionada por Voice Assistant.

Ten en cuenta que el uso del modelo de lenguaje GPT-4 puede ser costoso debido al consumo de tokens. Al utilizar este proyecto, reconoces que eres responsable de supervisar y gestionar tu propio uso de tokens y los costos asociados. Se recomienda encarecidamente revisar tu uso de la API de OpenAI con regularidad y configurar límites o alertas necesarios para evitar cargos inesperados.

Al usar Voice Assistant, aceptas indemnizar, defender y eximir de responsabilidad a los desarrolladores, contribuidores y cualquier parte afiliada frente a todas y cada una de las reclamaciones, daños, pérdidas, responsabilidades, costos y gastos (incluidos honorarios razonables de abogados) que surjan de tu uso de este software o del incumplimiento de estos términos.

<!-- LICENSE -->

## Licencia

Distribuido bajo la licencia MIT. Consulta `LICENSE` para más información.

Nota del repositorio: actualmente este repositorio almacena el archivo de licencia como [`LICENCE`](./LICENCE).
