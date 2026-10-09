# Dueli — وحدات التنفيذ وموجهات LOCAL/REMOTE

> **المزامنة الحاكمة — 2026-10-09:** CODE MAIN `375bd1809482d21ce2abd4aa7e6c013704967e50`؛ PR103–106 مدموجة، وPR106 post-merge Quality/Deploy SUCCESS. لاPR كود مفتوحة وقت المراجعة. NEXT: **R4-LIVE-INT-1** وفق [13-LIVE-CHUNKS-UNIFIED-GUIDE-PLAN.md](13-LIVE-CHUNKS-UNIFIED-GUIDE-PLAN.md). بقية الاستعادة في12 محفوظة؛ DB-01 OPEN للقياس، وتنظيف الإشعارات غير مثبت التنفيذ. الحالات التاريخية أدناه ليست NEXT الحالي. لا إعادة أعمال مغلقة أو تنفيذ103–106 مجددًا.

> **H7 معتمدة وثابتة:** السياسة الرقمية في11، وD0/D1/D2 مغلقة وفق04. لا إعادة تصميم أو اعتماد الأوزان؛ تحسين الاستهلاك يحفظها.

> **قرارات المالك المعتمدة — 2026-10-01:** اقرأ [08-OWNER-DECISIONS.md](08-OWNER-DECISIONS.md)؛ يعلو على المقترحات السابقة. السياسة محسومة، أرقام H7 معتمدة في11، ولا يعاد طلب اعتمادها، والإجراءات الواقعية تسجل منفصلة عن اعتمادها.

**مزامنة R4 بعد #102.** اقرأ 01 للنطاق و 05 للمواصفة و 04 للحالة. R1 مغلقة. عدد الوحدات ليس عدد PRs مفروضاً؛ كل وحدة متماسكة بقدر متوسط، والجزء المنجز يغلق ALREADY DONE بدليل موضعي دون إصلاح شكلي.

## مواصفات الوحدات السابقة — حالة الإغلاق في04؛ لا تعاد

الوحدات المغلقة أدناه مرجع عقود، وليست قائمة تكليف جديدة. وحداتR4 الحالية في12.

## وحدات العمل ومعايير الإغلاق

