> **مصدر الترتيب والحالة الوحيد:** [14-UNIFIED-EXECUTION-PATH.md](14-UNIFIED-EXECUTION-PATH.md). هذا الملف يحدد النطاق/العقود فقط؛ أرقام المهام وموضع التنفيذ والحالات القديمة فيه ليست تكليفًا نافذًا. أي تعديل نطاق أو إضافة أو تغيير أولوية يجب أن يحدّث المسار14 في PR الخطة نفسه، مع حفظ كل بند أزيح إلى ترتيب جديد.

## المزامنة الحاكمة — 2026-10-09

التكامل الجديد والتوثيق في[13-LIVE-CHUNKS-UNIFIED-GUIDE-PLAN.md](13-LIVE-CHUNKS-UNIFIED-GUIDE-PLAN.md)، وحالة04 هي المرجع. التوجيه التاريخي (ليس تكليفًا حاليًا) LIVE-INT-1 لاDIAGمكرر؛ PR103–106 مدموجة و106نشرهاSUCCESS. DB-01 يبقىOPENللقياس. الوحداتوالشواهدالتاريخيةأدناه محفوظة، لايعادreceiver/star/title/0039 منوصفقديمOPEN.

MEDIAانتقلتإلىLIVE/CHUNK/COMP بوحداتهافي13؛ قبولالإدارةالمخولباقٍ. UX-STATE توسعتإلىUX-I18N-1؛ كلالعيوبالأخرىMESSAGES/PROFILE/HOME والعداداتوالـa11yفيهذاالملفمحفوظة. cleanupالمأذونغيرمثبتالتنفيذ. نتائجالتقريرالأحدث تحدّثالشاهدولايفترضALREADYDONEلأيعيبجديد.

## 2026-10-08 — Owner screenshot findings and mandatory agent safeguards

- Authenticated competition page `/competition/2201?lang=ar`: top navigation Help icon duplicates Help in authenticated account menu; show top-nav Help **only to guests** while preserving guest discoverability, keyboard/aria, RTL/LTR and 390px layout. Scope to R4-UX-STATE-1 / VIS-02, no blanket removal.
- Same Arabic completed competition shows literal English `Reminder On`: i18n leak and incorrect completed lifecycle action. Scope to R4-UX-STATE-1 / U-01 and I-01: all visible states/labels translated via ar/en dictionaries and t()/translations, completed reminder hidden/disabled; verify ar/en and desktop/mobile. Screenshot alone does not establish VOD backend failure; check player processing/unavailable fallback in MEDIA/ADMIN.
- Every LOCAL/REMOTE prompt for UI work must explicitly require reading `AGENTS.md` and relevant binding docs (`docs/01-ARCHITECTURE-RULES.md`, `docs/11-DEFINITION-OF-DONE.md`, `docs/13-TEST-STRATEGY.md`, `docs/18-REPOSITORY-CHANGE-POLICY.md`), plus PLAN 08/10/12. Acceptance gates: MVC/OOP, SQL Models only, i18n ar/en, RTL/LTR, accessibility/aria, dark/mobile; tests on changed paths. No blanket re-audit of closed phases.
- Chat report compact: STATUS, PR/FULL HEAD, 3–5 evidence findings, BLOCKERS, التوجيه التاريخي (ليس تكليفًا حاليًا); full evidence in repository. Repeated long reports are not requested.

## 2026-10-08 — Verified execution update (supersedes historical snapshot in §1)

- CODE MAIN: `5a74310667bfed286cc1f1ba0dfa450be1bb041b`; PR#103 title fix MERGED/DEPLOYED; PR#104 R4-DB-OPT-1 MERGED with owner-authorized production migration 0039 applied and six indexes reported verified. No automatic migration in workflow.
- PR#104 production Deploy #37771438709 failed despite Quality Gate success: `deploy.yml` index collector restricted snapshot to `required_schema.tables`, omitting six indexes on other tables. This repeated #458's incomplete collector pattern. PR#105 changed snapshot to all `sqlite_master` indexes; independent APPROVE, MERGED, post-merge Quality Gate #37774306486 SUCCESS and Deploy #37774306356 SUCCESS.
- **DB-01 remains OPEN** pending measured production D1 rowsRead/rowsWritten/executions before/after; schema readiness and successful deploy are not proof of quota headroom. No paid upgrade or DB migration approved.
- **التوجيه التاريخي (ليس تكليفًا حاليًا)** R4-EVENTS-NOTIFY-1, LOCAL tasked, no reported PR yet. Owner-approved one-time cleanup cutoff `2026-10-08T03:31:39Z` is still NOT EXECUTED; leader must review specific guarded SQL/runbook before production write. Permanent closed=read policy unapproved. Existing N-03 conflict requires targeted role/state/HEAD evidence.
- **Leadership release regression rule**: prior incidents #458 and #37771438709 MUST be consulted for changes to manifest, schema collector or D1 migration; prove snapshot covers required indexes on tables not present in `required_schema.tables`, test missing-index fail-closed, and verify actual post-merge production workflow. PR preview success is not equivalent to production deploy success. Record run IDs and exact SHAs in 04.

# Dueli — R4 Recovery / D1 Consumption / Leadership Handoff

**خطة الاستعادة الهندسية — 2026-10-08. القرارات البشرية المفتوحة أدناه ليست معتمدة.** هذا الملف يضيف إصلاحات لعيوب استخدام وتشغيل جديدة محددة. لا يعيد فتح Backend/Core/Live/TURN/Finance/Ads/R1 أو الوحدات الصحيحة المغلقة. 08 مرجع قرار المالك، 11 مرجع H7 الثابتة، 04 الحالة، 10 بروتوكول الدمج والإصدار. لا تفويض فوترة أو نقل قاعدة أو كتابة إنتاجية من اعتماد هذا الملف.

