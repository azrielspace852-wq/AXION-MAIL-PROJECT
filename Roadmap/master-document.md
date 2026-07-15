# AXION MAIL MASTER DOCUMENT
## Versi 1.0 - MVP

### 1. IDENTITAS PROYEK
- Nama: AXION MAIL
- Deskripsi: Aplikasi email seperti Gmail, bisa untuk login di aplikasi lain (AXNDB, XENON-V, DLL)
- Target: Semua kalangan (anak-anak via orang tua, remaja, dewasa, lansia di 10 negara)
- Status: MVP (Telegram Bot)

### 2. TEKNOLOGI
- Interface: Telegram Bot (grammY)
- Backend: Cloudflare Worker (serverless)
- Main DB: Firebase Firestore
- Backup DB: Telegram Channel Private
- Email API: Resend (domain sementara: resend.dev)
- AI: Gemini 1.5 Flash (untuk feedback & deteksi)
- Deployment: Cloudflare Workers + Pages
- Bahasa: Indonesia, Inggris, Chinese, Hong Kong, Korea, Japan, Ukraina, Malaysia, Russia

### 3. FITUR MVP (14 HARI)
1. Registrasi email @resend.dev (parent-child)
   - Umur >= 12 → registrasi bebas
   - Umur < 12 → wajib parentEmail (harus terdaftar)
2. Kirim & terima email (via Resend API)
3. SSO token (JWT) untuk aplikasi lain
4. Backup otomatis ke Telegram Channel (setiap 6 jam)
5. Feedback user (dikirim ke grup)

### 4. STRUKTUR DATABASE (FIRESTORE)
- users: { userId, email, name, umur, passwordHash, createdAt, parentEmail (opsional), isParent: boolean }
- emails: { emailId, from, to, subject, body, timestamp, isRead, isSent }
- sessions: { sessionId, userId, token, device, loginTime, expiresAt }
- sso_tokens: { tokenId, userId, email, applications: ['axndb','xenon-v','dll'], createdAt, expiresAt }
- audit_logs: { logId, userId, action, timestamp, ipAddress }
- feedback: { feedbackId, userId, message, timestamp, analysis (dari Gemini) }

### 5. ENVIRONMENT VARIABLES
TELEGRAM_BOT_TOKEN=xxx
TELEGRAM_CHANNEL_ID=-100xxx
FIREBASE_PROJECT_ID=axion-mail
FIREBASE_PRIVATE_KEY=xxx
RESEND_API_KEY=xxx
RESEND_DOMAIN=resend.dev
JWT_SECRET=xxx
GEMINI_API_KEY=xxx

### 6. KEAMANAN
- Password hash: bcrypt (salt 12)
- Rate limiting: 5 request/menit per user
- Audit log: semua aksi dicatat
- JWT token: expire 1 jam
- Firestore rules: read/write hanya untuk pemilik data
- Backup Channel: PRIVATE

### 7. BACKUP
- Interval: setiap 6 jam (cron di Cloudflare)
- Format: JSON + ringkasan text
- Retention: 30 hari di Channel

### 8. TIM (34 PROFESI) & KORESPONDENSI PROMPT
- Manajemen: PM, PO, BA, Scrum Master, Delivery Manager → Prompt 1-5
- Desain: UI, UX Researcher, UX Writer, Visual, Motion → Prompt 6-10
- Backend: Backend Eng, DBA, DevOps, Security, Integration → Prompt 11-15
- Frontend: Frontend Web, Mobile iOS, Android, Cross-platform, Performance → Prompt 16-20
- QA: Manual, Automation, Performance, Security Tester → Prompt 21-24
- Data: Data Eng, Data Analyst, Data Scientist → Prompt 25-27
- Infra: Network, SysAdmin, IT Support → Prompt 28-30
- Konten: Content Manager, SEO, Digital Marketing → Prompt 31-33
- Legal: Compliance Officer → Prompt 34

### 9. BLOCKIR (TIDAK UNTUK MVP)
- Folder/label email
- Spam filter
- Template email
- Attachment (versi 1)
- Dashboard web (versi 2)
- Fitur gratis lebih luas (versi 2)

### 10. TIMELINE (14 HARI)
Hari 1-2: Manajemen & Desain
Hari 3-5: Backend & Frontend Bot
Hari 6-7: QA & Security
Hari 8-9: Deploy & Testing
Hari 10-14: Fix bug & Polish