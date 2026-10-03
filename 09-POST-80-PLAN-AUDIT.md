
> **تقريرتاريخيبعد#80:** العوائقهنا حسمتفي#81–#84؛ الحالةالحاليةوNEXT في 04، ومواصفةالعيبالجديد05 §9. لا يعاد تكليف الوحدات القديمة.

# Dueli — مراجعة الخطة بعد PR #80

## BASE وحدود الإثبات

Plan BASE: `9ed7aca24bbd2bed439bb09d8a953d092be37de6`.
Code BASE: `b23cfe2a9202136f47da08d55fecee74e259f979`، بعد دمج #80.
مراجعة وثائق وكود محددة، بلا تنفيذ features أو تعديل dueli-opus أو اختبارات تاريخية/اتصال إنتاج.
دمج PRs75–80 مثبت من GitHub. production deploy وتطبيق0033 والبريد الحي/SPF/DKIM/DMARC مصدرها تقرير القائد/المالك؛ لا ندّعي تحققًا مستقلاً من Cloudflare أو Gmail.

## A — PLAN AUDIT

- DONE: R1 المغلقة، #75 جلسة نتائج Explore، #76 continuation Guest مع قبول المالك، #77 إصلاح reset/normalization/error contract، #78 domain identity، #79 عودة مسار deploy، #80 Spam UX وforensic. DONE هنا لنطاق PR، لا كل مرحلة R2/R3.
- incident0033: code منشور قبل تطبيق schema؛ manual remote apply عالج العطل بحسب القائد، دون reset/seed/DROP. readiness الآلية ما زالت ناقصة.
- باقي J/L1/V/L2/A/M/P/F/D0/D1/D2/C1/C2/C3/R0/R4 حسب 04؛ H7 coefficients غير معتمدة. admin/bank/doc interfaces وقرارات النجوم لا تسقط من النطاق.
- obsolete: «Guest هو NEXT»، و«انتظار وصول Inbox قبل J»، وتعليمات LOCAL لإعادة #76/#77، وافتراض أن Home كله يستخدم session أو أن cap15 يحقق استمرارًا. أزيلت من الموجهات النشطة؛ أبقي سجل قرار العيبين في 08 تاريخياً.
- #80 UX فقط: register warnings machine-readable؛ لا guidance عند failed/unconfigured؛ resend generic لا يثبت send؛ forgot يحافظ على anti-enumeration. لا وصف ذلك كإصلاح deliverability، ولا نقل Spam إلى blocker جديد.
- لا تعديل 06/07 التاريخيين؛ 08 قرارات المالك أعلى من المقترحات القديمة، مع إضافة قرار Home والبريد الصريحين.

## B — INCIDENT REVIEW

### #79: NEEDS TARGETED REMEDIATION

الانتقال من action غير قابل للحل إلى Wrangler المثبت صحيح، وbranch من env مع quoting يعالج injection في command. production push-main وpreview conditions والأسرار لم تُستبدل؛ لا نطلب revert للنشر العامل. لكن لا يصح وصف سلامة المسار بالكامل SAFE دون التحفظات التالية:

