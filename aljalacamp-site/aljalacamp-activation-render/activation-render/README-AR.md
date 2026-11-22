# استضافة التفعيل الأول على Render

هذه حزمة خدمة Node فقط لمشروع aljalacamp-test. لا تحتوي كشف أسر، مفاتيح، أو ملفات Hosting. شغّلها على حساب Render تملكه كخدمة Web Service، باستخدام مستودع خاص لهذا المجلد.

## الإعداد على Render

- Runtime: Node
- Build Command: npm ci --omit=dev
- Start Command: npm start
- Health Check Path: /healthz
- Instance Type: Free للاختبار فقط
- Env: HOST=0.0.0.0
- Env: GOOGLE_APPLICATION_CREDENTIALS=/etc/secrets/firebase-admin.json
- Env: CAMP_RECOVERY_SECRET: قيمة ثابتة وعشوائية لا تقل عن 32 بايت. يمكن توليدها محليًا بأمر node -e "process.stdout.write(require('node:crypto').randomBytes(32).toString('hex'))".
- Secret File: firebase-admin.json. أضف اعتماد حساب الخدمة الخاص بمشروع aljalacamp-test في قسم Secret Files على Render. لا تضعه في المستودع أو Firebase Hosting.

بعد التشغيل، افتح https://<service>.onrender.com/healthz للتحقق من الجاهزية. اختبر على أسر وهمية فقط. أعطِ عنوان HTTPS للخدمة إلى من يتولى ربط Firebase Hosting. عند الربط، يُضاف العنوان إلى public/assets/camp-recovery-config.js في حزمة الموقع وتُنشر الاستضافة فقط.

اختبر عمليًا تفعيل حساب وهمي جديد، وإغلاق المحاولة بعد ثلاثة أخطاء، ومنع تغيير كلمة مرور حساب فعّال سابقًا. استضافة Render المجانية قد تتأخر عند أول فتح بعد السكون.
