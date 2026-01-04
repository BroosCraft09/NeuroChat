# 🧠 NeuroChat - AI Chat Assistant

NeuroChat adalah aplikasi chat AI modern yang dibangun dengan Vanilla JavaScript dan powered by Groq API. Aplikasi ini menawarkan interface yang clean, responsif, dan user-friendly untuk berinteraksi dengan berbagai model AI.

![NeuroChat Preview](https://via.placeholder.com/800x400/6366f1/ffffff?text=NeuroChat)

## ✨ Fitur Utama

- 🤖 **Multi-Model Support**: Llama 3 70B, Mixtral 8x7B, Gemma 7B
- 💬 **Chat Interface Modern**: Design mirip ChatGPT/Claude
- 📝 **Markdown Support**: Render markdown dengan syntax highlighting
- 💾 **Chat History**: Simpan dan load riwayat chat
- 🎨 **Dark/Light Theme**: Toggle tema sesuai preferensi
- 📱 **Responsive Design**: Optimal di desktop dan mobile
- ⚙️ **Customizable Settings**: Atur temperature, max tokens, dll
- 📥 **Export Chat**: Download chat sebagai file TXT
- ⚡ **Fast & Secure**: Backend di Netlify Functions

## 🛠️ Tech Stack

- **Frontend**: HTML5, CSS3, Vanilla JavaScript
- **Backend**: Netlify Functions (Serverless)
- **AI Provider**: Groq API
- **Libraries**:
  - Marked.js (Markdown parsing)
  - Highlight.js (Code syntax highlighting)
  - Font Awesome (Icons)
  - Google Fonts (Inter)

## 📦 Struktur Proyek

```
neurochat/
├── index.html              # Halaman utama
├── style.css               # Styling
├── script.js               # Logic frontend
├── netlify/
│   └── functions/
│       └── chat.js         # Backend API handler
├── netlify.toml            # Netlify configuration
├── package.json            # Dependencies
├── .env.example            # Template environment variables
├── .gitignore              # Git ignore rules
└── README.md               # Documentation (file ini)
```

## 🚀 Cara Deploy ke Netlify

### 1. Persiapan

Pastikan Anda memiliki:
- Akun GitHub (gratis)
- Akun Netlify (gratis)
- Groq API Key (gratis dari [console.groq.com](https://console.groq.com))

### 2. Setup Repository GitHub

```bash
# Clone atau download project ini
git clone https://github.com/yourusername/neurochat.git
cd neurochat

# Atau buat repo baru
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/neurochat.git
git push -u origin main
```

### 3. Deploy ke Netlify

**Opsi A: Via Website (Recommended)**

1. Login ke [netlify.app](https://app.netlify.com)
2. Klik "Add new site" → "Import an existing project"
3. Pilih "GitHub" dan authorize Netlify
4. Pilih repository "neurochat"
5. Build settings (biarkan default):
   - Build command: (kosongkan)
   - Publish directory: `.`
6. Klik "Deploy site"

**Opsi B: Via Netlify CLI**

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Login
netlify login

# Deploy
netlify deploy --prod
```

### 4. Set Environment Variable

Setelah deploy berhasil:

1. Buka dashboard site Anda di Netlify
2. Go to: **Site settings** → **Environment variables**
3. Klik "Add a variable"
4. Tambahkan:
   - **Key**: `GROQ_API_KEY`
   - **Value**: `gsk_xxxxxxxxxx` (API key Anda dari Groq)
5. Klik "Create variable"
6. **Trigger redeploy**: Deploys → Trigger deploy → Deploy site

### 5. Dapatkan Groq API Key

1. Kunjungi [console.groq.com](https://console.groq.com)
2. Sign up / Login (gratis)
3. Go to: API Keys
4. Klik "Create API Key"
5. Copy key yang dihasilkan (format: `gsk_...`)

### 6. Verifikasi Deployment

1. Buka URL site Anda (misalnya: `https://your-site-name.netlify.app`)
2. Test chat dengan mengirim pesan
3. Check browser console jika ada error

## 💻 Development Lokal

### Setup

```bash
# Install dependencies
npm install

# Copy environment template
cp .env.example .env

# Edit .env dan isi GROQ_API_KEY
nano .env
```

### Jalankan Development Server

```bash
# Menggunakan Netlify Dev (recommended)
npm run dev

# Atau menggunakan Netlify CLI langsung
netlify dev
```

Buka browser di `http://localhost:8888`

### Testing Netlify Function

```bash
# Test function langsung
curl -X POST http://localhost:8888/.netlify/functions/chat \
  -H "Content-Type: application/json" \
  -d '{
    "messages": [{"role": "user", "content": "Hello"}],
    "model": "llama3-70b-8192",
    "temperature": 0.7,
    "max_tokens": 1024
  }'
```

## ⚙️ Konfigurasi

### Model AI yang Tersedia

| Model | ID | Keterangan |
|-------|----|-----------| 
| Llama 3 70B | `llama3-70b-8192` | Recommended, paling pintar |
| Mixtral 8x7B | `mixtral-8x7b-32768` | Context window besar |
| Gemma 7B | `gemma-7b-it` | Lightweight, cepat |

### Settings Parameter

- **Temperature** (0-2): Kreativitas respons
  - 0 = Presisi tinggi, konsisten
  - 1 = Balanced
  - 2 = Sangat kreatif, variatif

- **Max Tokens** (100-4096): Panjang respons maksimal
  - 1024 = Default, cocok untuk chat
  - 2048 = Untuk respons panjang
  - 4096 = Maximum

## 🔒 Keamanan

### Best Practices

✅ **DO:**
- Simpan API key di environment variables
- Gunakan rate limiting
- Validate input di backend
- Set proper CORS headers
- Monitor usage di Groq dashboard

❌ **DON'T:**
- Commit `.env` ke Git
- Hardcode API key di frontend
- Expose API key di client-side code
- Skip input validation

### Rate Limiting

Backend sudah include rate limiting:
- **10 requests per minute** per IP address
- Error 429 jika limit terlampaui
- Counter reset setiap 1 menit

## 🐛 Troubleshooting

### Error: "API authentication failed"

**Solusi:**
1. Pastikan `GROQ_API_KEY` sudah di-set di Netlify
2. Verify format key benar (`gsk_...`)
3. Check key masih valid di Groq console
4. Trigger redeploy setelah set env variable

### Error: "Rate limit exceeded"

**Solusi:**
1. Wait 1 minute dan coba lagi
2. Jika terlalu sering, pertimbangkan upgrade Groq plan
3. Implement caching di frontend untuk reduce requests

### Chat tidak muncul / Loading terus

**Solusi:**
1. Check browser console untuk error
2. Verify Netlify function deployed dengan benar
3. Test function endpoint manual dengan curl
4. Check Network tab di DevTools untuk status response

### Styling tidak muncul

**Solusi:**
1. Clear browser cache (Ctrl+Shift+R)
2. Verify `style.css` loaded di Network tab
3. Check CSS file path di HTML

## 📱 Keyboard Shortcuts

- `Enter`: Send message
- `Shift + Enter`: New line dalam message
- `Ctrl + N`: New chat
- `Ctrl + /`: Focus input

## 🎨 Customization

### Ubah Warna Tema

Edit CSS variables di `style.css`:

```css
:root {
    --accent-primary: #6366f1;  /* Warna utama */
    --accent-secondary: #8b5cf6; /* Warna sekunder */
    /* ... dst */
}
```

### Tambah Model AI Baru

1. Edit `index.html` - tambah option di select:
```html
<option value="new-model-id">New Model Name</option>
```

2. Pastikan model supported oleh Groq

### Ubah System Prompt

Edit di `netlify/functions/chat.js`, tambahkan system message:

```javascript
messages: [
    {
        role: 'system',
        content: 'You are a helpful assistant...'
    },
    ...messages
]
```

## 📊 Monitoring

### Check Usage di Groq Dashboard

1. Login ke [console.groq.com](https://console.groq.com)
2. Go to Usage → Analytics
3. Monitor:
   - Requests per day
   - Token usage
   - Error rates

### Netlify Analytics

1. Site overview di Netlify dashboard
2. Check:
   - Function invocations
   - Build minutes
   - Bandwidth usage

## 🔄 Update & Maintenance

### Update Dependencies

```bash
# Check outdated packages
npm outdated

# Update
npm update

# Update Groq SDK specifically
npm install groq-sdk@latest
```

### Redeploy

```bash
# Via Git push (auto deploy)
git add .
git commit -m "Update"
git push

# Via Netlify CLI
netlify deploy --prod
```

## 🤝 Contributing

Contributions welcome! Please:

1. Fork repository
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

## 📄 License

MIT License - bebas digunakan untuk project personal maupun komersial.

## 🙏 Credits

- **Groq** - AI Infrastructure
- **Netlify** - Hosting & Serverless Functions
- **Marked.js** - Markdown Parser
- **Highlight.js** - Syntax Highlighting
- **Font Awesome** - Icons

## 📞 Support

Jika ada pertanyaan atau issue:

1. Check [Troubleshooting](#-troubleshooting) section
2. Open issue di GitHub
3. Contact: [your-email@example.com]

---

**Made with ❤️ by Rahadian**

*Powered by Groq & Netlify*
