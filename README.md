# 🐱 Meo AI

Ứng dụng chat AI đơn giản, giao diện đẹp kiểu ChatGPT, sử dụng **Groq API** với model **LLaMA 3.1** làm backend. Toàn bộ frontend là một file HTML duy nhất, backend là một Express server nhỏ gọn.

---

## ✨ Tính năng

- 💬 Chat hội thoại với AI (LLaMA 3.1 qua Groq)
- 🕓 Lịch sử chat theo thời gian (Hôm nay / Hôm qua / 7 ngày trước / Cũ hơn)
- 📌 Ghim / bỏ ghim đoạn chat
- ✏️ Đổi tên cuộc hội thoại
- 🗑️ Xoá cuộc hội thoại
- 🔍 Tìm kiếm cuộc hội thoại
- 🌗 Chuyển đổi Dark / Light mode
- 📱 Sidebar thu gọn (icon-only rail)
- 🔤 Giao diện tiếng Việt

---

## 🗂️ Cấu trúc dự án

```
meoAI/
├── index.html      # Toàn bộ giao diện frontend (HTML + CSS + JS)
├── server.js       # Express server – proxy đến Groq API
├── package.json    # Cấu hình npm
├── .env            # Chứa GROQ_API_KEY (không commit lên git)
└── node_modules/   # Thư viện (tự sinh sau npm install)
```

---

## 🚀 Cài đặt & Chạy

### Yêu cầu

- [Node.js](https://nodejs.org/) v18 trở lên
- Tài khoản [Groq](https://console.groq.com/) để lấy API key (miễn phí)

### Các bước

```bash
# 1. Clone hoặc giải nén dự án
cd meoAI

# 2. Cài dependencies
npm install

# 3. Tạo file .env (nếu chưa có)
echo "GROQ_API_KEY=your_api_key_here" > .env

# 4. Khởi động server
npm start
```

Server sẽ chạy tại `http://localhost:3000`.

### Mở giao diện

Mở file `index.html` trực tiếp trong trình duyệt (double-click), hoặc dùng extension **Live Server** trong VS Code.

> ⚠️ Frontend gọi đến `http://localhost:3000/chat` — server phải đang chạy thì mới nhận được phản hồi từ AI.

---

## ⚙️ Cấu hình

| Biến môi trường | Mô tả |
|---|---|
| `GROQ_API_KEY` | API key từ [console.groq.com](https://console.groq.com/) |

Model mặc định: `llama-3.1-8b-instant`. Để đổi model, sửa dòng sau trong `index.html`:

```js
body: JSON.stringify({ model: 'llama-3.1-8b-instant', messages: [...] })
```

Các model Groq phổ biến: `llama-3.3-70b-versatile`, `mixtral-8x7b-32768`, `gemma2-9b-it`.

---

## 🔌 API

Backend expose một endpoint duy nhất:

### `POST /chat`

Proxy request trực tiếp đến Groq API với format tương thích OpenAI.

**Request body:**
```json
{
  "model": "llama-3.1-8b-instant",
  "messages": [
    { "role": "user", "content": "Xin chào!" }
  ]
}
```

**Response:** Trả về nguyên JSON từ Groq (`choices[0].message.content`).

---

## 📦 Dependencies

| Package | Phiên bản | Mục đích |
|---|---|---|
| `express` | ^4.19.2 | HTTP server |
| `cors` | ^2.8.5 | Cho phép frontend gọi API cross-origin |
| `dotenv` | ^16.4.5 | Đọc biến môi trường từ `.env` |
| `node-fetch` | ^3.3.2 | Gọi HTTP đến Groq API |

---

## 🛠️ Phát triển thêm

Một số ý tưởng mở rộng:

- [ ] Lưu lịch sử chat vào `localStorage` để không mất khi reload
- [ ] Cho phép chọn model từ giao diện
- [ ] Thêm system prompt / persona tuỳ chỉnh
- [ ] Hỗ trợ streaming response
- [ ] Deploy lên Railway / Render / VPS

---

## 📄 License

ISC