## 1. الحالة ومصدر الدليل

- code main المثبت من GitHub: `2e3d3681093a591e917dd1c57dc9cc249c307458`، PR#102 merged. R2 ووحدات R3 مغلقة برمجيًا وفق سجل04؛ C3 وثيقة تصميم فقط ولا تفوض حذف synthetic.
- PR#103 OPEN وقت القراءة؛ HEAD `d020d8c4febdf778fabfe592dd11f40ed48add4a`، BASE هو main أعلاه؛ إصلاح title escaping موجود فلا يعاد تكليف تنفيذه. لا DEPLOYED قبل بروتوكول10.
- تقريران بصريان خارجيان، ملخصهما موجه القائد الذي نقله المالك في2026-10-08: NOT READY مع عيوب محددة. هذه المراجعة لم تدخل الإنتاج ولم تتصل بCloudflare. عند المراجعة الأولى كانت التقارير الأصلية غير متاحة؛ أصبح تقرير PDF الأصلي الأول متاحًا وقُرئ كاملًا في متابعة §10؛ لا نخترع تصنيف BOTH/ONE لكل بند. القائد يربط كل بند بالشاهد الأصلي المتاح دون إعادة الاختبار لمجرد تصنيفه.
- مصدر D1: تقرير مساعدCloudflare وجدولTop10 نقلهما المالك وصورة اللوحة. قال المساعد إنه قرأ GraphQL Analytics؛ لا وصول مستقل للمخطط إلى القياسات الأصلية. الإجماليات المنقولة:6,612,120 rowsRead،41,554 executions،212 query patterns،10,652 rowsWritten،503,544 rowsReturned في72ساعة. فترة التقرير الأول2026-10-05T00:27:48Z→2026-10-08T00:27:48Z. dueli-db UUID `f877f573-e31f-452a-8991-8e5035539d56` وفق التقرير؛ القاعدة الأخرى بلا مساهمة وفقه.
- تناقض غير محسوم: التقرير الأول ينسب48,828 executions إلى3ساعات رغم إجمالي41,554؛ لاحقًا تغيرت القراءات الساعية ومجموع يوم7أكتوبر إلى6,098,153. لا نستخدم هذه الأعداد لتحديد عدد الزوار أو يوم استنفاد بدقة. صفوفGraphQL أقل من10000 لا تثبت وحدها غياب sampling أو اكتمال attribution.
- وصف50params في الصفين1/2 غير موثوق: returned/execution نحو64/63، لا ينسجم مع GROUP BY50معرفًا فقط. النص مبتور؛ الكود على SHA المرجعي يستخدم دفعات حتى80. النص الكامل من الكود/المصدر يحسم المطابقة.

## 2. أدلة الاستهلاك الموجهة

| # | نمط الاستعلام المنقول | executions | rowsRead | avg read | rowsReturned |
|---|---|---:|---:|---:|---:|
|1|opponent_id COUNT GROUP BY IN|963|1611844|1674|61898|
|2|creator_id COUNT GROUP BY IN|936|1595104|1704|58963|
|3|Competition details joins|637|335591|527|57330|
|4|participation category COUNT creator OR opponent + started predicate|150|232170|1548|198|
|5|H7 competition signal columns/joins|694|222907|321|55520|
|6|creator COUNT IN2 + started_at IS NOT NULL|136|209730|1542|142|
|7|creator COUNT IN9 + started_at IS NOT NULL|122|189100|1550|732|
|8|eligible competition IDs joins|202|179883|891|27307|
|9|eligible IDs variant|234|154037|658|21590|
|10|creator/opponent/category/subcategory signals|81|124821|1541|0|

كلها rowsWritten=0 في الجدول. المتوسطات مقربة؛ إجمالي التنفيذات والأعداد المقاسة لا تستخرج بضرب المتوسط المقرب.
1+2=3,206,948 reads=48.5% من الإجمالي المنقول؛1+2+4+6+7=3,837,948=58.0%؛Top10=4,855,187=73.4%.
هذا دليل أولوية، لا إثبات full scan أو افتقاد فهرس. إرجاع0نتائج قد يكون تحققًا صحيحًا من أهلية/تخصص، وليس إذن حذف الاستعلام.

مسارات مؤيدة بالكود المرجعي:
- H7SignalsModel.loadProfiles: SUMratings وثلاث عمليات تحميل لكل دفعة منها creator/opponent actual-participation counts؛ loadViewerContext يجمع الأقسام في مسار4.
- UserSignalsModel يحمل تخصص creator/opponent؛ مرشح مطابقة10 لا نسبة نهائية من نص مبتور.
- HomeRailProviders يبني مجموعة IDs المؤهلة كاملة ثم يحمل signals/context/profiles ويرتب عندT0 قبل أول15بطاقة.
- HomePage ينشئ rails السياق كلها وينتظر Promise.all قبل الرسم؛ تغير generation يمنع الرسم القديم لكنه لا يثبت منع العمل القديم على الخادم.
- ExploreSessionService يستدعي deleteExpired عند البناء ويكتب chunks؛ expiry index موجود في0033.
- migration0006 تتضمن(status,started_at) ومؤشرات status/category/language/country. فهرس started_at مستقلاً ليس حلًا مفروضًا؛ تحقق من الفهارس الفعلية والخطة أولًا.

