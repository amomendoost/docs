# راهنمای نصب و راه‌اندازی Browser-Use Web UI

## مقدمه

یک پلتفرم قدرتمند است که به شما امکان اجرای عامل‌های هوش مصنوعی در مرورگر را می‌دهد. این ابزار با استفاده از Gradio ساخته شده و از مدل‌های مختلف زبانی بزرگ (LLM) پشتیبانی می‌کند.

## ویژگی‌های کلیدی

- **رابط کاربری آسان**: ساخته شده با Gradio
- **پشتیبانی از مدل‌های مختلف**: Google، OpenAI، Azure، Anthropic، DeepSeek، Ollama و غیره
- **استفاده از مرورگر شخصی**: امکان استفاده از مرورگر خودتان
- **ضبط صفحه با کیفیت بالا**: مشاهده فعالیت‌های عامل هوش مصنوعی
- **جلسات پایدار**: نگهداری وضعیت مرورگر بین وظایف مختلف

## روش نصب اول: نصب محلی

### مرحله ۱: کلون کردن پروژه

```bash
git clone https://github.com/browser-use/web-ui.git
cd web-ui
```

### مرحله ۲: راه‌اندازی محیط پایتون

**با استفاده از uv (پیشنهادی):**

```bash
uv venv --python 3.11
```

**فعال‌سازی محیط مجازی:**

- **ویندوز (Command Prompt):**
```cmd
.venv\Scripts\activate
```

- **ویندوز (PowerShell):**
```powershell
.\.venv\Scripts\Activate.ps1
```

- **مک/لینوکس:**
```bash
source .venv/bin/activate
```

### مرحله ۳: نصب وابستگی‌ها

**نصب پکیج‌های پایتون:**
```bash
uv pip install -r requirements.txt
```

**نصب مرورگرها در playwright:**
```bash
playwright install --with-deps
```

یا برای نصب مرورگر خاص:
```bash
playwright install chromium --with-deps
```

### مرحله ۴: تنظیم محیط

**۱. کپی کردن فایل تنظیمات:**

- **ویندوز:**
```cmd
copy .env.example .env
```

- **مک/لینوکس:**
```bash
cp .env.example .env
```

**۲. تنظیم کلیدهای API:**

فایل `.env` را باز کنید و کلیدهای API خود را اضافه کنید.

### مرحله ۵: اجرای برنامه

**۱. اجرای WebUI:**
```bash
python webui.py --ip 127.0.0.1 --port 7788
```

**۲. دسترسی به WebUI:**
مرورگر خود را باز کنید و به آدرس `http://127.0.0.1:7788` بروید.

**۳. استفاده از مرورگر شخصی (اختیاری):**

در فایل `.env` تنظیمات زیر را اضافه کنید:

- **ویندوز:**
```
BROWSER_PATH="C:\Program Files\Google\Chrome\Application\chrome.exe"
BROWSER_USER_DATA="C:\Users\YourUsername\AppData\Local\Google\Chrome\User Data"
```

- **مک:**
```
BROWSER_PATH="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"
BROWSER_USER_DATA="/Users/YourUsername/Library/Application Support/Google/Chrome"
```

**نکات مهم:**
- همه پنجره‌های کروم را ببندید
- WebUI را در مرورگر دیگری (فایرفاکس یا Edge) باز کنید
- گزینه "Use Own Browser" را در تنظیمات فعال کنید

## روش نصب دوم: استفاده از Docker

### پیش‌نیازها

- Docker و Docker Compose نصب شده باشد

### مرحله ۱: کلون کردن پروژه

```bash
git clone https://github.com/browser-use/web-ui.git
cd web-ui
```

### مرحله ۲: تنظیم محیط

```bash
cp .env.example .env
```

فایل `.env` را ویرایش کنید و کلیدهای API خود را اضافه کنید.

### مرحله ۳: اجرای Docker

**برای سیستم‌های معمولی:**
```bash
docker compose up --build
```

**برای سیستم‌های ARM64 (مثل مک‌های Apple Silicon):**
```bash
TARGETPLATFORM=linux/arm64 docker compose up --build
```

### مرحله ۴: دسترسی به برنامه

- **Web-UI:** `http://localhost:7788`
- **VNC Viewer:** `http://localhost:6080/vnc.html`
  - رمز عبور پیش‌فرض VNC: "youvncpassword"
  - می‌توانید با تنظیم `VNC_PASSWORD` در فایل `.env` آن را تغییر دهید

## نکات مهم

1. **امنیت:** کلیدهای API خود را محرمانه نگه دارید
2. **سیستم عامل:** این راهنما برای ویندوز، مک و لینوکس کار می‌کند
3. **پشتیبانی:** در صورت بروز مشکل، به مستندات رسمی پروژه مراجعه کنید
4. **به‌روزرسانی:** برای آخرین ویژگی‌ها، مخزن GitHub را دنبال کنید

## لینک‌های مفید

- [مخزن GitHub](https://github.com/browser-use/web-ui)
- [مستندات رسمی](https://github.com/browser-use/web-ui/blob/main/README.md)
- [ویدیوهای آموزشی](https://github.com/browser-use/web-ui#changelog)

---

**نوشته شده برای کاربران فارسی‌زبان - امیدوارم این راهنما مفید باشد! 🚀** 