1. **SEC-06 coverage regression مثبت بالكود:** [checker](https://github.com/Maelsh/dueli-opus/blob/b23cfe2a9202136f47da08d55fecee74e259f979/dev-tools/check-sec06-math-random.mjs) يشترط CallExpression بcallee PropertyAccessExpression مباشرة. `(Math.random)()` و`const r = Math.random; r()` لا يطابقان، رغم أنهما كانا يحتويان Math.random الذي يحظره grep السابق. `Math['random']()` أيضاً يفوته الفاحص، لكنه لم يكن كشفًا مضمونا في grep السابق. المسح أصبح .ts فقط بدل كل الملفات. [tests](https://github.com/Maelsh/dueli-opus/blob/b23cfe2a9202136f47da08d55fecee74e259f979/tests/dev-tools/sec06-checker.test.ts) تغطي direct/multiline/comments/strings ولا تغطي الصور المذكورة. هذا حكم قراءة AST، لا ادعاء تنفيذ suite. العلاج: استخدام references/access التنفيذي مع controls إضافية محددة، دون false positives نصية.
2. **preview binding risk:** [wrangler.jsonc](https://github.com/Maelsh/dueli-opus/blob/b23cfe2a9202136f47da08d55fecee74e259f979/wrangler.jsonc) فيه D1 الإنتاج top-level بلا env.preview. [deploy.yml](https://github.com/Maelsh/dueli-opus/blob/b23cfe2a9202136f47da08d55fecee74e259f979/.github/workflows/deploy.yml) صار يستخدم Wrangler configuration للنشر؛ Cloudflare تنبه إلى مطابقة الإعدادات وتعتبر الملف مصدر الحقيقة عند استخدامه. فصل branch لا يكفي لفصل DB. لا إثبات كتابة preview فعلية هنا؛ يلزم إثبات هوية/عزل الإعداد النشط قبل أول preview تالٍ.
3. **quality/deploy dependency ناقصة:** [quality gate](https://github.com/Maelsh/dueli-opus/blob/b23cfe2a9202136f47da08d55fecee74e259f979/.github/workflows/quality-gate.yml) workflow مستقل، وdeploy لا ينتظر نجاحه بنفس SHA. هذا قديم قبل #79 وليس عيبًا اخترعه #79؛ تربطهما وحدة إصدار محددة دون إعادة الأمن القديم أو تشغيل full suite ثانية.
4. لا دليل هنا على تسريب سر أو shell injection متبقٍ في quoted branch، ولا على خرق MVC/نسب المال أو code feature change في #79. لا نقل تحذيرات تاريخية في CI إلى أعمال هذه الوحدة.

### 0033: الحل الدائم

**read-only schema-readiness gate** قبل production deploy + release preparation منفصلة للمigrations المعتمدة، لا auto-apply عمياء. required-schema manifest يثبت الإصدار والملفات/بصماتها/قدرات schema؛ target DB مثبت؛ فحص migrations الفعلية والمخطط يفشل مغلقًا. 0033 مطلوب لهذا baseline.
أي apply يفحص **كل pending** أمام القائمة المعتمدة، لأن أمر D1 apply يطبق المتبقي. expand متوافق قبل code، serialize مع deploy، recheck قبل النشر. فشل قبل deploy يبقي النسخة القديمة؛ نجاح schema مع فشل deploy لا يتطلب down. rollback للكود المتوافق فقط، Time Travel استثنائي مفوض مع أثر فقد الكتابات. التفاصيل/DoD في05 §7.

**القاعدة المكسورة عملياً:** جاهزية المخطط الذي يعتمد عليه الإصدار لم تفرض قبل نشره. وجود migration في repo ونجاح local tests لا يكفيان. إصلاح gating مطلوب؛ ليس إعادة فتح Backend أو schema historical audit.

## C — RAILS PLAN

**الواقع:** [HomePage](https://github.com/Maelsh/dueli-opus/blob/b23cfe2a9202136f47da08d55fecee74e259f979/src/client/pages/HomePage.ts):
- Guest Suggested: sessions/cursor/score +15 أولاً واستمرار حتى النفاد. إنشاء الجلسة لا يمرر status؛ الفلتر يذهب للفallback فقط.
- Logged Suggested: RecommendationEngine batch15 واحدة، بلا continuation، request يتجاهل status.
- الأقسام والفروع: list limit15، لا fetch أفقي جديد؛ مسار CompetitionModel يعيد RANDOM. recorded mapping لا يضمن تسجيلًا صالحًا؛ upcoming Guest محجوب في Home.
- cross-rail dedup غير موجود؛ لا نجعله hard requirement يفرغ الأقسام، فالعضوية عبر الأسطح متداخلة بطبيعتها.

**الاختيار:** reuse لا إعادة تعميم. [ExploreSessionService](https://github.com/Maelsh/dueli-opus/blob/b23cfe2a9202136f47da08d55fecee74e259f979/src/lib/services/ExploreSessionService.ts) يتضمن بالفعل ResultSessionProvider seam من #76، ويملك snapshot/chunks/cursor/TTL/context/skip-fill. providers إضافية + per-rail client state؛ abstraction صغير بقدر الحاجة، لا engine موازٍ أو tables جديدة بلا ضرورة مثبتة.

**الوحدات:** R3-RAILS-1A providers/eligibility/context بعد RELEASE؛ R3-RAILS-1B near-end horizontal fetch بعد A، ويجوز PR واحد متوسط. D0 بالتوازي لتصميم H7؛ D1 يطبق ترتيب المنافسات/البحث/المشابهات المعتمد، D2 للمستخدمين. continuation المنجزة لا تعاد داخل D1.

**توضيح المالك بعد التقرير:** الأوزان مطلوبة لكل قسم وفرع، وليست Suggested وحده. A يمكن تجهيزه مستقلاً لكن random-only ليس نهائياً ولا continuation وحده قبول Home. D0 يبدأ مع RELEASE ويعرض الأرقام مبكراً، وD1 يطبقها على كل الصفوف بعد الاعتماد وجاهزية إشاراتها. freeze أثناء التمرير فقط؛ إعادة الدخول/refresh تعيد احتساب الترتيب. extraction كامل شرط؛ no cap15. التنويع وخفض تكرار المشاهد يدخلان D0، دون RANDOM لكل دفعة أو حذف ذيل النتائج.

**DoD:** stable snapshot؛ no RANDOM+OFFSET؛ near-end loading؛ كل مؤهل مستمر يظهر مرة داخل صفه حتى exhaustion؛ لا سقف15؛ filters/identity/language/surface معزولة؛ refresh/new arrivals؛ expiry/retry/stale response؛ hasMore true عند partial continuation؛ recorded playable/live/upcoming صحيحان؛ ar/en وRTL/LTR وmobile/desktop. T traversal + B DOM/network كافيان، لا Astra أو مشاهدة وسائط. 05 §8 المرجع الكامل.

## D — NEXT

**R-RELEASE-1 فقط**: معالجة التغطية التنفيذية وعزل binding وجاهزية schema تمنع تكرار حادث الإنتاج قبل نشر بقية features. بعدها R3-RAILS-1A/1B ثم J؛ لا Inbox انتظار ولا إعادة Guest/Auth.
لا OWNER DECISION جديدة لازمة الآن. H7 أرقامها ستعرض في D0. الكتابة الإنتاجية/إنشاء مورد/restore تحتاج التفويض المناسب عند التنفيذ؛ هذا PR تخطيط فقط.

## المراجع الرسمية للتصميم

- [Cloudflare Pages Wrangler configuration](https://developers.cloudflare.com/pages/functions/wrangler-configuration/): إعداد النشر مصدر الحقيقة، وproduction/preview overrides؛ مراجعة تطابق الإعداد عند الانتقال من dashboard.
- [Cloudflare D1 migrations](https://developers.cloudflare.com/d1/reference/migrations/): list/apply للمتبقي؛ لا تعامل apply كاختيار migration واحدة بالاسم.
- [D1 Time Travel](https://developers.cloudflare.com/d1/reference/time-travel/): استرجاع قاعدة إلى نقطة سابقة يختلف عن rollback للكود؛ لا ننفذه تلقائياً.

كل التعليمات الجديدة في01–05 و08 متسقة مع هذا التقرير؛ سجل التنفيذ في 04 يحدث بعد كل merge حقيقي.

التوضيح أعلاه يستبدل أي تفسير سابق لإبقاء category shuffle كترتيب نهائي؛ فصل البنية عن الأرقام لا يعني استثناء أقسام/فروع من الأوزان.