## 3. وحدات التنفيذ ومعايير القبول

| الوحدة | النطاق ومعيار الإغلاق | التحقق والاعتماد |
|---|---|---|
| R4-DB-DIAG-1 — التوجيه التاريخي (ليس تكليفًا حاليًا) | ربط أعلى الاستعلامات بالكود الكامل؛ فحص الفهارس وEXPLAIN محليًا؛ تتبع تكرار تحميل profile/context وبناء جلسات Home؛ تسليم baseline وخطة تحسين صغيرة | تحليل وT؛ قراءة الإنتاج فقط بتفويض محدد؛ لا Astra |
| R4-DB-OPT-1 | تحسين الفهارس أو الاستعلامات أو التكرار المثبت؛ مقارنة قبل/بعد بأحجام محددة؛ حفظ التقييم والمشاركة الفعلية وH7 والحجب والفلاتر والثبات والنفاد؛ binds<=100 وقياس الكتابة | بعد DIAG؛ T+B؛ migration إنتاجية بتفويض منفصل |
| R4-EVENTS-NOTIFY-1 | حفظ receiver في CSP delegate؛ فحص handleNotificationClick وtoggleStar والـhandlers المعتمدة المتأثرة بالنمط نفسه موضعيًا؛ النقر واللوحة؛ تحديث القراءة والعداد؛ رابط طلب الانضمام يصل إلى القرار؛ منع تكرار toast عند replay | T+B؛ allowlist وCSP محفوظان؛ حسم N-03؛ تنظيف الإشعارات القديمة مرة واحدة معتمد في08/§10؛ السياسة الدائمة منفصلة |
| R4-MESSAGES-1 | إظهار محادثة الهاتف والعودة للقائمة؛ Compose؛ فتح المحادثة الموجودة من profile وعرض الاسم؛ تحديث المعاينات والعدادات | T+B ar/en mobile/desktop؛ الملكية والحجب محفوظان |
| R4-PROFILE-SAVE-1 | تتبع PUT settings الذي يعيد200 دون حفظ display_name/bio؛ إصلاح المسار المثبت؛ GET وrefresh يثبتان الحفظ | T+B محدد؛ لا إعادة Auth/settings كاملة |
| R4-HOME-UX-1 | رسم كل rail عند جاهزيته مع loading/retry؛ الصف البطيء لا يحجب السريع؛ منع stale paint والطلبات المتكررة | ينسق مع DB-OPT على HomePage؛ لا تكليفين متعارضين |
| R4-UX-STATE-1 | النصوص التالفة وNaN والترجمة وreminder422 وhelp وadmin visibility والعدادات/popovers والتفاصيل المثبتة | T+B موضعي؛ جمع المترابط وتقسيم غير المترابط عند الحاجة |
| R4-MEDIA-ADMIN-ACCEPT-1 | تتبع VOD processing لعينة موجودة؛ فصل demo قديم عن عطل فعلي؛ قبول رد الإدارة بحساب صالح ومصرح | T/B أولًا؛ S/H للوسائط الحقيقية أو الوصول؛ BLOCKED ليس PASS |
| R4-ACCEPT-REM-1 | قبول الرحلات التي ثبت فشلها والمواضع المعدلة؛ استقرار الخدمة ضمن ميزانية مقاسة؛ تقرير الجاهزية | بعد الخدمة والإصلاحات؛ لا إعادة البوابات التاريخية |

الوحدات ليست عدد PRs مفروضًا. PR103 مسار قائم مستقل: مراجعة REMOTE رسمية ثم بروتوكول10، دون إعادة إصلاحه. يمكن DIAG بالتوازي معه، والعمل محليًا على الواجهات أثناء انتظار analytics. القبول الإنتاجي المعتمد علىDB ينتظر استعادتها.

## 4. سجل العيوب

مصدر العيوب ملخص القائد لتقريري المتصفح. تصنيف BOTH/ONE يحتاج الشاهد الأصلي، ولا يعاد الاختبار لمجرد التصنيف.

