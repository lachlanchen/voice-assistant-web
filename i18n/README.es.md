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

<h3 align="center">Conoce a Aura 👋</h3>

<p align="center">
Aura es un asistente de voz basado en navegador, parecido a Siri, optimizado para respuestas de baja latencia. Utiliza Vercel Edge Functions, reconocimiento de voz Whisper, GPT-4o y streaming de TTS de ElevenLabs.
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

## Índice

- [📌 Visión general](#visión-general)
- [✨ Características](#características)
- [🎥 Demo](#demo)
- [🧠 Motivación](#motivación)
- [⏱️ Ideas sobre latencia y experiencia de usuario](#ideas-sobre-latencia-y-experiencia-de-usuario)
- [🏗️ Arquitectura](#arquitectura)
- [📁 Estructura del proyecto](#estructura-del-proyecto)
- [✅ Requisitos previos](#requisitos-previos)
- [🧰 Instalación](#instalación)
- [⚙️ Configuración](#configuración)
- [🧪 Uso](#uso)
- [📦 Ejemplos de API](#ejemplos-de-api)
- [🛠️ Notas de desarrollo](#notas-de-desarrollo)
- [🧯 Solución de problemas](#solución-de-problemas)
- [🗺️ Hoja de ruta](#hoja-de-ruta)
- [❤️ Support](#%e2%9d%a4%ef%b8%8f-support)
- [📬 Contacto](#contacto)
- [⚠️ Descargo de responsabilidad](#descargo-de-responsabilidad)
- [📄 Licencia](#licencia)

## Visión general

Aura es un asistente de voz basado en el navegador, similar a Siri, construido con Next.js (App Router) y TypeScript.

### En un vistazo

| Área | Detalles |
| --- | --- |
| Objetivo principal | Interacción de voz rápida, práctica y de baja latencia en la web |
| Modelo de ejecución | Captura en el navegador + rutas API del servidor + endpoint de chat en Edge |
| Voz a texto | OpenAI Whisper (`whisper-1`) |
| Modelo del asistente | OpenAI GPT-4o |
| Texto a voz | Reproducción con streaming de ElevenLabs en el navegador |

El ciclo de interacción es:

1. Capturar el audio del micrófono en el navegador.
2. Transcribir el habla con OpenAI Whisper (`whisper-1`).
3. Generar una respuesta concisa con OpenAI GPT-4o.
4. Enviar audio sintetizado al usuario mediante ElevenLabs.

El proyecto está optimizado para una experiencia de usuario de baja latencia centrada en el uso real, con retroalimentación visual mientras el asistente escucha o está procesando.

### Resumen visual

| Etapa | Intención |
| --- | --- |
| 🎙️ Captura | Captura de audio en el navegador + estados de interfaz conscientes de permisos |
| 🧠 Procesamiento | Transcripción con Whisper + generación de respuesta de GPT-4o |
| 🔉 Entrega | Reproducción de ElevenLabs con streaming y estado de progreso |

## Características

| Capacidad | Qué significa |
| --- | --- |
| ✅ Asistente de voz tipo Siri | Interacción completa de voz de entrada y salida en una interfaz web simple |
| ⚡ Flujo de trabajo de baja latencia | Bucle de captura, transcripción, completado y reproducción optimizado |
| 🧠 Stack LLM + TTS | OpenAI Whisper, GPT-4o y síntesis en streaming de ElevenLabs |
| 🧩 Arquitectura extensible | Cambia el endpoint del modelo o proveedor de voz con ajustes a nivel de proyecto |

Detalles adicionales de implementación:

| Área de enfoque | Comportamiento actual |
| --- | --- |
| Framework | Next.js 13 App Router con TypeScript |
| Tiempo de ejecución de API | Endpoint de chat con runtime Edge (`/api/chat`) |
| Retroalimentación UX | Notificaciones toast para permisos de micrófono, escucha y estado de procesamiento |
| Interfaz de interacción | Botón animado del asistente con reproducción TTS en streaming |
| Red | Sobrescritura opcional de la URL base de OpenAI para setups de proxy/self-hosted gateway |

## Demo

Puedes probar Aura aquí: [https://voice.julianschoen.co](https://voice.julianschoen.co)

## Motivación

Los asistentes de voz se han vuelto parte integral de la vida diaria: teléfonos, autos, hogares y más. Llevar esa experiencia a la web con buena capacidad de respuesta históricamente fue difícil.

Hasta hace poco, el principal problema con los asistentes de voz en la web era la latencia. Tardaba demasiado enviar el audio al servidor, generar una completion de LLM y devolver el habla. Los avances recientes de OpenAI, ElevenLabs y Vercel han hecho posible construir un asistente de voz suficientemente rápido como para ser práctico en la web.

Este repositorio busca ser un punto de referencia para quienes desean construir su propio asistente de voz y entender los compromisos en implementaciones reales.

## Ideas sobre latencia y experiencia de usuario

La latencia es el factor más importante para una buena experiencia de voz. Actualmente hay tres contribuyentes principales:

- Tiempo de transcripción (reconocimiento de voz Whisper).
- Tiempo de generación de respuesta (GPT-4o Mini en las notas originales del proyecto).
- Tiempo de streaming de síntesis de voz (ElevenLabs TTS).

Por experiencia práctica, la generación de voz suele llevar más tiempo y ser lo menos predecible, especialmente en respuestas más largas.

Una posible estrategia de mitigación es dividir la respuesta en varias partes y transmitirlas una detrás de otra. Esto permite que el usuario empiece a escuchar antes, mientras el resto aún se está generando. Aún no está implementado, pero es una dirección prometedora.

Otro concepto clave es el tiempo de espera percibido. Incluso con una latencia total fija, los usuarios toleran mejor los retrasos cuando reciben retroalimentación inmediata. El proyecto incluye actualmente un aviso de "pensando" durante el procesamiento para mejorar la sensación de respuesta.

## Arquitectura

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

Archivos clave:

- `src/components/AssistantButton/AssistantButton.tsx`: estado de grabación, orquestación de solicitudes y reproducción.
- `src/app/api/speechToText/route.ts`: audio base64 -> `/tmp/input.webm` -> transcripción Whisper.
- `src/app/api/chat/route.ts`: generación de completion de chat a través de OpenAI.
- `src/app/page.tsx`: interfaz orientada a escritorio y mensaje de fallback para móviles.

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

| Requisito | Detalles |
| --- | --- |
| Node.js | 18+ (recomendado: Node.js 18.17+ o 20 LTS para Next.js 13) |
| Gestor de paquetes | npm (el proyecto usa `package-lock.json`) |
| Acceso a API | Clave API de OpenAI |
| Acceso a TTS | Clave API de ElevenLabs e ID de voz |
| Cliente | Navegador de escritorio con acceso al micrófono (la experiencia móvil hoy prioriza escritorio) |

## Instalación

1. Clona el repositorio:

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. Copia la plantilla de entorno y edita los valores:

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL="" # Optional
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. Instala dependencias:

```sh
npm install
```

4. Ejecuta la app en local:

```sh
npm run dev
```

5. Abre la app en `http://localhost:3000`.

Suponemos que si pruebas acceso al micrófono en dominios no locales, normalmente se requiere HTTPS.

6. Despliega en Vercel:

Este proyecto sigue un flujo de despliegue estándar de Next.js. Usa la configuración de importación por defecto de Vercel y define las mismas variables de entorno en tu proyecto.

## Configuración

Variables de entorno usadas por este proyecto:

| Variable | Requerida | Descripción |
| --- | --- | --- |
| `OPENAI_API_KEY` | Sí | Clave API para transcripción Whisper y completion de chat de GPT. |
| `OPENAI_BASE_URL` | No | Sobrescritura opcional de la URL base de la API de OpenAI (proxy/gateway). |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Sí | Clave API de ElevenLabs usada en la solicitud TTS del lado del cliente. |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Sí | ID de voz de ElevenLabs para la síntesis TTS. |

Notas:

- Las variables `NEXT_PUBLIC_*` se exponen al cliente conforme a las convenciones de Next.js.
- `speechToText` actualmente guarda el audio temporal en `/tmp/input.webm` antes de la transcripción.

## Uso

1. Abre la app en un navegador de escritorio.
2. Haz clic una vez en el botón del asistente y concede permisos de micrófono.
3. Haz clic de nuevo para iniciar la grabación, y de nuevo para detenerla y enviarla.
4. Aura transcribe tu entrada, genera una respuesta y luego reproduce el audio sintetizado.

Scripts locales:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## Ejemplos de API

Estos ejemplos son útiles para depurar las rutas API locales.

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

Forma esperada de respuesta:

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

Forma esperada de respuesta:

```json
"Assistant response text"
```

## Notas de desarrollo

- La ruta de chat está configurada para Edge runtime (`export const runtime = "edge"`).
- La ruta de Whisper se ejecuta del lado del servidor y depende del acceso al sistema de archivos para almacenamiento temporal.
- La UI actualmente muestra un mensaje de fallback para móvil en lugar de una interacción móvil completa.
- Se usan notificaciones toast para mostrar estados de permiso, escucha y procesamiento.
- El prompt actual pide respuestas concisas (`Your answer has to be as concise as possible.`).
- Los logs de runtime, la trazabilidad de solicitudes y el comportamiento de streaming no están probados actualmente en CI (no hay suite de pruebas automatizada en este repositorio).

## Solución de problemas

### 🎤 La solicitud de permiso del micrófono no aparece

- Asegúrate de que tu navegador permita acceso al micrófono para `localhost`.
- Usa HTTPS al probar en dominios que no sean localhost.

### 🔈 No se reproduce audio

- Verifica `NEXT_PUBLIC_ELEVENLABS_API_KEY` y `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`.
- Comprueba las restricciones de autoplay/audio-context del navegador (se requiere interacción del usuario).

### 📡 Error 500 de la API en `/api/speechToText`

- Confirma que `OPENAI_API_KEY` esté configurada.
- Comprueba que la entrada incluya audio `webm` válido codificado en base64.

### 📡 Error 500 de la API en `/api/chat`

- Confirma que `OPENAI_API_KEY` y `OPENAI_BASE_URL` (opcional) sean correctas.
- Verifica la disponibilidad del modelo `gpt-4o` en tu cuenta de OpenAI.

### ⏳ Alta latencia

- El tiempo de síntesis de voz suele dominar la latencia de extremo a extremo.
- Mantén prompts concisos y considera dividir respuestas largas.

## Hoja de ruta

Mejoras potenciales inferidas del código actual y las notas:

- Soporte de interacción con enfoque móvil (sustituir la restricción actual orientada a escritorio).
- Streaming de respuestas parciales del asistente para reducir la latencia percibida.
- Mejorar la UX de reintentos y errores alrededor de fallos de transcripción y TTS.
- Añadir pruebas automatizadas y comprobaciones de CI.
- Expandir la documentación multilingüe en [`/i18n`](./i18n/).

## Contribuir

Las contribuciones son bienvenidas y apreciadas.

- Lee [CONTRIBUTING.md](./CONTRIBUTING.md) para conocer el flujo de trabajo y las expectativas.
- Lee [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) antes de participar.
- Abre issues para reportar errores o proponer mejoras:
  - Informe de error: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
  - Solicitud de función: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |

## Contacto

¡Hola! Gracias por mirar y usar esta librería. Si te interesa hablar de tu proyecto, necesitas mentoría, quieres contratarme o simplemente charlar, estaré encantado de hablar.

Puedes enviarme un correo a `j.schoen@mail.com` o escribirme en Twitter: [@julianschoen](https://twitter.com/julianschoen)

Si quieres agradecer, tengo una cuenta de Buy Me A Coffee:

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

¡Gracias y que tengas un gran día 👋

## Descargo de responsabilidad

Voice Assistant es una aplicación experimental y se ofrece "tal cual" sin ninguna garantía, expresa o implícita. Al usar este software, aceptas asumir todos los riesgos asociados con su uso, incluyendo, entre otros, pérdida de datos, fallos del sistema o cualquier otro problema que pueda surgir.

Los desarrolladores y colaboradores de este proyecto no aceptan ninguna responsabilidad o obligación por pérdidas, daños u otras consecuencias que puedan derivarse del uso de este software. Tú eres el único responsable de cualquier decisión o acción basada en la información proporcionada por Voice Assistant.

Ten en cuenta que usar el modelo GPT-4 puede ser costoso por el consumo de tokens. Al utilizar este proyecto, reconoces que eres responsable de controlar y gestionar tu propio uso de tokens y costos asociados. Se recomienda encarecidamente revisar regularmente tu uso de la API de OpenAI y configurar límites o alertas para evitar cargos inesperados.

Al usar Voice Assistant, aceptas indemnizar, defender y eximir de responsabilidad a los desarrolladores, colaboradores y cualquier parte asociada por cualquier reclamación, daño, pérdida, responsabilidad, costo y gasto (incluidos honorarios razonables de abogados) que surjan del uso de este software o de la violación de estos términos.

<!-- LICENSE -->

## Licencia

Distribuido bajo la Licencia MIT. Consulta `LICENSE` para más información.

Nota del repositorio: este repositorio actualmente guarda el archivo de licencia como [`LICENCE`](./LICENCE).