| الوحدة | النطاق ومعيار القبول | الاعتماد / التحقق |
|---|---|---|
| **R3-GUEST-1 — DONE #76** | استمرار Guest حتى النفاد على جلسة#75؛ قبول المالك مثبت. | لا إعادة تكليف؛ عزل tabs الجديد في RAILS. |
| **R2-AUTH-1 — DONE #77** | تطبيع/عقد خطأ واستعادة؛ #78 للدومين و#80 UX. وصول Spam لا يعني ضمان Inbox. | قرار المالك: لا deliverability investigation الآن؛ ليست dependency لـJ. |
| **R3-B7 — DONE #75** | Explore competitions وبنية جلسة/chunks/cursor مشتركة. حفظ الشكل 6+6 ودلالة ترتيبها الحالي مرة بالجلسة. أكثر من 1000 مرشح محلي يعرضون مرة حتى النفاد بلا سقف؛ retry وتغيّر درجات وفقد أهلية وهوية وفلتر و TTL و preview/view-all صحيحة. لا نهاية من client dedup. تسجيل تكلفة البناء والقراءة. | مدموجة، لا إعادة تكليف؛ مرجع بنية D1/D2. |
| **R-RELEASE-1 — DONE بعد #83** | workflow/SEC-06/preview isolation/schema readiness gate؛ التفاصيل الملزمة 05 §7. لا migrations عمياء أو remote write من المحلي. | مغلقة؛ لا إعادة؛ البروتوكول10 مستمر. |
| **R3-RAILS-1A — CODE MERGED #82** | providers وسياق وفلاتر كل Home rails على مخزن الجلسة الموجود؛ تهيئة provider للأوزان المعتمدة لكل قسم وفرع؛ freeze داخل الجلسة فقط، لا random-only نهائي. | البنية مدموجة ومشكلة الإصدار أغلقت في #83؛ لا إعادة. الأوزان في D1 بعد D0. |
| **R3-RAILS-1B — CODE MERGED #82** | near-end horizontal fetch per rail حتى exhaustion؛ retry/reset/ar-en/mobile-desktop؛ 05 §8. | البنية مدموجة؛ عقد View All الناقص في الوحدة التالية، والأوزان في D1. |
| **R3-EXPLORE-CONTEXT-1 — DONE #86** | View All ينقل category/subcategory/status، وExplore يتيح الفرع ويحفظ URL وسياق الجلسة حتى النفاد؛ المواصفة وDoD في 05 §9. | مغلقة#86؛ المواصفة محفوظة، لا إعادة تكليف. |
| **R0.1–3** | القائد يعرض بطاقات 05 ويعد إجراءات البنك/الكيان/المزوّد والمسؤول. تحفظ إجابات المالك والإجراءات اللازمة؛ لا تنفذ الإنتاج ضمن تكليف LOCAL. | بالتوازي؛ H، لا S. |
| **R2-J — DONE #85** | الدعوة/الطلب والقبول/الرفض/الانتهاء، accepted_at في atomic، إشعار وترجمة ورابط صحيح، سجل صادر/وارد، أزرار الدور والحالة. A يدعو B وحالتهما محفوظة بعد refresh؛ السباق ينتج خصماً واحداً؛ التعايش وفق H3؛ أخطاء 401/403/409 مرئية وقيم الحالة موافقة للمخطط. | H3 معتمدة في 08؛ T+B ar/en. |
| **R2-L1 — CLOSED #87/88/89** | تعليقات مشتركة محفوظة API/SSE بأسماء وأعداد صحيحة و dedup بالمعرف؛ مشاهدة مؤهلة وحضور مستقل، GET لا يزيد العد. A/B/C ترى نفس التعليقات بعد refresh؛ نبض مكرر لا يضاعف المدة أو العد؛ أهلية V تقرأ الكاتب الصحيح. | R3-EXPLORE-CONTEXT-1 وJ؛ H1=300 ثانية و H2 معتمدتان؛ T+B. |
| **R2-V — CLOSED #90** | تقييم 1..5 لكل طرف بعد 300 ثانية وتعديله واستبدال مساهمته، حصيلة live ظاهرة مؤقتة، الإغلاق النهائي SQL و resultFinal/finalize. اختبار قبل/أثناء/بعد وسباق الإنهاء؛ قبول قبل cutoff فقط؛ النتيجة/ELO/التوزيع مرة مع retry. لا نافذة بعد النهاية ولا تغيير معادلات أو تاريخ. | L1؛ H4/H5 معتمدتان؛ T+B وأثر مالي مستهدف للتوقيت فقط. |
| **R2-L2 — CLOSED #91** | غرفة المنافسة الإنتاجية ووظائف البث المدمجة، دخول الأدوار والمشاهد والتحكم والإنهاء، الوسائط والتسجيل والانتظار والفشل، إعلان على عقد قائم و Like/Dislike بدلاً من القلب وتعليقات مرتبطة بزمن الفيديو وقائمة نهائية مرتبة. T/B تثبت الربط والمهلة وجاهزية التسجيل وانطباع الإعلان مرة دون تغطية. S مؤجلة إلى R4. | J/L1/V؛ T+B ثم S مجمعة. |
| **R2-A — CLOSED #92** | حساب admin/admin المؤقت وإعدادات username/password/email ونظام الوثائق/البيانات من واجهة المدير، مدخل الإدارة وحراسة الوصول، توافق الدور/is_admin وقيود الدور، runbook/bootstrap لهوية ودور وسجل تدقيق. مسؤول اختباري يعمل والعادي ممنوع API؛ منح/سحب الدور فعّال ولا يمنح دوراً أعلى. dry-run جاهز، لا فعل إنتاجي بلا H8. | مستقل؛ T+B، H8 للإنتاج. |
| **R2-M — CLOSED #93** | رسائل شخصية، ونظام رسائل إدارة مستقل ببيانات/مسار/تبويب وهوية Dueli/الموظف الإداري وإشعار unread خارجي؛ إصلاح الأيقونة الحالية. مستخدمان يتراسلان بعد refresh؛ طلب الإدارة يُقرأ ويُرد عليه دون كشف بيانات الآخرين. | A للهوية/الصلاحيات؛ H6 معتمدة؛ T+B personal/admin منفصلان. |
| **R2-P — CLOSED #94** | طرق الصرف CRUD/default وربط طريقة محفوظة مملوكة بـ id و snapshot التفاصيل اللازمة بالسحب، مع توافق القديم. حفظ/تعديل/حذف/افتراضي واختيار تعمل؛ غير المالك ممنوع؛ تعديل لاحق لا يغير طلباً معتمداً. لا تحويل فعلي. | مستقل؛ T+B، البنك الحقيقي H في R0. |
| **R2-F — CLOSED #95** | قائمة قصيرة من نواقص الرحلات الأصلية خارج R1: إشعارات، ملف، حذف حساب، اجتماعي، تبرع، معلن وإشراف. كل ناقص محدد مكتمل أو ALREADY DONE؛ لا إعادة بوابات الخدمات. | فحص موضعي؛ T+B. |
| **R3-D0 — DOCS DONE / OWNER APPROVED** | h7-v1: كل الجداول والصيغ والحداثة والتنوع والمفضلات وfallback معتمدة في11 بتاريخ2026-10-04. | لا تكليف تصميم/اعتماد جديد؛ التنفيذ في D1/D2. |
| **R3-D1 — CLOSED #96/97** | ترتيب بالأوزان المعتمدة لجميع Home rails Guest/User وكل قسم وفرع والبحث والمشابهات على بنية B7؛ استمرار وحده لا يكفي لإغلاق Home. حالة تبويب Home تمر فعلاً؛ الزائر يرى upcoming؛ أمثلة صلة وجودة وتنوع معتمدة؛ جميع المؤهلين يصلون عبر الصفحات، لا أول 100 فقط. | B7+D0؛ مشاهدة مصححة إذا استخدمت إشارتها؛ T+B. |
| **R3-D2 — CLOSED #98** | مؤشر Profile المحسوم وعرضه وسجله وترتيب بحث المستخدمين؛ اقتراح الخصم يبدأ بالقسم الفرعي واللغة والبلد ثم الرئيسي، بحث واقتراح المستخدمين للمتابعة/المواجهة، competition→user و user→competition، ثبات التمرير رغم تغيّر الحضور، وإعادة أهلية الدعوة عند إرسالها. المتابع المؤهل لا يستبعد من المواجهة و busy لا يمنع المتابعة؛ حظر/ذات/تعارض محفوظة. | D1/J و H7؛ T+B. |
| **R3-C1 — CLOSED #99** | مساعدة سياقية و FAQ وأدلة الأدوار، i18n و RTL/focus/تكبير وإتاحة للأسطح المتبقية. نص وروابط وأسماء controls واضحة وفحص keyboard/axe للمواضع المعدلة. | مستقل حيث لا تعارض ملفات؛ T+B، S قارئ شاشة لاحقاً عند سؤال حصري. |
| **R3-C2 — CLOSED #101** | واجهة إدخال/تحرير/رفع ونشر وثائق وبيانات المدير وفق H9، والحقيقيات بعدالإطلاق دونتعديلكود؛ القانون/المنتج حسب الحاجة، رسالة المشروع والهندسة والمصدر المفتوح ومساهمة AI، ar/en. نصوص وروابط صحيحة وموافقات المالك/المختص اللازمة قبل النشر. | R0/H؛ مراجعة نص وروابط، لا S افتراضياً. |
| **R3-C3 — CLOSED #102** | تصميم تقاعد التخليقي مستقبلاً: حد أدنى ومحفزات وحماية روابط وبيانات و dry-run. وثيقة فقط بلا حذف أو migration؛ بعد الإطلاق إذا لم يشترطه المالك. | KEEP NOW؛ تحليل+H لقرار لاحق. |
| **R4** | رحلات 01 باستخدام أدلة T/B السابقة ثم وسائط فعلية A/B→C→تسجيل وجهاز/قارئ شاشة عند الحاجة، إصلاح الحاجب، إجراءات R0 والإطلاق. صفر عيب حاجب معلوم وقبول الرحلات وقرار المالك؛ عائق جهاز موثق لا PASS كاذب. | T/B أولاً، S حصرية مجمعة، H. |