| ID | الأولوية | العيب والدليل المتاح | الوحدة |
|---|---|---|---|
| DB-01 | BLOCKER | رسالة تجاوز daily reads نقلها المالك؛ ليست migration أو bind-limit | DIAG/OPT |
| N-01 | BLOCKER | dropdown يفشل بنقر الإشعار؛ فقد receiver مؤيد بمسار resolveFn/runHandler | EVENTS-NOTIFY |
| M-01 | BLOCKER | حاوية محادثة الهاتف hidden md:flex لا تظهر وفق التقرير | MESSAGES |
| P-01 | HIGH | settings200 دون حفظ الاسم/bio؛ السبب يحتاج تتبع | PROFILE-SAVE |
| N-02 | HIGH | فتح View لا يحدث is_read؛ MarkAll واليدوي يعملان | EVENTS-NOTIFY |
| N-03 | DISPUTED / TARGETED CHECK | الملخص السابق يقول إن رابط طلب الانضمام لا يصل إلى القرار؛ PDF §6 يقول إنه يصل لقرار قابل للاستخدام. لا يغلق ولا يصلح افتراضيًا قبل حسم العينة والدور والحالة على HEAD الحالي | EVENTS-NOTIFY |
| M-02 | HIGH | فتح الرسائل من profile يعرض #id ولا يسترجع المحادثة كما ينبغي | MESSAGES |
| H-01 | HIGH | تأخر Home15–30ثانية وفق المتصفح؛ Promise.all مؤيد بالكود | HOME-UX/OPT |
| S-01 | HIGH | title غير مهرب؛ PR103 مفتوحة تعالج المسار المركزي | PR103 القائمة |
| N-04 | MEDIUM | toasts قديمة وclosed unread ونص قبول بعنوان طلب جديد وعربي داخلEN | EVENTS-NOTIFY/UX-STATE |
| I-01 | MEDIUM | InvitePanel: mojibake وNaN% ومفاتيح ترجمة ناقصة | UX-STATE |
| U-01 | MEDIUM | RemindMe422 بلا تفسير؛ تأخر القبول10–12ثانية؛ عداد التعليقات لا يتحدث | UX-STATE |
| U-02 | MEDIUM | AdminPanel للعادي ثم403؛ help رابط [object Object] | UX-STATE |
| U-03 | MEDIUM | بحث المدعوين بطيء وpopovers مكررة وتأخر الانتقال بعد create | UX-STATE |
| M-03 | GAP | Compose غير موجود ومعاينات/عدادات الرسائل متأخرة | MESSAGES |
| VOD-01 | NEEDS TARGETED VERIFICATION | processing في عينات؛ لم يحسم demo قديم أم عطل | MEDIA-ADMIN-ACCEPT |
| ADM-01 | BLOCKED ACCESS | لا حساب إداري صالح للتجربة؛ لا PASS ولا FAIL | MEDIA-ADMIN-ACCEPT |
| VIS-01 | TARGETED | responsive/a11y/dark mode؛ يلزم موضع وشاهد لكل بند | الرحلة المتأثرة ثم ACCEPT |
| DATA-01 | DATA / TARGETED | بيانات demo قديمة أو غير مناسبة وفق ملخص القائد؛ توثيق العينات وأثرها على الاختبار، دون حذف أو تعديل يخالف KEEP NOW | UX-STATE / MEDIA-ADMIN-ACCEPT |
| AUTH-OBS-01 | OBSERVATION / NOT AUTOMATIC DEFECT | الدخول يعتمد البريد وفق التقرير؛ فشل admin/admin يثبت غياب وصول صالح فقط. تحقق من عقد معرف الدخول قبل وصفه عيبًا؛ لا إضافة username login أو إنشاء حساب إنتاجي تلقائيًا | MEDIA-ADMIN-ACCEPT / حساب مصرح |

يضيف القائد روابط الشواهد الأصلية عند توفرها. لا حذف demo أو التاريخ لإخفاء العيوب، ولا فتح TURN/Finance/Ads كاملة من عينة وسائط أو واجهة.

## 5. التحقيق والتحسين دون تغيير المنتج

1. لا مزيد من جولات المحادثة مع مساعد Cloudflare المغلق. الجدول دليل أولوية كافٍ للفحص المحلي؛ raw analytics إن توفر بسهولة، وليس شرطًا لتعطيل العمل على الاستعلامات المحددة.
2. فحص indices الفعلية عند توفر وصول مصرح؛ EXPLAIN QUERY PLAN للنص الكامل على local/preview مماثل. لا benchmark ثقيل أو تصدير production وهي مستنفدة. فهرس فيrepo لا يثبت وجوده الفعلي دون شاهد.
3. تجربة فهرس مناسب لـcreator/opponent وشرط المشاركة الفعلية حسب الخطة والحجم. لا إنشاء ثلاثة فهارس عمياء، ولا وعد بأن COUNT لخمسين مستخدمًا سيقرأ أرقامًا أحادية.
4. قياس تكرار loadProfiles/loadViewerContext بين rails. مشاركة إشارات خام أو سياق ضمن بناء منسق أو cache محكوم إذا برره القياس. لا KV إلزامي، ولا cache شخصي مشترك يكشف بيانات؛ الهوية والسياق والسياسة والصلاحيات وexpiry محفوظة.
5. قياس إنشاء snapshot كاملة واستمرار الصفحات كل على حدة. لا سقف15/100 ولا RANDOM+OFFSET ولا اختلاط فلاتر. إعادة الزيارة الصريحة تظل جلسة جديدة وفق السياسة.
6. aggregates مسبقة حل لاحق إن ثبتت الحاجة؛ تحتاج invalidation عند تعديل الأصوات/النهاية/المشاركة. صيغة Profile وH7 لا تتغير؛ صفوف النتائج الفارغة لا تحذف وظيفتها دون فهم.
7. ميزانية الاستخدام = طلبات الواجهات × القراءات لكل طلب + polling/background/QA. زمن1ms لا يثبت انخفاض استهلاك الصفوف. يقاس rowsWritten أيضًا عند تغيير session/cache/indices.
8. اختبار إنتاجي صغير بعد استعادة الخدمة ضمن ميزانية مصرح بها؛ لا reload متكرر بلا غرض. لا إعادة اختبارات تاريخية.
9. تجميد ترتيب الكتالوج كاملًا لكل rail عندT0 تكلفة تتوسع مع الحجم؛ التحسين يحفظ العقد. إذا لم تكف الفهارس وتقليل التكرار، يعرض تصميم بناء/precomputation مناسب قبل تغيير معنى T0/exhaustion، ولا يسقط المؤهلين بصمت.

## 6. القرارات المفتوحة والتفويض

