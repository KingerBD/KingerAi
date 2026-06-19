# KingerAi v4.0.0

<div align="center">

**Enterprise AI Workspace**

*Multi-Agent • Memory • Artifacts • Code Interpreter • Voice Mode*

[![Version](https://img.shields.io/badge/version-4.0.0-ef233c?style=flat-square)]()
[![Python](https://img.shields.io/badge/Python-3.10+-3776ab?style=flat-square)]()
[![Flask](https://img.shields.io/badge/Flask-3.0-black?style=flat-square)]()
[![License](https://img.shields.io/badge/license-MIT-22c55e?style=flat-square)]()
[![Platform](https://img.shields.io/badge/platform-Linux%20amd64-7c3aed?style=flat-square)]()

**.deb package for Debian / Ubuntu / Linux Mint / Pop!_OS**

</div>

---

## 📋 Table of Contents | فهرست

- [English Documentation](#-english-documentation)
  - [Overview](#-overview)
  - [Features](#-features)
  - [Installation](#-installation)
  - [Usage](#-usage)
  - [Configuration](#-configuration)
  - [API Reference](#-api-reference)
  - [Troubleshooting](#-troubleshooting)
- [مستندات فارسی](#-مستندات-فارسی)
  - [معرفی](#-معرفی)
  - [امکانات](#-امکانات)
  - [نصب](#-نصب)
  - [استفاده](#-استفاده)
  - [تنظیمات](#-تنظیمات)
  - [رفع اشکال](#-رفع-اشکال)

---

# 🇬🇧 English Documentation

## 🎯 Overview

**KingerAi** is a self-hosted, multi-agent AI workspace built on Flask.
It bundles a Python runtime, a modern web UI, and a powerful AI provider
proxy — all in a single `.deb` package that runs out of the box with
**zero configuration**.

The application is powered by the **WormGPT** API and exposes a
ChatGPT-like experience with workspace features inspired by
**Claude**, **Cursor**, and **ChatGPT Plus**.

### What makes it "Enterprise"?

| Capability | Status | Description |
|---|---|---|
| 🤖 Multi-Agent Routing | ✅ Built-in | 5 specialized agents + smart orchestrator |
| 🧠 Long-Term Memory | ✅ Built-in | Persistent facts injected into every chat |
| 📦 Artifacts Panel | ✅ Built-in | Live HTML/SVG/code preview (à la Claude) |
| 💻 Code Interpreter | ✅ Built-in | Sandboxed Python execution |
| 🎤 Voice Mode | ✅ Built-in | Browser-native STT + TTS |
| 📊 Admin Dashboard | ✅ Built-in | Stats, agent usage, service health |
| 🔒 Security | ✅ Built-in | Configurable CORS, JWT-ready, admin token |
| 🚀 Streaming | ✅ Built-in | SSE streaming with stop/regenerate |
| 📎 File Uploads | ✅ Built-in | 20MB per file, 5 files per message |

---

## ✨ Features

### 🤖 Multi-Agent System

KingerAi ships with **5 specialized agents** and a smart orchestrator
that automatically routes each user message to the most appropriate one:

| Agent | Icon | Specialty |
|---|---|---|
| **Research Agent** | 🔬 | Research, fact-finding, summarization, multi-source synthesis |
| **Coding Agent** | 💻 | Code writing, debugging, refactoring, code review |
| **Writing Agent** | ✍️ | Prose, emails, essays, copywriting, creative content |
| **Vision Agent** | 👁️ | Diagrams, charts, SVG/Mermaid generation, visual design feedback |
| **Reasoning Agent** | 🧠 | Math, logic, multi-step analysis, decision matrices |
| **Default Assistant** | ⭐ | Fallback for general conversation |

**Manual override:** prefix your message with `@research`, `@coding`,
`@writing`, `@vision`, or `@reasoning` to force a specific agent.

### 🧠 Long-Term Memory

KingerAi remembers facts about you across all chats:

- **Auto-extraction:** Detects patterns like "my name is X", "I work at Y",
  "I prefer Z" and saves them automatically
- **Manual entry:** Add facts via the Memory tab in the workspace panel
- **Context injection:** Top memories are injected into the AI's system
  prompt on every request
- **Usage tracking:** Tracks how often each memory is used

### 📦 Artifacts Panel

When the AI generates a complete standalone artifact (HTML page, SVG
diagram, Python script), it appears in the **Artifacts tab** of the
workspace panel — not as raw text in the chat bubble.

**Supported artifact types:**

| Type | Live Preview | Use Case |
|---|---|---|
| `html` | ✅ Iframe render | Landing pages, demos, widgets |
| `svg` | ✅ Image render | Diagrams, logos, illustrations |
| `mermaid` | Source view | Flowcharts, sequence diagrams |
| `python` | Source view | Standalone scripts |
| `javascript` | Source view | Standalone JS |
| `markdown` | Source view | Essays, reports, documents |

Each artifact card has **Copy**, **Download**, and **Open in new tab** actions.

### 💻 Code Interpreter

Run Python code in a safe sandbox directly from the workspace panel:

- **Resource limits:** 10s CPU time, 256MB RAM (configurable)
- **Whitelisted modules:** `math`, `statistics`, `random`, `datetime`,
  `json`, `re`, `collections`, `itertools`, `functools`, `decimal`,
  `fractions`, `hashlib`, `base64`, `uuid`, `csv`, `io`, `string`,
  `textwrap` (and `numpy`/`pandas` if installed)
- **Disabled builtins:** `open()`, `exec()`, `eval()` for safety
- **Output truncation:** Max 10,000 chars to prevent memory exhaustion

### 🎤 Voice Mode

Browser-native voice interaction — no extra dependencies:

- **Speech-to-Text** (Chrome/Edge): dictate your message instead of typing
- **Text-to-Speech** (all major browsers): have the AI read its replies aloud
- **Toggle:** click the 🎤 microphone icon in the header

### 📊 Admin Dashboard

Access real-time analytics at `/api/admin/stats`:

- Total counts: chats, messages, attachments, artifacts, memories, agent runs
- Activity timeline: messages per day (last 7 days)
- Per-agent breakdown: invocation count, avg duration, token usage
- Service health: database, AI provider, feature flags

**Authentication:** `Authorization: Bearer YOUR_ADMIN_TOKEN` header.

### 🎨 Modern UI

- **3-column workspace layout** (Chats | Conversation | Workspace)
- **Glassmorphism design** with animated gradient backgrounds
- **Light / Dark theme** toggle (persisted in localStorage)
- **Fully responsive:** desktop, tablet, mobile
- **Keyboard shortcuts:**
  - `Ctrl/Cmd + B` → toggle chats sidebar
  - `Ctrl/Cmd + J` → toggle workspace panel
  - `Ctrl/Cmd + K` → new chat
  - `Enter` → send message
  - `Shift + Enter` → newline

---

## 📦 Installation

### Requirements

- **OS:** Debian 11+, Ubuntu 20.04+, Linux Mint 20+, Pop!_OS 20.04+,
  or any Debian-based distro with glibc 2.31+
- **Architecture:** amd64 (x86_64)
- **RAM:** 512 MB minimum, 1 GB recommended
- **Disk:** 250 MB free space
- **Browser:** Chrome 90+, Firefox 88+, Edge 90+, or Safari 14+
  (for voice mode: Chrome or Edge recommended)

### Install via dpkg

```bash
# Download the .deb file
# (place kingerai_4.0.0_amd64.deb in your current directory)

# Install
sudo dpkg -i kingerai_4.0.0_amd64.deb

# If dependency errors appear, fix them with:
sudo apt-get install -f
```

### Install via apt (alternative)

```bash
sudo apt install ./kingerai_4.0.0_amd64.deb
```

### Verify installation

```bash
# Check the package is registered
dpkg -l | grep kingerai

# Check the binary exists
which kingerai
# → /usr/bin/kingerai

# Check the launcher script
cat /usr/bin/kingerai
```

### Uninstall

```bash
# Remove the package (keeps your data)
sudo dpkg -r kingerai

# Full purge (removes config + data)
sudo dpkg -P kingerai
```

---

## 🚀 Usage

### Starting the server

```bash
# As a regular user (recommended for testing)
kingerai
```

The server starts on `http://localhost:3333`. Open it in your browser.

**First run output:**

```
============================================================
  KingerAi  →  http://0.0.0.0:3333
  Environment    :  development
  Debug mode     :  True
  AI Provider    :  https://api.example.com/v1/chat/completions
  AI Model       :  DEFAULT_MODEL
============================================================
 * Running on http://127.0.0.1:3333
 * Running on http://<your-LAN-IP>:3333
```

### Running in the background

```bash
# Option 1: nohup
nohup kingerai > ~/.kingerai.log 2>&1 &
disown

# Option 2: systemd (recommended for production)
sudo tee /etc/systemd/system/kingerai.service > /dev/null <<'EOF'
[Unit]
Description=KingerAi Enterprise AI Workspace
After=network.target

[Service]
Type=simple
User=YOUR_USERNAME
ExecStart=/usr/bin/kingerai
Restart=on-failure
RestartSec=5
Environment=PYTHONUNBUFFERED=1

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable --now kingerai
sudo systemctl status kingerai
```

### Running with gunicorn (production)

```bash
# Install gunicorn (if not already in the bundle)
# The .deb already bundles it, so:
<internal path> \
  -b 0.0.0.0:3333 \
  -w 4 \
  --timeout 120 \
  run:app
```

### Accessing the UI

Open `http://localhost:3333` (or `http://YOUR_IP:3333` from another
device on your LAN) in a modern browser.

### Stopping the server

```bash
# If running in foreground: Ctrl+C

# If running in background:
pkill -f KingerAi

# If running as a systemd service:
sudo systemctl stop kingerai
```

---

## ⚙️ Configuration

**All configuration is hardcoded in the binary.** No `.env` file is needed.

The defaults are baked in:

| Setting | Default Value |
|---|---|
| Listen port | `3333` |
| Listen host | `0.0.0.0` (all interfaces) |
| AI API URL | `https://api.example.com/v1/chat/completions` |
| AI API Key | `YOUR_API_KEY` |
| AI Model | `DEFAULT_MODEL` |
| Temperature | `0.72` |
| Max tokens | `4098` |
| Database | SQLite at `<DATA_DIR>/database.db` |
| Upload limit | 20 MB per file, 5 files per message |
| Admin token | `YOUR_ADMIN_TOKEN` |
| Rate limit | 60 chat requests / minute |

### Changing the port

Override the port via the `PORT` environment variable:

```bash
PORT=8080 kingerai
```

### Changing the data directory

By default, the SQLite database and uploaded files live in
`~/.local/share/kingerai/`. Override with `KINGERAI_DATA_DIR`:

```bash
KINGERAI_DATA_DIR=/var/lib/kingerai kingerai
```

### Where data is stored

| Path | Purpose |
|---|---|
| `<DATA_DIR>/database.db` | SQLite database (chats, messages, memories, artifacts) |
| `<DATA_DIR>/uploads/` | Uploaded file attachments |
| `<DATA_DIR>/vector/` | (Reserved for future RAG/vector storage) |

---

## 📡 API Reference

All endpoints are prefixed with `/api`. The base URL is `http://localhost:3333`.

### Health

| Method | Path | Description |
|---|---|---|
| `GET` | `/health` | Service health check (no auth) |

### Chats

| Method | Path | Description |
|---|---|---|
| `GET` | `/api/chats` | List all chats |
| `POST` | `/api/chats` | Create a new chat |
| `GET` | `/api/chats/<id>` | Get a chat with all messages |
| `PATCH` | `/api/chats/<id>` | Rename a chat |
| `DELETE` | `/api/chats/<id>` | Delete a chat |

### Chat (streaming)

| Method | Path | Description |
|---|---|---|
| `POST` | `/api/chat/stream` | Send message + stream AI reply (SSE) |

**Request body:**

```json
{
  "chat_id": "abc123...",
  "content": "Hello, what can you do?",
  "file_ids": ["file-uuid-1", "file-uuid-2"],
  "force_agent": "coding"
}
```

**Response:** Server-Sent-Events stream with three event types:

```
data: {"agent": {"name": "coding", "display_name": "Coding Agent", "icon": "💻", "reason": "..."}}

data: {"delta": "Here is your code..."}

data: {"artifacts": [{"type": "html", "title": "...", "content": "..."}]}

data: [DONE]
```

### Files

| Method | Path | Description |
|---|---|---|
| `POST` | `/api/files` | Upload one or more files (multipart/form-data) |
| `GET` | `/api/uploads/<filename>` | Serve an uploaded file |
| `GET` | `/api/files/<attachment_id>` | Download an attachment linked to a message |

### Memory

| Method | Path | Description |
|---|---|---|
| `GET` | `/api/memory` | List all memory facts |
| `POST` | `/api/memory` | Add/update a memory fact |
| `DELETE` | `/api/memory/<id>` | Delete a specific memory |
| `DELETE` | `/api/memory` | Clear all memories |

### Artifacts

| Method | Path | Description |
|---|---|---|
| `GET` | `/api/chats/<chat_id>/artifacts` | List artifacts in a chat |
| `GET` | `/api/artifacts/<id>` | Get artifact details |
| `DELETE` | `/api/artifacts/<id>` | Delete an artifact |

### Agents

| Method | Path | Description |
|---|---|---|
| `GET` | `/api/agents` | List all available agents |
| `GET` | `/api/agents/runs` | Recent agent invocations |
| `GET` | `/api/agents/stats` | Per-agent aggregate stats |

### Code Interpreter

| Method | Path | Description |
|---|---|---|
| `POST` | `/api/code/run` | Execute Python code in sandbox |

**Request body:**

```json
{
  "code": "import math\nprint(math.factorial(10))",
  "timeout": 10
}
```

### Admin

| Method | Path | Description |
|---|---|---|
| `GET` | `/api/admin/stats` | Dashboard statistics |
| `GET` | `/api/admin/health` | Detailed service health |

**Auth header required:** `Authorization: Bearer YOUR_ADMIN_TOKEN`

### Import / Export

| Method | Path | Description |
|---|---|---|
| `GET` | `/api/export` | Export all chats as JSON (.kgpt format) |
| `POST` | `/api/import` | Import chats from a .kgpt file |

---

## 🛠 Troubleshooting

### The server won't start

**Symptom:** Running `kingerai` produces no output or exits immediately.

**Fix:**

```bash
# Check if port 3333 is already in use
sudo ss -tlnp | grep 3333

# If something is using it, either stop that process or use a different port:
PORT=8080 kingerai

# Check the binary is executable
ls -la /usr/share/kingerai/KingerAi
# Should show: -rwxr-xr-x ... KingerAi
```

### Browser can't connect

**Symptom:** `ERR_CONNECTION_REFUSED` when opening `http://localhost:3333`.

**Fix:**

```bash
# Verify the server is running
ps aux | grep KingerAi

# Check it's listening
curl http://127.0.0.1:3333/health
# Should return: {"service":"KingerAi","status":"ok","version":"4.0.0"}

# If accessing from another machine, check the firewall
sudo ufw allow 3333/tcp
```

### Permission denied writing to database

**Symptom:** `sqlite3.OperationalError: unable to open database file`

**Fix:** The launcher uses `$HOME/.local/share/kingerai/` as the working
directory. Make sure your user has write access:

```bash
mkdir -p ~/.local/share/kingerai
chmod 755 ~/.local/share/kingerai
```

Or override the data directory:

```bash
KINGERAI_DATA_DIR=/tmp/kingerai kingerai
```

### AI responses are empty or error messages

**Symptom:** Chat returns `⚠️ Agent error: Upstream returned HTTP 401`

**Fix:** The bundled API key may have been revoked. Unfortunately, since
all config is hardcoded, you'd need to rebuild from source with a new key
in `<config file>`:

```bash
# Get the source
unzip source-package.zip
cd kingergpt-pro

# Edit the config
sed -i 's|YOUR_API_KEY|YOUR_NEW_KEY|' <config file>

# Rebuild
<build script>
```

### Code interpreter returns "disabled"

**Symptom:** `{"error": "Code interpreter is disabled."}`

**Fix:** This is controlled by `CODE_INTERPRETER_ENABLED` in the config
(defaults to `True`). Since config is hardcoded, this should not happen
unless you modified the source.

### Voice mode not working

**Symptom:** Clicking the 🎤 icon shows "Voice mode not supported in this browser".

**Fix:** Voice mode requires the **Web Speech API**, which is only
available in:

- Chrome (desktop + Android)
- Microsoft Edge
- Safari 14.1+ (partial)

**Firefox does not support speech recognition.** Use Chrome or Edge for
voice mode.

### Database corruption recovery

If the SQLite database gets corrupted:

```bash
# Stop the server
pkill -f KingerAi

# Backup the corrupt file
mv <DATA_DIR>/database.db <DATA_DIR>/database.db.bak

# Restart — a fresh database will be created automatically
kingerai
```

### Getting logs

```bash
# If running in foreground: logs appear in the terminal
# If running with nohup: check the log file
tail -f ~/.kingerai.log

# If running as systemd:
sudo journalctl -u kingerai -f
```

---

# 🇮🇷 مستندات فارسی

## 🎯 معرفی

**KingerAi** یک پلتفرم هوش مصنوعی سازمانیِ خودمیزبان (self-hosted) است که با
Flask ساخته شده. این پکیج `.deb` شامل موارد زیر است:

- 🔧 Runtime پایتون (نیازی به نصب پایتون ندارید)
- 🎨 رابط کاربری مدرن (Glassmorphism + تم تاریک/روشن)
- 🔌 اتصال به API هوش مصنوعی (WormGPT)
- 🗄️ دیتابیس SQLite برای ذخیره‌سازی چت‌ها و حافظه

**همه‌چیز آماده‌ی اجراست — بدون نیاز به هرگونه تنظیمات یا فایل `.env`.**

### چرا "سازمانی"؟

| قابلیت | وضعیت | توضیح |
|---|---|---|
| 🤖 سیستم Multi-Agent | ✅ | ۵ Agent تخصصی + Orchestrator هوشمند |
| 🧠 حافظه بلندمدت | ✅ | ذخیره‌ی حقایق کاربر و تزریق به هر چت |
| 📦 پنل Artifacts | ✅ | پیش‌نمایش زنده HTML/SVG/کد (مثل Claude) |
| 💻 مفسر کد | ✅ | اجرای امن پایتون در sandbox |
| 🎤 حالت صوتی | ✅ | تبدیل صوت به متن و برعکس (بدون وابستگی خارجی) |
| 📊 داشبورد مدیریتی | ✅ | آمار، مصرف، سلامت سرویس |
| 🔒 امنیت | ✅ | CORS قابل تنظیم، JWT-ready، توکن ادمین |

---

## ✨ امکانات

### 🤖 سیستم Multi-Agent

پنج Agent تخصصی + یک Orchestrator که خودش تشخیص می‌دهد هر پیام باید به کدام
Agent برود:

| Agent | آیکون | تخصص |
|---|---|---|
| **Research Agent** | 🔬 | تحقیق، جمع‌آوری اطلاعات، خلاصه‌سازی |
| **Coding Agent** | 💻 | نوشتن کد، دیباگ، refactor، code review |
| **Writing Agent** | ✍️ | متن، ایمیل، مقاله، کپی‌رایتینگ |
| **Vision Agent** | 👁️ | دیاگرام، چارت، تولید SVG/Mermaid |
| **Reasoning Agent** | 🧠 | ریاضی، منطق، تحلیل چندمرحله‌ای |
| **Default Assistant** | ⭐ | گفتگوی عمومی |

**انتخاب دستی:** قبل از پیام، `@research`، `@coding`، `@writing`، `@vision`
یا `@reasoning` بنویسید.

### 🧠 حافظه بلندمدت

KingerAi حقایق درباره‌ی شما را در همه‌ی چت‌ها به یاد می‌آورد:

- **استخراج خودکار:** الگوهایی مثل "اسم من X است"، "در Y کار می‌کنم" را تشخیص می‌دهد
- **ورودی دستی:** از تب Memory در پنل Workspace حقایق اضافه کنید
- **تزریق خودکار:** مهم‌ترین خاطرات در هر درخواست به system prompt اضافه می‌شوند
- **ردیابی استفاده:** تعداد دفعات استفاده‌ی هر خاطره ثبت می‌شود

### 📦 پنل Artifacts

وقتی AI یک artifact کامل (صفحه‌ی HTML، دیاگرام SVG، اسکریپت پایتون) تولید می‌کند،
به‌جای نمایش در چت، در تب **Artifacts** پنل Workspace نمایش داده می‌شود.

**انواع پشتیبانی‌شده:**

| نوع | پیش‌نمایش زنده | کاربرد |
|---|---|---|
| `html` | ✅ render در iframe | صفحه‌های فرود، دمو، ویجت |
| `svg` | ✅ نمایش تصویر | دیاگرام، لوگو، تصویرسازی |
| `mermaid` | نمایش سورس | فلوچارت، دیاگرام توالی |
| `python` | نمایش سورس | اسکریپت‌های مستقل |
| `markdown` | نمایش سورس | مقاله، گزارش، سند |

هر artifact شامل دکمه‌های **کپی**، **دانلود** و **باز کردن در تب جدید** است.

### 💻 مفسر کد

اجرای پایتون در sandbox امن مستقیماً از پنل Workspace:

- **محدودیت منابع:** ۱۰ ثانیه CPU، ۲۵۶ مگابایت RAM
- **ماژول‌های مجاز:** `math`, `statistics`, `random`, `datetime`, `json`,
  `re`, `collections`, `itertools`, `functools`, `decimal`, `fractions`,
  `hashlib`, `base64`, `uuid`, `csv`, `io`, `string`, `textwrap`
- **توابع غیرفعال:** `open()`, `exec()`, `eval()` برای امنیت
- **حداکثر خروجی:** ۱۰,۰۰۰ کاراکتر

### 🎤 حالت صوتی

تعامل صوتی مبتنی بر مرورگر — بدون وابستگی خارجی:

- **تبدیل صوت به متن** (Chrome/Edge): به‌جای تایپ، پیام را بگویید
- **تبدیل متن به صوت** (همه‌ی مرورگرهای اصلی): پاسخ AI را بشنوید
- **فعال‌سازی:** روی آیکون 🎤 در هدر کلیک کنید

### 📊 داشبورد مدیریتی

آمار بلادرنگ در `/api/admin/stats`:

- مجموع: چت‌ها، پیام‌ها، فایل‌ها، artifacts، خاطرات، اجراهای agent
- جدول زمانی فعالیت: پیام‌ها در ۷ روز اخیر
- تفکیک per-agent: تعداد اجرا، مدت زمان، مصرف توکن
- سلامت سرویس: دیتابیس، AI provider، flagهای قابلیت‌ها

**احراز هویت:** هدر `Authorization: Bearer YOUR_ADMIN_TOKEN`

### 🎨 رابط کاربری مدرن

- **چیدمان ۳ ستونه** (چت‌ها | گفتگو | Workspace)
- **طراحی Glassmorphism** با پس‌زمینه‌ی گرادیانی متحرک
- **تم تاریک/روشن** (ذخیره در localStorage)
- **کاملاً ریسپانسیو:** دسکتاپ، تبلت، موبایل
- **میانبرهای کیبورد:**
  - `Ctrl/Cmd + B` → باز/بسته کردن sidebar چت‌ها
  - `Ctrl/Cmd + J` → باز/بسته کردن پنل Workspace
  - `Ctrl/Cmd + K` → چت جدید
  - `Enter` → ارسال پیام
  - `Shift + Enter` → خط جدید

---

## 📦 نصب

### پیش‌نیازها

- **سیستم‌عامل:** Debian 11+، Ubuntu 20.04+، Linux Mint 20+، Pop!_OS 20.04+
  یا هر توزیع مبتنی بر Debian با glibc 2.31+
- **معماری:** amd64 (x86_64)
- **رم:** حداقل ۵۱۲ مگابایت، پیشنهادی ۱ گیگابایت
- **فضای دیسک:** ۲۵۰ مگابایت
- **مرورگر:** Chrome 90+، Firefox 88+، Edge 90+ یا Safari 14+
  (برای حالت صوتی: Chrome یا Edge توصیه می‌شود)

### نصب با dpkg

```bash
# دانلود فایل .deb
# (فایل kingerai_4.0.0_amd64.deb را در دایرکتوری فعلی قرار دهید)

# نصب
sudo dpkg -i kingerai_4.0.0_amd64.deb

# اگر خطای وابستگی ظاهر شد:
sudo apt-get install -f
```

### نصب با apt (جایگزین)

```bash
sudo apt install ./kingerai_4.0.0_amd64.deb
```

### تأیید نصب

```bash
# بررسی ثبت پکیج
dpkg -l | grep kingerai

# بررسی وجود باینری
which kingerai
# → /usr/bin/kingerai
```

### حذف

```bash
# حذف پکیج (داده‌ها نگه داشته می‌شوند)
sudo dpkg -r kingerai

# حذف کامل (شامل کانفیگ و داده‌ها)
sudo dpkg -P kingerai
```

---

## 🚀 استفاده

### اجرای سرور

```bash
# به‌عنوان کاربر عادی (برای تست)
kingerai
```

سرور روی `http://localhost:3333` اجرا می‌شود. آن را در مرورگر باز کنید.

**خروجی اولین اجرا:**

```
============================================================
  KingerAi  →  http://0.0.0.0:3333
  Environment    :  development
  Debug mode     :  True
  AI Provider    :  https://api.example.com/v1/chat/completions
  AI Model       :  DEFAULT_MODEL
============================================================
 * Running on http://127.0.0.1:3333
 * Running on http://<IP-LAN-شما>:3333
```

### اجرا در پس‌زمینه

```bash
# روش ۱: nohup
nohup kingerai > ~/.kingerai.log 2>&1 &
disown

# روش ۲: systemd (برای پروداکشن)
sudo tee /etc/systemd/system/kingerai.service > /dev/null <<'EOF'
[Unit]
Description=KingerAi Enterprise AI Workspace
After=network.target

[Service]
Type=simple
User=نام_کاربری_شما
ExecStart=/usr/bin/kingerai
Restart=on-failure
RestartSec=5
Environment=PYTHONUNBUFFERED=1

[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable --now kingerai
sudo systemctl status kingerai
```

### دسترسی به رابط کاربری

`http://localhost:3333` (یا `http://IP_شما:3333` از دستگاه دیگری در شبکه)
را در مرورگر باز کنید.

### توقف سرور

```bash
# اگر در پیش‌زمینه اجرا شده: Ctrl+C
# اگر در پس‌زمینه اجرا شده:
pkill -f KingerAi

# اگر با systemd اجرا شده:
sudo systemctl stop kingerai
```

---

## ⚙️ تنظیمات

**تمام تنظیمات در باینری hardcoded شده‌اند.** هیچ فایل `.env`‌ای نیاز نیست.

| تنظیم | مقدار پیش‌فرض |
|---|---|
| پورت | `3333` |
| هاست | `0.0.0.0` (همه‌ی اینترفیس‌ها) |
| آدرس API | `https://api.example.com/v1/chat/completions` |
| کلید API | `YOUR_API_KEY` |
| مدل AI | `DEFAULT_MODEL` |
| دمای sampling | `0.72` |
| حداکثر توکن | `4098` |
| دیتابیس | SQLite در `<DATA_DIR>/database.db` |
| محدودیت آپلود | ۲۰ مگابایت هر فایل، ۵ فایل هر پیام |
| توکن ادمین | `YOUR_ADMIN_TOKEN` |
| محدودیت نرخ | ۶۰ درخواست چت در دقیقه |

### تغییر پورت

با متغیر محیطی `PORT`:

```bash
PORT=8080 kingerai
```

### تغییر مسیر داده‌ها

به‌طور پیش‌فرض، دیتابیس SQLite و فایل‌های آپلودشده در
`~/.local/share/kingerai/` هستند. با `KINGERAI_DATA_DIR` تغییر دهید:

```bash
KINGERAI_DATA_DIR=/var/lib/kingerai kingerai
```

### محل ذخیره‌سازی داده‌ها

| مسیر | کاربرد |
|---|---|
| `<DATA_DIR>/database.db` | دیتابیس SQLite |
| `<DATA_DIR>/uploads/` | فایل‌های آپلودشده |
| `<DATA_DIR>/vector/` | (آینده: ذخیره‌سازی برداری RAG) |

---

## 🛠 رفع اشکال

### سرور اجرا نمی‌شود

**علامت:** اجرای `kingerai` خروجی ندارد یا بلافاصله خارج می‌شود.

**راه‌حل:**

```bash
# بررسی اشغال بودن پورت 3333
sudo ss -tlnp | grep 3333

# اگر چیزی روی آن اجرا است، یا آن را متوقف کنید یا پورت دیگری استفاده کنید:
PORT=8080 kingerai
```

### مرورگر متصل نمی‌شود

**علامت:** `ERR_CONNECTION_REFUSED` هنگام باز کردن `http://localhost:3333`.

**راه‌حل:**

```bash
# بررسی اجرای سرور
ps aux | grep KingerAi

# تست اتصال
curl http://127.0.0.1:3333/health
# باید برگرداند: {"service":"KingerAi","status":"ok","version":"4.0.0"}

# اگر از ماشین دیگری دسترسی دارید، فایروال را بررسی کنید:
sudo ufw allow 3333/tcp
```

### خطای Permission denied در دیتابیس

**علامت:** `sqlite3.OperationalError: unable to open database file`

**راه‌حل:**

```bash
mkdir -p ~/.local/share/kingerai
chmod 755 ~/.local/share/kingerai
```

یا مسیر داده را تغییر دهید:

```bash
KINGERAI_DATA_DIR=/tmp/kingerai kingerai
```

### پاسخ‌های AI خالی یا خطا

**علامت:** چت برمی‌گرداند `⚠️ Agent error: Upstream returned HTTP 401`

**راه‌حل:** کلید API باندل‌شده ممکن است باطل شده باشد. متأسفانه چون تنظیمات
hardcoded هستند، باید از سورس با کلید جدید rebuild کنید:

```bash
# دریافت سورس
unzip source-package.zip
cd KingerAi

# ویرایش کانفیگ
sed -i 's|YOUR_API_KEY|کلید_جدید_شما|' <config file>

# rebuild
<build script>
```

### حالت صوتی کار نمی‌کند

**علامت:** کلیک روی آیکون 🎤 پیام "Voice mode not supported in this browser" می‌دهد.

**راه‌حل:** حالت صوتی به **Web Speech API** نیاز دارد که فقط در موارد زیر موجود است:

- Chrome (دسکتاپ + اندروید)
- Microsoft Edge
- Safari 14.1+ (جزئی)

**Firefox از تشخیص صوت پشتیبانی نمی‌کند.** از Chrome یا Edge استفاده کنید.

### بازیابی دیتابیس خراب

اگر دیتابیس SQLite خراب شد:

```bash
# توقف سرور
pkill -f KingerAi

# بکاپ فایل خراب
mv <DATA_DIR>/database.db <DATA_DIR>/database.db.bak

# راه‌اندازی مجدد — دیتابیس جدید خودکار ساخته می‌شود
kingerai
```

### دریافت لاگ‌ها

```bash
# اگر در پیش‌زمینه اجرا شده: لاگ‌ها در ترمینال نمایش داده می‌شوند
# اگر با nohup: فایل لاگ را بررسی کنید
tail -f ~/.kingerai.log

# اگر با systemd:
sudo journalctl -u kingerai -f
```

---

## 📄 License | مجوز

Released for personal and educational use.

---

<div align="center">

**KingerAi v4.0.0** — Built with ❤️ on Flask + Python 3.12

</div>