## ترتيب ومنع تعارض الملفات

الترتيب السابق حتىC3 أُنجز وفق04. NEXT الحالي: R4-DB-DIAG-1 وفق12؛ ثم التحسين المبني على الدليل ووحدات الواجهة المستقلة والقبول. R0 بالتوازي؛ D0/D1/D2 مغلقة، وH7 لا تعاد.

- J/L1/V/L2 تقتسم CompetitionController وصفحات المنافسة/الغرفة؛ تنفيذها تسلسلي، تصميم اللاحقة يمكن بالتوازي.
- B7 تمتلك مخزن الجلسة و Models/service و Explore أثناء تكليفها؛ D1/D2 بعد دمجها.
- V تمتلك RatingModel/ScheduledTaskService وأثر التوقيت الضروري؛ L1 لا تنشئ بوابة تقييم بديلة.
- A/M ينسقان الهوية وصندوق الإدارة. P مستقلة غالباً. C1 لا تعدل صفحات يعمل عليها وكيل آخر.
- القائد يوزع الملفات، لا يكلف عاملين بتعديل الملف نفسه، ولا يوقف كل المسار على البنك.

## قالب LOCAL

```text
DUELI — LOCAL — <UNIT>
CODE: Maelsh/dueli-opus | BASE: <main SHA confirmed by lead>
PLAN: https://github.com/Maelsh/dueli-plan/tree/main/dueli-completion-plan
PLAN COMMIT: <الخطة المدموجة الحالية>؛ رابط05 §<الوحدة> ومقتطفالنطاق/DoD يرفقهالقائد.
اقرأ 01 و 03 و 05 و08 و10؛ إن تعذر الوصول يرجعالقائد بالنص اللازم. نفذ <UNIT> فقط وفق نطاقها ومعيار قبولها واعتمادها.
قرارات المالك في 08 ملزمة؛ لا تعاودها. أرقام H7 معتمدة في11؛ لا تغيرها بصمت أو تعيد عرضها.
أعد استخدام القائم؛ المنجز ALREADY DONE بدليل، بلا PR شكلي.
OOP/MVC/SQL Models/ar-en/CSP. لا إعادة R1/خطة 16/خوادم/TURN/مال/إعلانات،
ولا تنظيف واسع/خدمة مدفوعة/حذف أو كتابة إنتاجية أو منح صلاحيات.
اختبر ما تغير T/B فقط؛ لا full suite أو Astra بلا سبب.
حدث WORKLOG.md وPLAN-STATUS.md داخل PR، LOCAL VERIFIED/awaiting REMOTE، بلا DONE/DEPLOYED مسبقاً.
فرع+PR متوسط دون دمج/نشر.
التقرير: BASE/HEAD/PR، التغيير والأدلة والاختبارات، المتبقي و H/DEVICE.
```

