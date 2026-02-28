[English](../README.md) · [العربية](README.ar.md) · [Español](README.es.md) · [Français](README.fr.md) · [日本語](README.ja.md) · [한국어](README.ko.md) · [Tiếng Việt](README.vi.md) · [中文 (简体)](README.zh-Hans.md) · [中文（繁體）](README.zh-Hant.md) · [Deutsch](README.de.md) · [Русский](README.ru.md)


<a name="readme-top"></a>

<br />
<div align="center">

<h3 align="center">Chào Aura 👋</h3>

<p align="center">
Aura là một trợ lý giọng nói thông minh, được tối ưu cho phản hồi độ trễ thấp. Dự án sử dụng Vercel Edge Functions, nhận dạng giọng nói Whisper, GPT-4o và phát trực tuyến TTS từ ElevenLabs.
<br />
<br />
<a href="https://voice.julianschoen.co">Xem Demo</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=">Báo lỗi</a>
·
<a href="https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=">Đề xuất tính năng</a>
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

- [Tổng quan](#tổng-quan)
- [Tính năng](#tính-năng)
- [Demo](#demo)
- [Động lực](#động-lực)
- [Suy nghĩ về độ trễ và trải nghiệm người dùng](#suy-nghĩ-về-độ-trễ-và-trải-nghiệm-người-dùng)
- [Kiến trúc](#kiến-trúc)
- [Cấu trúc dự án](#cấu-trúc-dự-án)
- [Điều kiện tiên quyết](#điều-kiện-tiên-quyết)
- [Cài đặt](#cài-đặt)
- [Cấu hình](#cấu-hình)
- [Cách sử dụng](#cách-sử-dụng)
- [Ví dụ API](#ví-dụ-api)
- [Ghi chú phát triển](#ghi-chú-phát-triển)
- [Khắc phục sự cố](#khắc-phục-sự-cố)
- [Lộ trình](#lộ-trình)
- [Đóng góp](#đóng-góp)
- [Liên hệ](#liên-hệ)
- [Tuyên bố miễn trừ trách nhiệm](#tuyên-bố-miễn-trừ-trách-nhiệm)
- [Giấy phép](#giấy-phép)

## Tổng quan

Aura là một trợ lý giọng nói kiểu Siri chạy trong trình duyệt, được xây dựng bằng Next.js (App Router) và TypeScript.

### Tóm tắt nhanh

| Khu vực | Chi tiết |
| --- | --- |
| Mục tiêu chính | Tương tác giọng nói nhanh, thực tiễn, độ trễ thấp trên web |
| Mô hình runtime | Ghi âm trên trình duyệt + API routes phía server + chat endpoint trên Edge |
| Speech-to-text | OpenAI Whisper (`whisper-1`) |
| Mô hình trợ lý | OpenAI GPT-4o |
| Text-to-speech | Phát trực tuyến ElevenLabs trong trình duyệt |

Vòng lặp tương tác gồm:

1. Thu âm micro trong trình duyệt.
2. Chuyển giọng nói thành văn bản bằng OpenAI Whisper (`whisper-1`).
3. Tạo câu trả lời ngắn gọn bằng OpenAI GPT-4o.
4. Phát trực tuyến âm thanh tổng hợp trả về cho người dùng bằng ElevenLabs.

Dự án được tối ưu xoay quanh UX độ trễ thấp trong thực tế, có phản hồi trực quan khi trợ lý đang lắng nghe hoặc suy nghĩ.

## Tính năng

✅ Trợ lý giọng nói kiểu Siri ngay trong trình duyệt  
✅ Tối ưu cho phản hồi độ trễ thấp  
✅ Xây dựng với OpenAI, nhận dạng giọng nói Whisper và ElevenLabs

Chi tiết triển khai bổ sung:

- Next.js 13 App Router với TypeScript.
- Chat endpoint chạy Edge runtime (`/api/chat`).
- Phản hồi tương tác bằng toast (quyền micro, đang lắng nghe, đang suy nghĩ).
- Nút trợ lý có hoạt ảnh cùng phát lại TTS dạng stream.
- Tùy chọn ghi đè OpenAI base URL cho thiết lập proxy/gateway self-hosted.

## Demo

Bạn có thể thử Aura tại đây: [https://voice.julianschoen.co](https://voice.julianschoen.co)

## Động lực

Trợ lý giọng nói đã trở thành một phần không thể thiếu trong đời sống hằng ngày: điện thoại, ô tô, nhà ở, và nhiều hơn thế. Đưa trải nghiệm đó lên web với độ phản hồi tốt trước đây vốn rất khó.

Cho đến gần đây, vấn đề chính của trợ lý giọng nói trên web là độ trễ. Mất quá nhiều thời gian để gửi âm thanh lên server, tạo phản hồi từ LLM, rồi stream giọng nói trở lại. Những tiến bộ gần đây từ OpenAI, ElevenLabs và Vercel đã giúp việc xây một trợ lý giọng nói đủ nhanh để dùng thực tế trên web trở nên khả thi.

Repository này hướng đến việc trở thành điểm tham khảo cho những ai muốn tự xây trợ lý giọng nói của riêng mình và hiểu các trade-off trong triển khai thực tế.

## Suy nghĩ về độ trễ và trải nghiệm người dùng

Độ trễ là yếu tố quan trọng nhất đối với một UX giọng nói tốt. Hiện có ba yếu tố đóng góp chính:

- Thời gian phiên âm (nhận dạng giọng nói Whisper).
- Thời gian tạo phản hồi (GPT-4o Mini trong ghi chú dự án ban đầu).
- Thời gian stream tổng hợp giọng nói (ElevenLabs TTS).

Theo ghi chú thử nghiệm thực tế, quá trình tạo giọng nói thường tốn nhiều thời gian nhất và khó dự đoán nhất, đặc biệt với phản hồi dài.

Một chiến lược giảm thiểu khả dĩ là chia phản hồi thành nhiều phần và stream lần lượt từng phần. Cách này cho phép người dùng bắt đầu nghe sớm hơn trong khi phần còn lại vẫn đang được tạo. Hiện chưa được triển khai, nhưng là một hướng đi đầy hứa hẹn.

Một khái niệm quan trọng khác là thời gian chờ cảm nhận. Ngay cả khi tổng độ trễ không đổi, người dùng vẫn chấp nhận tốt hơn nếu nhận được phản hồi ngay lập tức. Dự án hiện có thông báo "thinking" trong lúc xử lý để cải thiện cảm nhận về độ phản hồi.

## Kiến trúc

```text
Browser (MediaRecorder)
  -> POST /api/speechToText (OpenAI Whisper transcription)
  -> POST /api/chat (OpenAI GPT-4o, Edge runtime)
  -> ElevenLabs TTS stream playback in browser (AudioContext)
```

Các tệp chính:

- `src/components/AssistantButton/AssistantButton.tsx`: trạng thái ghi âm, điều phối request, phát lại.
- `src/app/api/speechToText/route.ts`: base64 audio -> `/tmp/input.webm` -> Whisper transcription.
- `src/app/api/chat/route.ts`: chat completion qua OpenAI.
- `src/app/page.tsx`: giao diện ưu tiên desktop và thông báo fallback cho mobile.

## Cấu trúc dự án

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

## Điều kiện tiên quyết

- Node.js 18+ (khuyến nghị: Node.js 18.17+ hoặc 20 LTS cho Next.js 13).
- npm (dự án dùng `package-lock.json`).
- OpenAI API key.
- ElevenLabs API key và voice ID.
- Trình duyệt desktop có quyền truy cập micro (UX trên mobile hiện còn hạn chế theo thiết kế).

## Cài đặt

1. Clone repo:

```sh
git clone https://github.com/ntegrals/aura-voice
```

2. Lấy API key từ [https://openai.com/](https://openai.com/) và [https://elevenlabs.com/](https://elevenlabs.com/).

Sao chép tệp `.env.example` thành `.env.local` rồi thêm key của bạn:

```sh
cp .env.example .env.local
```

```sh
OPENAI_API_KEY="YOUR OPENAI API KEY"
OPENAI_BASE_URL=(Optional)
NEXT_PUBLIC_ELEVENLABS_API_KEY="YOUR ELEVENLABS API KEY"
NEXT_PUBLIC_ELEVENLABS_VOICE_ID="YOUR ELEVENLABS VOICE ID"
```

3. Cài dependencies:

```sh
npm install
```

4. Chạy ứng dụng local:

```sh
npm run dev
```

5. Triển khai lên Vercel:

Dự án này tương thích với luồng triển khai Vercel tiêu chuẩn cho Next.js.

## Cấu hình

Các biến môi trường được dùng trong dự án:

| Biến | Bắt buộc | Mô tả |
| --- | --- | --- |
| `OPENAI_API_KEY` | Có | API key dùng cho Whisper transcription và GPT chat completion. |
| `OPENAI_BASE_URL` | Không | Tùy chọn ghi đè OpenAI API base URL (proxy/gateway). |
| `NEXT_PUBLIC_ELEVENLABS_API_KEY` | Có | ElevenLabs API key dùng cho request TTS phía trình duyệt. |
| `NEXT_PUBLIC_ELEVENLABS_VOICE_ID` | Có | ElevenLabs voice ID dùng để tổng hợp TTS. |

Ghi chú:

- Biến `NEXT_PUBLIC_*` được Next.js expose ra phía client theo quy ước.
- `speechToText` hiện ghi âm thanh tạm vào `/tmp/input.webm` trước khi phiên âm.

## Cách sử dụng

1. Mở ứng dụng trong trình duyệt desktop.
2. Nhấn vào orb trợ lý một lần và cấp quyền micro.
3. Nhấn lần nữa để bắt đầu ghi âm, sau đó nhấn lại để dừng và gửi.
4. Aura phiên âm đầu vào của bạn, tạo phản hồi, rồi phát giọng nói tổng hợp.

Các script local:

```sh
npm run dev
npm run build
npm run start
npm run lint
```

## Ví dụ API

Các ví dụ này hữu ích để debug API routes local.

### `POST /api/speechToText`

```bash
curl -X POST http://localhost:3000/api/speechToText \
  -H "Content-Type: application/json" \
  -d '{"audio":"<base64-webm-audio>"}'
```

Định dạng phản hồi dự kiến:

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

Định dạng phản hồi dự kiến:

```json
"Assistant response text"
```

## Ghi chú phát triển

- Chat route được cấu hình cho Edge runtime (`export const runtime = "edge"`).
- Whisper route chạy phía server và phụ thuộc quyền truy cập hệ thống tệp để lưu tạm.
- UI hiện hiển thị thông báo fallback cho mobile thay vì tương tác đầy đủ trên mobile.
- Toast notifications được dùng để hiển thị trạng thái quyền/lắng nghe/suy nghĩ.
- Prompt shaping hiện yêu cầu trả lời ngắn gọn (`Your answer has to be as consise as possible.`).

## Khắc phục sự cố

### Không xuất hiện hộp thoại xin quyền micro

- Đảm bảo trình duyệt của bạn cho phép truy cập micro với `localhost`.
- Dùng HTTPS khi kiểm thử trên domain không phải localhost.

### Không phát được âm thanh

- Kiểm tra `NEXT_PUBLIC_ELEVENLABS_API_KEY` và `NEXT_PUBLIC_ELEVENLABS_VOICE_ID`.
- Xác minh giới hạn autoplay/audio-context của trình duyệt (cần có tương tác người dùng).

### API 500 từ `/api/speechToText`

- Xác nhận `OPENAI_API_KEY` đã được thiết lập.
- Kiểm tra đầu vào chứa âm thanh `webm` mã hóa base64 hợp lệ.

### API 500 từ `/api/chat`

- Xác nhận `OPENAI_API_KEY` và `OPENAI_BASE_URL` (nếu dùng) là chính xác.
- Kiểm tra khả dụng mô hình `gpt-4o` trong tài khoản OpenAI của bạn.

### Độ trễ cao

- Thời gian tổng hợp TTS thường chiếm phần lớn độ trễ đầu-cuối.
- Giữ prompt ngắn gọn và cân nhắc chia nhỏ phản hồi dài.

## Lộ trình

Các cải tiến tiềm năng tiếp theo được suy ra từ mã và ghi chú hiện tại:

- Hỗ trợ tương tác mobile-first (thay thế cơ chế chỉ cho desktop hiện tại).
- Streaming từng phần phản hồi của trợ lý để giảm độ trễ cảm nhận.
- Cải thiện UX retry/lỗi cho các lỗi phiên âm và TTS.
- Thêm kiểm thử tự động và kiểm tra CI.
- Mở rộng tài liệu đa ngôn ngữ trong [`/i18n`](./i18n/).

## Đóng góp

Rất hoan nghênh và trân trọng mọi đóng góp.

- Đọc [CONTRIBUTING.md](./CONTRIBUTING.md) để nắm quy trình và kỳ vọng.
- Đọc [CODE_OF_CONDUCT.md](./CODE_OF_CONDUCT.md) trước khi tham gia.
- Mở issue cho lỗi hoặc ý tưởng tính năng:
- Báo lỗi: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=bug&projects=&template=bug_report.md&title=)
- Yêu cầu tính năng: [template](https://github.com/ntegrals/aura-voice/issues/new?assignees=&labels=enhancement&projects=&template=feature_request.md&title=)

## Liên hệ

Xin chào! Cảm ơn bạn đã xem và sử dụng thư viện này. Nếu bạn muốn trao đổi về dự án của mình, cần mentorship, cân nhắc thuê tôi, hoặc chỉ đơn giản là trò chuyện, tôi rất sẵn lòng.

Bạn có thể gửi email cho tôi: `j.schoen@mail.com` hoặc nhắn trên Twitter: [@julianschoen](https://twitter.com/julianschoen)

Nếu bạn muốn ủng hộ lại, tôi có trang Buy Me A Coffee:

<a href="https://www.buymeacoffee.com/ntegrals">
<img src=".assets/buymeacoffee.png" alt="buymeacoffee" width="192">
</a>

Cảm ơn bạn và chúc một ngày tuyệt vời 👋

## Tuyên bố miễn trừ trách nhiệm

Voice Assistant là một ứng dụng thử nghiệm và được cung cấp theo trạng thái "as-is", không có bất kỳ bảo đảm nào, dù rõ ràng hay ngụ ý. Khi sử dụng phần mềm này, bạn đồng ý tự chịu mọi rủi ro liên quan đến việc sử dụng, bao gồm nhưng không giới hạn ở mất dữ liệu, lỗi hệ thống hoặc bất kỳ vấn đề nào khác có thể phát sinh.

Các nhà phát triển và cộng tác viên của dự án này không chấp nhận bất kỳ trách nhiệm pháp lý nào đối với tổn thất, thiệt hại hoặc hậu quả khác có thể xảy ra do việc sử dụng phần mềm này. Bạn hoàn toàn chịu trách nhiệm cho mọi quyết định và hành động dựa trên thông tin do Voice Assistant cung cấp.

Xin lưu ý rằng việc sử dụng mô hình ngôn ngữ GPT-4 có thể tốn kém do mức sử dụng token. Khi dùng dự án này, bạn thừa nhận rằng bạn có trách nhiệm tự theo dõi và quản lý mức sử dụng token cũng như các chi phí liên quan. Rất khuyến nghị kiểm tra mức sử dụng OpenAI API thường xuyên và thiết lập giới hạn hoặc cảnh báo cần thiết để tránh phát sinh phí ngoài dự kiến.

Khi sử dụng Voice Assistant, bạn đồng ý bồi thường, bảo vệ và miễn trừ trách nhiệm cho các nhà phát triển, cộng tác viên và mọi bên liên quan khỏi mọi khiếu nại, thiệt hại, tổn thất, trách nhiệm pháp lý, chi phí và khoản phí (bao gồm phí luật sư hợp lý) phát sinh từ việc bạn sử dụng phần mềm này hoặc vi phạm các điều khoản này.

<!-- LICENSE -->

## Giấy phép

Phân phối theo giấy phép MIT. Xem `LICENSE` để biết thêm thông tin.

Ghi chú repository: repository này hiện lưu tệp giấy phép dưới tên [`LICENCE`](./LICENCE).
