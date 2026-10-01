# نشر MS VPS Panel على Railway

## الملفات المطلوبة

ارفع هذه الملفات إلى نفس مجلد المشروع أو ارفع ملف `ms-vps-railway.zip`:

- `main.py`
- `requirements.txt`
- `Procfile`
- `railway.toml`

## خطوات Railway

1. أنشئ مشروعًا جديدًا من GitHub أو ارفع الملفات إلى مستودع Git.
2. تأكد أن Railway يرى `requirements.txt` و`railway.toml` في جذر المشروع.
3. في **Variables** أضف:

```env
SECRET_KEY=ضع_قيمة_عشوائية_طويلة_ومختلفة
MASTER_USERNAME=WEMOHAMMED1#
MASTER_PASSWORD=WEMOHAMMED1#
ENABLE_TELEGRAM_BOT=0
MAX_UPLOAD_MB=100
COOKIE_SECURE=1
```

4. اضغط **Deploy** ثم راقب **Deploy Logs**.
5. بعد نجاح النشر افتح الرابط العام. Railway يمرر `PORT` تلقائيًا؛ لا تضع رقم Port ثابتًا.

## أمر التشغيل

```bash
gunicorn --bind 0.0.0.0:$PORT --workers 1 --threads 8 --timeout 120 --access-logfile - --error-logfile - main:app
```

## فحص الصحة

افتح `https://YOUR-DOMAIN.up.railway.app/health` ويجب أن تظهر:

```json
{"status":"ok","service":"ms-vps-panel"}
```

## ملاحظات مهمة

لا ترفع مجلد `panel_data` القديم إذا كان يحتوي على بيانات أو سجلات غير مطلوبة؛ التطبيق ينشئه تلقائيًا. استخدم **Volume** أو قاعدة بيانات خارجية إذا أردت الاحتفاظ بالبيانات بعد إعادة التشغيل، لأن التخزين المحلي في Railway قد يكون مؤقتًا.

كلمة المرور المطلوبة موجودة كقيمة افتراضية داخل `main.py` حسب طلبك، لكنها ظاهرة لمن يملك الملف. يفضل وضعها في Railway Variables وتغييرها لاحقًا.