## قالب تاريخي — R-RELEASE-1 مدموجة#81، لا يعاد التكليف

```text
DUELI — LOCAL — R-RELEASE-1
CODE: Maelsh/dueli-opus | BASE: <القائد يثبت main بعد#80>
PLAN: https://github.com/Maelsh/dueli-plan/tree/main/dueli-completion-plan
اقرأ 03 و05 §7 و08 و09. نفذ وحدة سلامة الإصدار فقط.
صحح نقص تغطية SEC-06 التنفيذي مع استمرار تجاهل التعليقات/النصوص.
اضبط عقد preview/production bindings دون توريث D1 الإنتاج للمعاينة.
جهز بوابة قراءة مخطط required migrations تربط الإصدار والهدف وتمنع deploy
عند pending مطلوبة/خطأ/هوية خاطئة. لا auto-apply أعمى؛ runbook منفصل.
ربط Quality Gate بنفس SHA وقفل إجراءات الإنتاج، وفق 05 §7.
لا توسع إلى gates تاريخية أو features/rails/Auth/DNS/provider.
T مستهدفة وrunbook قابل للمراجعة. لا Astra أو full suite إضافية.
لا remote writes/deploy أو إنشاء قاعدة أو عرض secrets ضمن هذا التكليف.
فرع+PR دون دمج؛ سلّم BASE/HEAD/PR والأدلة والاعتماديات المتبقية.
```