- **DB-HOSTING OPEN:** Free/Paid/النقل لم يعتمد. توصية التخطيط: تحسين الاستعلامات، وعرض Paid على المالك عند حاجة استعادة الخدمة. لا فوترة أو نقل من اعتماد هذه الوثيقة. MySQL/MariaDB علىiFastNet يدرسان لاحقًا بمواصفات الباقة/TLS/الموارد/النسخ/latency وخطة انتقال تحفظ الكتابات. SQLite عبرAPI يضيف خدمة وصول، وليس نقل ملف يفتحه Worker بعيد.
- **NOTIFICATION-CLOSED POLICY PROPOSED (دائمة فقط):** حفظ التاريخ مع Closed/Expired/Declined وإخفاء الإجراء المنتهي. الإغلاق لا يعني القراءة، والقراءة لا تعني الإغلاق؛ unread للقراءة والطلبات القابلة للإجراء مستقلة. رابط مباشر لواجهة القرار يكفي بدل أزرار داخلdropdown. المقترح الدائم ليس قرار مالك مثبتًا. استثناء اختباري صريح: المالك اعتمد الآن تعليم الإشعارات القديمة مقروءة مرة واحدة وفق08 و§10؛ لا يعاد طلب هذا الإذن ولا يمتد تلقائيًا للإشعارات الجديدة.
- **ADMIN ACCESS OPEN:** حساب صالح مصرح به، تسلم بياناته خاصًا. لا admin/admin إنتاجي من هذه الوثيقة، ولا منح دور تلقائي لفشل اختبار الدخول.
- **REMOTE ACCESS:** الإذن بقراءة الفهارس/EXPLAIN لمساعدCloudflare لا يتحول إذن وصول عام للوكلاء. القائد يحدد أوامر القراءة والهوية عند الحاجة؛ migration إنتاجية تفوض منفصلة بعد إعدادrunbook قابل للمراجعة.
- H1–H9 وh7-v1 ثابتة؛ KEEP NOW ثابتة؛ فحوصSEC غير المانعة لا تتحول دينًا أو بوابات جديدة.

## 7. القبول والكلفة وتسليم القيادة

T للاستدعاء والحفظ وخطة الاستعلام والحسابات والملكية. B عبرPlaywright أو متصفح معتاد للنقر/الرسائل/الروابط/الفلاتر/العدادات/التمرير وar/en وmobile/desktop وRTL/LTR. S/Astra أو المالك فقط للصوت والصورة والجهاز الحقيقي أو حكم بصري حصري لا يحسمهT/B. H للوصول الإداري والبنك والفوترة والإطلاق.

R4 تغلق عندما لا يوجد blocker/High معلوم في الرحلات الأساسية، والخدمة ضمن ميزانية مقاسة، والرحلات الفاشلة مقبولة، والوصول الإداري مصرح وبيانات الإطلاق غير مؤقتة. R0 خارجية حالتها صريحة؛ لا ادعاء تشغيل دفع حقيقي قبل البنك/المزود ولا قرار إطلاق آلي.

تقدير من8أكتوبر مع إبقاءD1: متفائل3–5أيام، أرجح5–9، ومع عطلmedia أو بناءsnapshot بنيوي10–14. تقدير تخطيطي يحدث بعدDIAG، وليس موعد إطلاق مضمونًا ولا يشمل نقلDB أو الانتظار الخارجي.

يمكن نقل القيادة الآن دون انتظار إصلاح كل العيوب. يحفظ القائد04 وحالةPR103 وتكليفREMOTE النشط والشواهد والتفويضات، ويعطيCODE/PLAN SHA النهائيين ومرجع12 والتوجيه التاريخي (ليس تكليفًا حاليًا). لا تكليف إصلاح مكرر لـ103 ولا إعادةH7/R2/R3.

كلPR كود: WORKLOG.md وPLAN-STATUS.md بحالة صادقة، ثم REMOTE علىexactHEAD/currentbase، merge expected_head_sha، Quality علىactualmergeSHA، Deploy لنفسSHA، وفق10.

## 8. بطاقة LOCAL للخطوة الأولى

```text
DUELI — LOCAL — R4-DB-DIAG-1 — READ ONLY / NO CODE CHANGES
CODE: https://github.com/Maelsh/dueli-opus
PLAN: https://github.com/Maelsh/dueli-plan/tree/main/dueli-completion-plan
PLAN COMMIT: <merged plan SHA>; BASE: <current code main confirmed by lead>
اقرأ12 §§1–5 و04 و08 و10 و11؛ القائد يرفق النطاق والجدول عند تعذر الوصول.
استعلاما creator/opponent counts يمثلان48.5% من الجدول المنقول.
اربط النص الكامل بـH7SignalsModel وUserSignalsModel.
افحص indices وEXPLAIN علىlocal/preview، وتكرار profile/context وsession builds.
قِس بناء جميع المؤهلين واستمرار الدفعات منفصلين.
النص المبتور50params وfull scan ليسا حقيقتين مثبتتين.
سلم BASE والمسارات والـSQL والفهارس والخطة وbaseline وأصغر OPT مقترحة.
احفظ H7 والتقييم والمشاركة الفعلية والحجب والسياق وexhaustion.
لا كود أو PR شكلي، ولا production load/export/write/index/migration،
ولا billing أو نقل أو حذف synthetic. اذكر نقص الوصول دون طلب أسرار بالمحادثة.
```

## 9. مطابقة تغطية ملخص التحقيق — 2026-10-08

