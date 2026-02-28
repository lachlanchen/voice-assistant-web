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

<h3 align="center">Xin chào Aura 👋</h3>

<p align="center">
Aura là trợ lý giọng nói kiểu Siri chạy trong trình duyệt, được tối ưu cho phản hồi độ trễ thấp. Nó sử dụng Vercel Edge Functions, nhận diện giọng nói Whisper, GPT-4o và phát sóng trực tiếp TTS của ElevenLabs.
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

## Mục lục

- [📌 Tổng quan](#overview)
- [✨ Tính năng](#features)
- [🎥 Demo](#demo)
- [🧠 Động lực tạo ra sản phẩm](#motivation)
- [⏱️ Suy nghĩ về độ trễ và trải nghiệm người dùng](#thoughts-on-latency-and-user-experience)
- [🏗️ Kiến trúc](#architecture)
- [📁 Cấu trúc dự án](#project-structure)
- [✅ Yêu cầu](#prerequisites)
- [🧰 Cài đặt](#installation)
- [⚙️ Cấu hình](#configuration)
- [🧪 Sử dụng](#usage)
- [📦 Ví dụ API](#api-examples)
- [🛠️ Ghi chú phát triển](#development-notes)
- [🧯 Khắc phục sự cố](#troubleshooting)
- [🗺️ Lộ trình](#roadmap)
- [🤝 Đóng góp](#contributing)
- [❤️ Support](#support)
- [📬 Liên hệ](#contact)
- [⚠️ Tuyên bố từ chối](#disclaimer)
- [📄 Giấy phép](#license)

## Tổng quan <a id="overview"></a>

Aura là trợ lý giọng nói kiểu Siri chạy trên trình duyệt, được xây dựng bằng Next.js (App Router) và TypeScript.

### Tóm tắt

| Khu vực | Chi tiết |
| --- | --- |
| Mục tiêu chính | Tương tác giọng nói nhanh, thực tế, độ trễ thấp trên web |
| Mô hình chạy | Ghi âm phía trình duyệt + API routes máy chủ + endpoint chat Edge |
| Chuyển giọng nói thành văn bản | OpenAI Whisper (`whisper-1`) |
| Mô hình trợ lý | OpenAI GPT-4o |
| Chuyển văn bản thành giọng nói | Phát phát trực tiếp ElevenLabs trong trình duyệt |

Chu trình tương tác là:

1. Ghi âm từ micro trong trình duyệt.
2. Chuyển giọng nói thành văn bản bằng OpenAI Whisper (`whisper-1`).
3. Tạo câu trả lời ngắn gọn bằng OpenAI GPT-4o.
4. Phát lại âm thanh đã tổng hợp cho người dùng qua ElevenLabs.

Dự án được tối ưu cho trải nghiệm người dùng thấp độ trễ, với phản hồi trực quan khi trợ lý đang lắng nghe hoặc đang suy nghĩ.

### Tóm tắt trực quan

| Giai đoạn | Ý định |
| --- | --- |
| 🎙️ Ghi âm | Ghi âm trên trình duyệt + trạng thái giao diện nhận biết quyền |
| 🧠 Xử lý | Chuyển giọng nói bằng Whisper + tạo phản hồi GPT-4o |
| 🔉 Giao | Phát phát trực tiếp ElevenLabs cùng phản hồi trạng thái |

## Tính năng <a id="features"></a>

| Năng lực | Ý nghĩa |
| --- | --- |
| ✅ Trợ lý kiểu Siri trên trình duyệt | Tương tác đầy đủ đầu vào và đầu ra bằng giọng nói trong giao diện web đơn giản |
| ⚡ Luồng làm việc độ trễ thấp | Đã tối ưu chu trình ghi âm, chuyển văn bản, sinh kết quả và phát lại |
| 🧠 Ngăn xếp LLM + TTS | OpenAI Whisper, GPT-4o và tổng hợp stream của ElevenLabs |
| 🧩 Kiến trúc ứng dụng có thể mở rộng | Có thể thay thế endpoint mô hình hoặc nhà cung cấp giọng nói bằng thay đổi cấp dự án |

Thông tin triển khai bổ sung:

| Khu vực tập trung | Hành vi hiện tại |
| --- | --- |
| Framework | Next.js 13 App Router với TypeScript |
| Runtime API | Endpoint chat của môi trường Edge (`/api/chat`) |
| Phản hồi UX | Thông báo toast cho các trạng thái quyền micro, lắng nghe và suy nghĩ |
| Giao diện tương tác | Nút trợ lý hoạt hình với phát lại TTS streaming |
| Mạng lưới | Tuỳ chọn ghi đè URL cơ sở của OpenAI cho kiến trúc gateway/proxy tự host |

## Demo <a id="demo"></a>

Bạn có thể dùng thử Aura tại: [https://voice.julianschoen.co](https://voice.julianschoen.co)

## Động lực tạo ra sản phẩm <a id="motivation"></a>

Trợ lý giọng nói đã trở thành một phần trong cuộc sống hằng ngày: điện thoại, ô tô, nhà thông minh và nhiều hơn nữa. Đưa trải nghiệm đó lên web với độ phản hồi tốt lâu nay đã rất khó.

Cho đến gần đây, vấn đề lớn nhất của trợ lý giọng nói trên web là độ trễ. Quá trình gửi âm thanh lên máy chủ, sinh phản hồi LLM và phát giọng nói lại mất quá lâu. Những tiến bộ gần đây từ OpenAI, ElevenLabs và Vercel đã khiến việc xây dựng một trợ lý giọng nói đủ nhanh để dùng thực tế trên web trở nên khả thi.

Kho lưu trữ này nhằm trở thành điểm tham chiếu cho những người muốn tự xây trợ lý giọng nói và hiểu các đánh đổi trong triển khai thực tế.

## Suy nghĩ về độ trễ và trải nghiệm người dùng <a id="thoughts-on-latency-and-user-experience"></a>

Độ trễ là yếu tố quan trọng nhất của một trải nghiệm giọng nói tốt. Hiện có ba nguyên nhân chính:

- Thời gian phiên âm (nhận diện giọng nói Whisper).
- Thời gian tạo phản hồi (GPT-4o Mini trong ghi chú dự án gốc).
- Thời gian phát trực tiếp phần tổng hợp giọng nói (ElevenLabs TTS).

Theo ghi chú thử nghiệm thực tế, việc tạo âm thanh thường mất nhiều thời gian nhất và khó dự đoán nhất, đặc biệt với các câu trả lời dài.

Một hướng giảm thiểu là chia phản hồi thành nhiều phần rồi phát trực tiếp lần lượt. Cách này giúp người dùng bắt đầu nghe sớm hơn trong khi phần còn lại vẫn đang được tạo. Hiện chưa được triển khai, nhưng là hướng triển khai hứa hẹn.

Một khái niệm quan trọng khác là thời gian chờ cảm nhận được. Ngay cả khi tổng độ trễ không đổi, người dùng vẫn chịu được độ chậm tốt hơn khi họ nhận được phản hồi ngay lập tức. Dự án hiện đã có thông báo “đang suy nghĩ” trong khi xử lý để cải thiện cảm giác phản hồi.

## Kiến trúc <a id="architecture"></a>

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

Các tệp chính:

- `src/components/AssistantButton/AssistantButton.tsx`: trạng thái ghi âm, phối hợp request, phát lại.
- `src/app/api/speechToText/route.ts`: audio base64 -> `/tmp/input.webm` -> phiên âm Whisper.
- `src/app/api/chat/route.ts`: hoàn tất cuộc trò chuyện qua OpenAI.
- `src/app/page.tsx`: giao diện ưu tiên desktop và thông báo dự phòng cho mobile.

## Cấu trúc dự án <a id="project-structure"></a>

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

## Yêu cầu <a id="prerequisites"></a>

| Yêu cầu | Chi tiết |
| --- | --- |
| Node.js | 18+ (khuyến nghị: Node.js 18.17+ hoặc 20 LTS cho Next.js 13) |
| Quản lý gói | npm (dự án dùng `package-lock.json`) |
| Truy cập API | Khóa API OpenAI |
| Truy cập TTS | Khóa API ElevenLabs và voice ID |
| Máy khách | Trình duyệt desktop có quyền truy cập micro (UX mobile hiện vẫn ưu tiên desktop) |

## Cài đặt <a id="installation"></a>

1. Clone kho:

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. Sao chép mẫu môi trường và chỉnh sửa giá trị:

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL="" # Optional
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. Cài đặt phụ thuộc:

```sh
npm install
```

4. Chạy ứng dụng cục bộ:

```sh
npm run dev
```

5. Mở ứng dụng tại `http://localhost:3000`.

Giả định: nếu bạn kiểm tra quyền micro trên domain không cục bộ, thường cần HTTPS.

6. Triển khai lên Vercel:

Dự án này theo quy trình triển khai mặc định của Next.js. Hãy dùng cấu hình import mặc định của Vercel và đặt cùng biến môi trường trong dự án của bạn.

## Cấu hình <a id="configuration"></a>

Các biến môi trường được sử dụng:

| Biến | Bắt buộc | Mô tả |
| --- | --- | --- |
| `OPENAI_API_KEY` | Có | Khóa API dùng cho phiên âm Whisper và hoàn tất chat của GPT. |
| `OPENAI_BASE_URL` | Không | Ghi đè tuỳ chọn URL cơ sở API OpenAI (proxy/gateway). |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Có | Khóa API ElevenLabs dùng trong request TTS bên phía trình duyệt. |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Có | ID giọng nói ElevenLabs cho tổng hợp TTS. |

Ghi chú:

- Biến `NEXT_PUBLIC_*` được Next.js phơi ra phía client theo quy ước.
- `speechToText` hiện ghi file âm thanh tạm thời vào `/tmp/input.webm` trước khi phiên âm.

## Sử dụng <a id="usage"></a>

1. Mở ứng dụng trên trình duyệt desktop.
2. Nhấp một lần vào hình cầu trợ lý và cấp quyền micro.
3. Nhấp lại để bắt đầu ghi âm, rồi nhấp lại để dừng và gửi.
4. Aura phiên âm đầu vào của bạn, sinh phản hồi, sau đó phát giọng nói tổng hợp.

Các script cục bộ:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## Ví dụ API <a id="api-examples"></a>

Các ví dụ này hữu ích cho gỡ lỗi route API cục bộ.

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

Dạng phản hồi mong đợi:

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

Dạng phản hồi mong đợi:

```json
"Assistant response text"
```

## Ghi chú phát triển <a id="development-notes"></a>

- Route chat được cấu hình chạy trên Edge runtime (`export const runtime = "edge"`).
- Route Whisper chạy phía server và phụ thuộc vào quyền truy cập hệ thống tệp cho bộ nhớ tạm.
- Giao diện hiện đang hiển thị thông điệp dự phòng mobile thay cho tương tác mobile đầy đủ.
- Thông báo toast được dùng để hiển thị trạng thái quyền, đang nghe và đang suy nghĩ.
- Prompt hiện tại yêu cầu câu trả lời ngắn gọn (`Your answer has to be as concise as possible.`).
- Log runtime, khả năng truy vết request và hành vi streaming hiện chưa được kiểm thử trong CI (repo chưa có test tự động).

## Khắc phục sự cố <a id="troubleshooting"></a>

### 🎤 Hộp thoại xin quyền micro không xuất hiện

- Đảm bảo trình duyệt cho phép truy cập micro cho `localhost`.
- Dùng HTTPS khi thử nghiệm trên các domain không phải localhost.

### 🔈 Không có âm thanh phát lại

- Kiểm tra `NEXT_PUBLIC_ELEVENLABS_API_KEY` và `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`.
- Xác nhận các ràng buộc autoplay/audio-context của trình duyệt (cần tương tác từ người dùng).

### 📡 API trả về 500 từ `/api/speechToText`

- Xác nhận `OPENAI_API_KEY` đã được đặt.
- Kiểm tra input có chứa âm thanh `webm` mã hóa base64 hợp lệ.

### 📡 API trả về 500 từ `/api/chat`

- Xác nhận `OPENAI_API_KEY` và `OPENAI_BASE_URL` (nếu có) chính xác.
- Kiểm tra tính khả dụng của mô hình `gpt-4o` trong tài khoản OpenAI của bạn.

### ⏳ Độ trễ cao

- Thời gian tổng hợp TTS thường chiếm ưu thế trong độ trễ đầu-cuối.
- Giữ prompt ngắn gọn và cân nhắc tách các phản hồi dài.

## Lộ trình <a id="roadmap"></a>

Các cải tiến tiềm năng suy ra từ mã hiện tại và ghi chú:

- Hỗ trợ tương tác ưu tiên mobile (thay thế cơ chế khóa desktop-only hiện tại).
- Phát dần các phản hồi phụ của trợ lý theo luồng để giảm độ trễ cảm nhận.
- UX retry/lỗi tốt hơn cho lỗi phiên âm và TTS.
- Thêm kiểm thử tự động và kiểm tra CI.
- Mở rộng tài liệu đa ngôn ngữ dưới [`/i18n`](./i18n/).

## Đóng góp <a id="contributing"></a>

Đóng góp luôn được chào đón và đánh giá cao.

- Đọc [CONTRIBUTING.md](./CONTRIBUTING.md) để biết quy trình và kỳ vọng.
- Đọc [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) trước khi tham gia.
- Tạo issue cho lỗi hoặc ý tưởng tính năng:
- Báo lỗi: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- Yêu cầu tính năng: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## Liên hệ <a id="contact"></a>

Xin chào! Cảm ơn bạn đã ghé thăm và dùng thư viện này. Nếu bạn muốn trao đổi về dự án, cần định hướng, đang cân nhắc thuê tôi hoặc chỉ muốn chat, mình rất sẵn lòng trao đổi.

Bạn có thể gửi email tới: `j.schoen@mail.com` hoặc nhắn trên Twitter: [@julianschoen](https://twitter.com/julianschoen)

Nếu bạn muốn đóng góp lại, mình có tài khoản Buy Me A Coffee:

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

Cảm ơn và chúc bạn một ngày tuyệt vời 👋

## Tuyên bố từ chối <a id="disclaimer"></a>

Voice Assistant là ứng dụng thử nghiệm và được cung cấp "nguyên trạng", không có bất kỳ bảo hành nào, rõ ràng hay ngầm định. Khi sử dụng phần mềm này, bạn đồng ý chấp nhận mọi rủi ro liên quan, kể cả mất dữ liệu, lỗi hệ thống hoặc các vấn đề khác có thể phát sinh.

Những nhà phát triển và đóng góp của dự án không chịu trách nhiệm đối với bất kỳ tổn thất, thiệt hại hay hậu quả nào có thể xảy ra từ việc sử dụng phần mềm này. Bạn hoàn toàn chịu trách nhiệm cho mọi quyết định và hành động dựa trên thông tin do Voice Assistant cung cấp.

Lưu ý: việc sử dụng mô hình ngôn ngữ GPT-4 có thể tốn chi phí đáng kể do tiêu thụ token. Khi dùng dự án này, bạn có trách nhiệm theo dõi và quản lý chi phí token của mình. Nên kiểm tra thường xuyên lượng sử dụng API OpenAI của bạn và thiết lập các giới hạn hoặc cảnh báo cần thiết để ngăn phí phát sinh ngoài dự tính.

Khi sử dụng Voice Assistant, bạn đồng ý bồi thường, bảo vệ và giữ cho các nhà phát triển, người đóng góp và các bên liên quan không phải chịu trách nhiệm cho mọi khiếu nại, thiệt hại, mất mát, trách nhiệm pháp lý, chi phí và chi tiêu (bao gồm cả phí luật sư hợp lý) phát sinh do phần mềm này hoặc vi phạm các điều khoản này.

<!-- LICENSE -->

## Giấy phép <a id="license"></a>

Được phân phối theo Giấy phép MIT. Xem `LICENSE` để biết thêm chi tiết.

Lưu ý: repository này hiện lưu file giấy phép tại [`LICENCE`](./LICENCE).


## ❤️ Support

| Donate | PayPal | Stripe |
| --- | --- | --- |
| [![Donate](https://camo.githubusercontent.com/24a4914f0b42c6f435f9e101621f1e52535b02c225764b2f6cc99416926004b7/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f446f6e6174652d4c617a79696e674172742d3045413545393f7374796c653d666f722d7468652d6261646765266c6f676f3d6b6f2d6669266c6f676f436f6c6f723d7768697465)](https://chat.lazying.art/donate) | [![PayPal](https://camo.githubusercontent.com/d0f57e8b016517a4b06961b24d0ca87d62fdba16e18bbdb6aba28e978dc0ea21/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f50617950616c2d526f6e677a686f754368656e2d3030343537433f7374796c653d666f722d7468652d6261646765266c6f676f3d70617970616c266c6f676f436f6c6f723d7768697465)](https://paypal.me/RongzhouChen) | [![Stripe](https://camo.githubusercontent.com/1152dfe04b6943afe3a8d2953676749603fb9f95e24088c92c97a01a897b4942/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f5374726970652d446f6e6174652d3633354246463f7374796c653d666f722d7468652d6261646765266c6f676f3d737472697065266c6f676f436f6c6f723d7768697465)](https://buy.stripe.com/aFadR8gIaflgfQV6T4fw400) |