## قالب تاريخي — R3-RAILS-1A/1B مدموجة#82، لا يعاد التكليف

```text
DUELI — LOCAL — R3-RAILS-1A/1B
BASE: <main بعد R-RELEASE-1> | PLAN: dueli-plan/main/dueli-completion-plan
اقرأ 05 §8 و08. reuse ExploreSessionService/ResultSessionProvider/chunk Models.
كل Suggested Guest/User وDialogue/Science/Talents/الفروع،
مع Live/Recorded/Upcoming: جلسة مستقلة لكل سياق، كامل المؤهلين عند T0،
horizontal near-end fetch حتى exhaustion، retry/expiry/reset واضحة.
صحح تجاهل status وحجب upcoming Guest ضمن عقد الفلاتر الجديد.
الثبات أثناء جلسة التمرير فقط؛ إعادة الدخول/refresh تعيد حساب الترتيب.
الأوزان تشمل كل قسم وفرع؛ الأرقام معتمدة في11 للتطبيق في D1.
لا RANDOM+OFFSET أو random-only كحل نهائي؛ لا pool cap15/100 أو engine موازٍ.
1A providers/context/eligibility، 1B per-rail client؛ جمعهما جائز بوحدة متوسطة.
T+B traversal بأكثر من دفعتين ar/en/mobile/desktop؛ لا Astra/وسائط/بنك.
هذا قالب تاريخي للبنية المدموجة؛ الأرقام اعتمدت لاحقاً في11. تطبيقها في D1، لا إعادة تكليف RAILS.
لا coefficients بلا اعتماد أو تنظيف واسع أو remote writes/deploy.
فرع+PR؛ BASE/HEAD/PR ودليل كل DoD، والمتبقي المحدد فقط.
```

## قالب REMOTE

```text
DUELI — REMOTE — <UNIT> — READ ONLY
PR: <url> | BASE: <sha> | HEAD: <sha>
اقرأ معيار 03 ومواصفة 05 وقرارات 08 على dueli-plan/main؛08 يعلو علىالمقترحات.
راجع HEAD المحدد مستقلاً ببيئة نظيفة؛ تحقق من الهدف والعقود والأثر المحدد.
شغّل الاختبارات المستهدفة اللازمة فقط؛ لا إعادة R1/خطة 16 أو full suite متكرر.
لا تعديل/دمج/نشر/كتابة إنتاجية أو منح أدوار. T/B قبل S؛ لا Astra بلا سبب.
سلّم APPROVE/REJECT مع دليل BASE/HEAD وموانع محددة؛ وجود مكوّن لا يكفي لقبول رحلة.
```

موجه R4/S لا يصدر إلا عند الجاهزية: سؤال حصري، جهاز/صوت/وسائط متاحة، حسابات A/B/C يرفقها المالك خاصة، رحلة واحدة وأدلة. لا تغيير كود أو أموال/حذف/مراسلة ناس. BLOCKED DEVICE إن تعذر الالتقاط، ولا استنتاج فشل خوادم.

## قالب تاريخي — remediation الإصدار مغلقة#83، لا يعاد التكليف