راجعت قائمة BLOCKERS/HIGH/MEDIUM/UX/DATA في موجه القائد المرفق بندًا ببند مقابل سجل§4. جميع الموانع والعيوب المسماة في هذا الملخص لها وحدة معالجة أو قبول/تصنيف محدد، بما فيها بياناتdemo وعقد معرف الدخول وtoggleStar. هذه تغطية للملخص المتاح، وليست ادعاء جرد كل صفحة في تقريري المتصفح الأصليين أو ضمان عدم ظهور عيب جديد. عند توفر التقريرين، يطابق القائد الشواهد والمواضع الإضافية بالسجل، دون إعادة اختبار بند ثبت أو إعادة فتح تاريخ مغلق.


## 10. التقرير الأصلي وقرار المالك — 2026-10-08

**المصدر:** Dueli_R4_Production_Forensic_Audit_Report.pdf، مؤرخ8أكتوبر، اختبار23:33UTC يوم7أكتوبر إلى نحو01:00UTC يوم8أكتوبر، production SHA `2e3d3681093a591e917dd1c57dc9cc249c307458`. قُرئ التقرير كاملًا بما فيه21 finding والشواهد المضمنة وخرائط الإشعارات وتقييمPR103. هذا شاهد تاريخي، لا اختبار مستقل على HEAD أحدث. التقرير الثاني ما زال متاحًا بالملخص فقط. أرقام الصفحات أدناه هي المطبوعة داخلPDF؛ لا حاجة لإرفاق كل الصور.

**قرار المالك:** تثبيت الإضافات وإبلاغ القائد، والتحقق من اختلاف إشعار طلب الانضمام، وعدم إغلاق مشكلة الاستهلاك بمجرد تعافيD1، وتعليم الإشعارات القديمة مقروءة مرة واحدة. الإضافات OPEN/PLANNED وليست DONE من دمج الوثائق.

### 10.1 مطابقة جميع بنود PDF

| مصدر PDF | سجل الخطة والإضافة المطلوبة | الوحدة |
|---|---|---|
| C-1 ص2 | DB-01؛ عودة الخدمة لا تثبت خفض الاستهلاك. أضف حالة تعطل واضحة وretry محدودًا/backoff؛ صمم تنبيه استخدام بحسب القدرات المتاحة دون افتراض alert جاهز أو تفويض فوترة | DIAG/OPT + HOME-UX/UX-STATE |
| C-2 ص3 | N-01؛ النقر وstar يفقدان receiver؛ لا يكفي استدعاء مباشر يتجاوز delegate | EVENTS-NOTIFY |
| H-1 ص4 | N-02؛ فتح View يحدث القراءة المحفوظة والعداد؛ اليدوي وMarkAll ضوابط إيجابية | EVENTS-NOTIFY |
| H-2 ص4 | P-01؛ endpoint يتجاهل display_name/bio وفق التقرير؛ نجاح الحفظ يجب أن يكون صادقًا | PROFILE-SAVE |
| H-3 ص5 | I-01؛ mojibake وNaN وpluralization في card وdrawer معًا | UX-STATE |
| H-4 ص6 | N-04؛ انتهاء الدعوة/الطلب لا يظهر في الإشعار؛ التنظيف الاختباري معتمد أدناه والسياسة الدائمة منفصلة | EVENTS-NOTIFY |
| M-1 ص7 و§6 | N-03 والتحقق أدناه؛ /my-requests لا يُكتشف إلا منHelp؛ أضف مدخلًا مرئيًا مناسبًا. رابط يصل للقرار يكفي؛ لا أزرار جديدة داخل الإشعار إلزامية | EVENTS-NOTIFY/UX-STATE |
| M-2 ص7 | M-02؛ ?user يفتح التاريخ الموجود ويعرض الاسم بدل#id | MESSAGES |
| M-3 ص8 | **M-04 جديد:** رسالة محفوظة لا تظهر حتىreload، وترتيب/تمرير خاطئ، وEnter لا يرسل. DoD: عرض الرسالة بعد نجاح موثوق؛ ترتيب زمني صحيح وأحدث رسالة مرئية؛ Enter للإرسال وShift+Enter لسطر مع حفظIME عند استخدام composer متعدد الأسطر | MESSAGES |
| M-4 ص8 | N-02/M-03؛ تحديثbadge بعد الفعل من حالة موثوقة دون انتظارpoll/reload؛ حفظSSE/poll دون زيادة غير لازمة | EVENTS-NOTIFY/MESSAGES |
| M-5 ص9 | I-01؛ notification.no_notifications يتسرب أثناءloading؛ افصل loading عنempty وترجمar/en | EVENTS-NOTIFY/UX-STATE |
| M-6 ص9 | **VOD-02 جديد:** spinner عربي داخلEN وغيابfallback عندsource فارغ؛ أنهِloading بحالة unavailable/processing/error صحيحة، بلا وعد بتسجيل غير موجود | MEDIA-ADMIN-ACCEPT/UX-STATE |
| M-7 ص10 | **VIS-02 جديد:** تداخلlogo/help بعرض390px علىmessages/competition؛ إصلاحCSS وقبول موضعيar/en | UX-STATE |
| M-8 ص10 | U-03 موسع: create يعيد201 بلاredirect/feedback وفقPDF، مقابل تأخر حسب الملخص؛ نجاح واضح وانتقال للمعرف المنشأ ومنعdouble-submit محلي. لم يثبت حدوثduplicate فعلي | UX-STATE |
| L-1 ص11 | U-01؛ إخفاء/تعطيلRemindMe غير المؤهل بعد النهاية وحالة مفهومة | UX-STATE |
| L-2 ص11 | **N-05 جديد:** التقرير يقول إن /api/notifications/:id/star غير موجود. تحقق منroute الحالي بعدreceiver fix؛ دعمcontrol القائم بعقد آمن إن كانت وظيفته مطلوبة، أو عرض إزالته إن لم تكن معتمدة؛ لا زر ميت أو404 | EVENTS-NOTIFY |
| L-3 ص11 | **VIS-03 جديد:** donate بلاmain target للskip-link؛ تعديلlandmark فقط، لاFinance audit | UX-STATE |
| L-4 ص11 | **U-04 جديد LOW:** countries ترتب بحسب الاسم المعروض واللغة، لاISO، إن ثبت الخلل | UX-STATE |
| L-5 ص11 | **U-05 جديد LOW:** copyright2025 قديم؛ سنة صحيحة من مصدر واحد | UX-STATE |
| L-6 ص11 | **N-06 جديد:** أربعةGET notifications متوازية أول التحميل؛ تتبعcallers ومنع التكرار ضمن السياق دون حذف تحديث ضروري؛ ضمنbaseline الاستهلاك | EVENTS-NOTIFY/OPT |
| L-7 ص11 | **M-05 جديد:** mark-all للرسائلclient-only؛ حفظread state بالسيرفر واستمرار صحة العداد بعدreload. startConversation بلاcallers ملاحظة وليست إذنcleanup واسع | MESSAGES |

تفاصيل إضافية:
- **N-07 TARGETED:** PDF §6 ص12 يذكر orphan invite/request عند حذفcompetition من قراءة الكود. تحقق محليًا من المسار وFK/cleanup الحالي؛ أصلح المتبقي المثبت ضمنEVENTS-NOTIFY. لا حذف إنتاجي للتجربة ولا إعادةJ.
- **S-02 TARGETED:** PDF §9 ص18 يذكر احتمالdoubleescaping لعناوينcompetition المخزنة مهربة بعد#103. اختبارrender مثلTom & Jerry بعد معرفة حالة#103 الحالية؛ عالج حد الترميز في المصدر المثبت مع حفظescaping النهائي. لا فك كيانات كل العناوين بشكل أعمى ولاmigration تاريخية تلقائية.

### 10.2 تعليم الإشعارات القديمة مقروءة — OWNER APPROVED / NOT EXECUTED

اعتمد المالك في2026-10-08T03:31:39Z تعليم **الإشعارات الموجودة قبل لحظة القرار** مقروءة مرة واحدة لأن المنصة ما زالت اختبارية. هذاcutoff ثابت؛ لا يستبدل بـnow عند التنفيذ. التفويض يشملnotification read-state فقط، لاpersonal/support messages ولاحالةinvite/request.

القائد يوجهLOCAL لإعداد أمر محدد/runbook: تأكيدdueli-db والschema وتفسيرcreated_at بـUTC؛ SELECTcount قبل، UPDATE للصفوف المؤهلة فقط معguardis_read، SELECT بعد وتحققbadge/reload. إن وجدread timestamp فاتبع عقده. الإذن الصريح يشمل هذه الكتابة الإنتاجية المحدودة بعد مراجعة الأمر؛ لا يعاد طلب الموافقة لنفس النطاق. لاDELETE/reset/seed أو تغيير دعوات أو رسائل أو أدوار. سجل العدد والcutoff والنتيجة دون نصوص شخصية. التنفيذidempotent؛ الإشعارات المنشأة بعدcutoff تحتفظ بحالتها.

هذا استثناء اختباري مرة واحدة؛ ليس قاعدة دائمةclosed=read، ولا يغني عن إصلاح الفتح والعداد والحالة المنتهية. KEEP NOW والتاريخ محفوظان.

### 10.3 حسم اختلاف N-03 بأقل تكلفة

داخلEVENTS-NOTIFY، لا تدقيق شامل جديد: سجلHEAD والدورcreator/invitee وحالةcompetition/request ونوع/id الإشعار والرابط. قارن الملخص السابق بـPDF §6 الذي يقول إنcreator يصل للقرار. على حالةQA فعالة واحدة، اختبر النقر الحقيقي منdropdown بعد إصلاحreceiver ومنView بصفحة الإشعارات: هل تظهرAccept/Decline للمستخدم المخول؟ إن انتهى الطلب، تعرض حالته دون أزرار مضللة.

حدد سبب الاختلاف: مسار أو دور أو حالة أو نسخة مختلفة، أو عيب متبقٍ. ALREADY WORKS إذا ثبتت الصحة بالشاهد؛ إصلاح صغير إن فشل. T+B يكفيان؛ لاAstra ولا إعادةJ.

PDF وصفmobile عمومًا بأنه جيد؛ هذا لا ينفيM-01 في فتحpane وفق الملخص. قارن عرض القائمة بفتح المحادثة على390px فقط ضمنMESSAGES. غيابCompose لا يعني غيابprofileMessage المثبت؛ لا تعاد رحلة موجودة.

### 10.4 ترتيب التنفيذ والإغلاق

لا يوقف التحديثDIAG أوREMOTE نشطًا ولا يفترض حالته. القائد يحدث04 من الواقع الحالي قبل تكليف جديد. الأولوية: DIAG→OPT للاستهلاك؛ EVENTS-NOTIFY (N-03 والتنظيف المأذون)؛ MESSAGES/PROFILE-SAVE؛ HOME-UX/UX-STATE؛ MEDIA/ADMIN؛ ACCEPT-REM. التوازي حيث لا تتعارض الملفات والتبعيات.