```text
DUELI — LOCAL — R-RELEASE-1-REM1
CODE: https://github.com/Maelsh/dueli-opus
PLAN: https://github.com/Maelsh/dueli-plan/tree/main/dueli-completion-plan
اقرأ10 و05 §7 و04. القائد يثبت BASE من main لحظة إصدار التكليف.
عالج deploy workflow expression/contexts وانتظار Quality للنسخة نفسها.
حدد Cloudflare Git integration الموازي، وجهز منع bypass وفق تفويض القائد؛
لا dashboard changes أو deploy أو remote writes من تلقاء نفسك.
شخص assertion الثانية الواحدة في turn-credentials.test على cb80789؛
ثبت زمن الاختبار عند ثبوت race دون إضعاف العقد أو تعديل TURN runtime.
لا إعادة RELEASE/RAILS كاملتين أو gates تاريخية. T مستهدفة وworkflow validation.
PR واحدة→REMOTE على آخرHEAD/candidate→القائد يدمج مع expected_head_sha.
تقرير BASE/HEAD/PR/الأدلة والمتبقي؛ لا إعلان DEPLOYED من merge فقط.
```

كل LOCAL/REMOTE من القوالب أعلاه يلتزم10؛ بطاقة التكليف تحوي repo/plan commit/BASE/branch/UNIT/DoD، وREMOTE يحوي PR/HEAD/base/tested candidate. حالات main بعد الدمج لا تسقط من التسليم.

## LOCAL التالي

**R4-DB-DIAG-1** — بطاقة LOCAL والنطاق وDoD في12 §8. لا كود أو كتابة إنتاجية فيDIAG؛ PR103 تكليف قائم مستقل. أصدرOPT فقط بعد تقريرDIAG، وبقية وحدات الواجهة المستقلة وفق12.

## تنفيذ استعادة التكامل — مرجع13 / 2026-10-09

مرجع13 حاكم للترتيب الجديد: LIVE-INT-1 → CHUNK-PLAY-1 → COMP-UNIFIED-1 وCHUNK-DOWNLOAD-1 → ACCEPT-REM. UX-I18N-1 توسعةUX-STATE، وGUIDE-1/2 فوقالتوثيقالموجود؛ لاوحداتمكررة. DB-01 وMESSAGES/PROFILE/HOME/ADMIN/R0 محفوظة وفق04/12.

### LOCAL — أول وحدة

```text
DUELI — LOCAL — R4-LIVE-INT-1
CODE: https://github.com/Maelsh/dueli-opus
PLAN: https://github.com/Maelsh/dueli-plan/tree/main/dueli-completion-plan
BASE: <current CODE MAIN confirmed by lead>
PLAN SHA: <merged plan commit>; read13 §§1–5 / LIVE-INT-1.
Read CODE AGENTS.md, docs00/01/04/05/11/13/16/18;
PLAN08/10/11/12/13. Closed work stays closed.
Production room uses legacy P2P signaling; reuse correct SignalingManager.
Start with a short actual-call map for lifecycle/upload/resume/end;
then implement the smallest shared-client integration, preserving server contracts.
Owner: only host records/uploads; host loss does not end competition;
resume appends ordered chunks, no overwrite; server-end documents final marker.
Keep test pages and reuse their correct functions; no legacy aliases/new WebRTC.
T/B first; media A/B acceptance is separate, environment BLOCKED is not PASS.
No code PR for diagnosis only; no server/billing/migration/production writes.
Update WORKLOG/PLAN-STATUS in same PR, truthful pre-merge status.
Return STATUS/BASE/HEAD/PR, at most5 evidence items, BLOCKERS/NEXT;
detailed evidence in approved repository files per10.
```

### REMOTE — لكل وحدة من13

موجه مستقل يذكر CODE/PLAN وBASE/HEAD المتوقع ومرجعالوحدةوالـDoD، ويطلب قراءةالعقود وdelta الحالي، دونتعديلكود. يراجعMVC/OOP/security/i18n والاختباراتالمحددة، ويفصلT/B/S/H. الصوتوالصورةوالتنزيللاPASSمنAPIفقط. لايكررالبواباتالمغلقة، ويسلمAPPROVE/REJECT/BLOCKED والموانعبروابطشواهد. القائديفحصCIexactHEAD ثمبروتوكول10.