DoD: تعطلDB يحاكى محليًا/preview بحقن خطأ محدد لإثبات رسالة واضحة وretry محدود، **لا استنفاد الحصة الحقيقية عمدًا**. DB-01 لا يغلق بمجرد التعافي؛ يلزم قياس قبل/بعدrowsRead/rowsWritten وتكرار الطلبات وبناءsession وميزانية استخدام، وقرار استضافة مأذون عند الحاجة.

الإضافات ضمن الوحدات القائمة، لاPR لكل صف. لكل عيب شاهد قبول أوALREADY DONE بعينة موضعية؛ BLOCKED للadmin/media ليسPASS. WORKLOG/PLAN-STATUS في كلPR كود، ثم بروتوكول10 وتحديث04. لاH7 جديدة ولا إعادةTURN/Finance/Ads/J.


### 10.5 R4-DB-DIAG-1 — تقرير LOCAL مستلم، REVIEW PENDING (2026-10-08)

- **تشخيص READ-ONLY مكتمل محليًا فقط**: لا تعديل كود/PR ولا استعلام إنتاجي. HEAD المحلي `d020d8c` لا يطابق BASE `2e3d368`، والشجرة متسخة بملفات ELO/وثيقة غير متعلقة بالقياس. لا تعتبر الحالة CODE MERGED أو OPT DONE.
- **أدلة EXPLAIN المحلية**: مسح ratings على competitor_id؛ مسح competitions لعد creator/opponent ولملف المستخدم؛ users is_active؛ الاتجاه المعاكس للحجب؛ وفرز SSE خارج فهرس (channel,created_at). بعض مسارات status/likes/PK مُفهرسة بالفعل. راجع خطة التنفيذ الفعلية لكل استعلام قبل تعديل الفهارس.
- **مصادر التضخيم**: إعادة بناء T0 لكل rail/status/filter/identity، وsearchUsers يحمّل جميع المستخدمين، وSSE polling كل 10 ثوانٍ/اتصال؛ تكاليف continuation أقل من T0. البذور المحلية تتضمن recorded اصطناعيًا بخلاف مسار completed+VOD في الإنتاج؛ لا تعتمد قبول recorded عليها وحدها.
- **حدود الأدلة**: rowsRead/rowsWritten الفعلية غير مقاسة محليًا؛ أرقام DAU ‏500/125/40 للخفيف/المتوسط/الثقيل تقديرات عند 278 منافسة و26 مستخدمًا، وهامش 50%، **وليست سعة إنتاجية معتمدة**. بيانات Cloudflare السابقة مرجع baseline تاريخي منفصل. يجب إثبات before/after الحقيقي، وتكرار الطلبات، وT0/continuation، والتكلفة الثابتة، والكتابات؛ لا يُغلق DB-01 بالتعافي أو EXPLAIN وحده.
- **مقترح OPT وليس تفويض تنفيذ**: فهارس موجهة لratings(competitor_id)، competitions(creator_id/opponent_id)، users(is_active)، user_blocks(blocked_id)، sse_event_log(channel,id) بعد فحص الحجم والخطة، ثم تحسين T0/البحث/التكرار **إذا أثبت القياس الحاجة**؛ الفهارس وحدها لا تضمن خفض rowsRead المطلوب. أي migration أو كتابة إنتاجية تحتاج بوابتها وتفويضها، ولا تفويض فوترة/نقلDB. احفظ H7-v1، actual participation، الحجب، العزل، الترتيب، continuation حتى النفاد، وحد100 binds.
- **DoD OPT**: baseline واقعي قابل للمقارنة + EXPLAIN محلي/بيئة مأذونة، قياس rowsRead/rowsWritten/executions وT0 وcontinuation قبل/بعد، اختبارات تكافؤ، وdegraded UI مع retry محدود بحقن خطأ محلي/preview، لا استنفاد الحصة الإنتاجية. **التوجيه التاريخي (ليس تكليفًا حاليًا)**: مراجعة DIAG وتحديد أصغر OPT؛ لا تكليف مكرر.
- **PR#103 منفصل OPEN**: اختبر S-02 (stored encoded title مثل Tom & Jerry) ومسار create→persist→render قبل REMOTE FINAL؛ لا دمج بمجرد CI.

### 10.6 انضباط الذاكرة والتقارير — توجيه المالك الملزم

- **ملفات الخطة هي سجل العمل الدائم، لا سياق المحادثة**: كل ملاحظة أو قرار أو نتيجة أو قيد يُضاف **بجوار الخطوة ذات الصلة** في 12/03/08، وتُحدّث حالة 04؛ 10 يحفظ البروتوكول العام. لا تعتمد على أن القائد سيتذكر معلومة من رسالة سابقة، ولا تكرر نصوصًا مطولة في كل handoff.
- **كل موجه LOCAL/REMOTE/مخطط/استكشافي يفرض تقريرًا بالغ الاختصار**: الحالة PASS/FAIL/BLOCKED، HEAD/PR، حتى 5 نتائج مؤثرة بدليل مرجعي، العوائق، التوجيه التاريخي (ليس تكليفًا حاليًا). التفاصيل/SQL/EXPLAIN/صور/مصفوفات الاختبار في ملفات repo أو مرفق مُشار إليه، لا في الرد؛ لا تكرر تاريخ المشروع أو سجل الاختبارات الطويل. اذكر الاستثناء فقط إن كان التفصيل ضروريًا لقرار أو سلامة.
- لا توقف مهمة نشطة ولا تعيد تكليفها لتوثيق الملاحظات. تحديث الخطة ليس تنفيذًا أو إغلاقًا للكود.
