# Dueli — بروتوكول التكليف والمراجعة والدمج والنشر

**ملزم للقائد وLOCAL وREMOTE.** يكمّل 02/03؛ لا يغير سياسات المنتج في 08 ولا يعيد فتح الأعمال المغلقة. تحديث 2026-10-03 بعد #81/#82.

## 1. بطاقة التكليف — مرجع لا يعتمد على الذاكرة

كل LOCAL يستلم:
- CODE repo، UNIT، رابط الخطة وcommit الخطة وملفاتها/مقتطف نطاق الوحدة وDoD.
- BASE محدد من قراءة main الحالية في GitHub، وbranch جديدة للمهمة، وتبعيات وملفات يملكها المنفذ.
- حدود التنفيذ والاختبارات المستهدفة، وما إذا كان مسموحاً نشر/remote write. الافتراضي لا.
- كل REMOTE يستلم PR URL وHEAD الحالي وBASE الفعلي وcandidate/merge SHA الذي اختُبر، مع كيفية checkout؛ لا branch name وحده.

عند الاستلام: fetch من الريموت ثم تحقق أن BASE موجود وأن الشجرة صحيحة ونظيفة. لا يشترط أن HEAD لفرع العمل يساوي main بعد بدء العمل. لا تفرض origin/main==BASE للأبد. إذا كان التكليف قديماً قبل البدء، يثبت القائد main الجديد ويحدث التكليف بعد فحص الاعتماديات؛ لا يطلب العامل تخمين SHA أو تنفيذ reset --hard على عمل قائم. clone/worktree معزولة أفضل من إعادة استخدام detached/ahead checkout مجهول. اقرأ خطة repo المنفصلة من رابطها؛ إن تعذر الوصول يرفق القائد النص اللازم، لا يكلف وكيلًا بمدخلات ناقصة.

## 2. PR واحد وHEAD واضح

- LOCAL يفتح PR للوحدة إلى main، ويقدم HEAD الكامل. لا دفع مباشر إلى main ولا force-push إليه.
- أي remediation تدفع إلى PR نفسها ما دام النطاق نفسه، ويصدر HEAD جديد؛ APPROVE القديمة لا تغطي التعديل الجديد.
- لا فروع تجميع/دمج stack/cherry-pick أو PR موازٍ لنفس العمل، إلا تبعية صريحة موثقة. القائد وحده يسلسل الدمج؛ التنفيذ المستقل جائز، الدمج إلى main واحد في كل مرة.
- لا تحذف فرعًا أو تغلق PR كوسيلة «إصلاح» فشل CI. لا merge/force/revert أو تغيير أسرار وrulesets من LOCAL/REMOTE.

## 3. شرط الدمج — APPROVE وحدها لا تكفي

القائد يقرأ GitHub مباشرة قبل الدمج ويثبت:
1. PR الصحيحة في repo الصحيح، base=main، HEAD يطابق آخر REMOTE APPROVE، لا تعارض ولا تغييرات خارجة عن النطاق.
2. checks المطلوبة نجحت على آخر candidate المرتبط **بالـHEAD والـbase الحاليين**، مع run URL/event/check name/SHA الحقيقي في checkout. لا مساواة بين HEAD وrefs/pull/.../merge؛ لا اعتبار نجاح PR قديم أو synthetic merge قديم دليلاً للدمج الحالي.
3. الانتظار حتى اكتمال runs. pending/queued/in_progress/unknown ليست نجاحًا؛ skipped/neutral لا يغلق فحصًا مطلوبًا. continue-on-error التاريخية تبقى كما هي؛ لا تُرفع بوابات قديمة إلى blockers جديدة.
4. workflow النشر نفسه صالح وفق سياقات GitHub، لا YAML parsing وحده. إذا تغير CI/deploy: تحقق من run فعلي غير فارغ أو workflow validation صريح؛ نجاح Quality Gate لا يثبت صلاحية deploy.yml. لا تجاهل failed check باعتباره «نشرًا بعد الدمج» إذا كشف invalid workflow أو عيبًا فعليًا في التغيير.
5. تحديث base: إن تقدم main، افحص delta والتعارض/التبعيات. حدث فرع المرشح بطريقة عادية/أعد تحضير candidate إذا لزم، وشغّل ما يلزم للتكامل الجديد وأعد REMOTE للجزء المتأثر. لا rebase/إعادة suite شاملة آلية لكل تقدم main، ولا تمرير مراجعة قديمة على تركيب غير مختبر.
6. فشل اختبار: اقرأ اسم الخطوة/log/assertion؛ ميّز product failure/test clock flake/environment/schema/workflow. لا تعطيل/حذف assertion أو تجاهل gate. يسمح rerun مضبوط مرة عند سبب transient مدعوم، وتوثق الأولى والثانية؛ تكرر الفشل = remediation مستهدفة. لا إعادة TURN/Finance gate لأن اختبار توقيت فشل.
7. نفّذ merge عبر GitHub مع **expected_head_sha** الذي وافق عليه REMOTE، ومرة واحدة. إذا رفض SHA/moved base/conflict تحقق مجدداً؛ لا تعطل الحماية أو تغير الطريقة للمرور.

## 4. بعد الدمج — لا انتقال أعمى

- اقرأ merge result ثم main الحقيقي وmerge SHA/parents/history. سجّل المدموج في 04؛ لا تعِد دمجه ولا ترسل للمهمة التالية SHA من الذاكرة.
- انتظر Quality Gate للـmerge commit الفعلي، ثم تحقق مسار النشر المقرر لنفس إصدار الكود. لا إعادة full suite يدويًا إذا CI تؤديها بالفعل.
- failure على main = MERGED / POST-MERGE BLOCKED، لا DONE تشغيلي. أصلح السبب المحدد عبر LOCAL→REMOTE→PR جديد. توقف عمليات دمج features التالية حتى حسم blocker؛ يجوز تصميم D0 أو عمل مستقل لا يتسبب بنشر جديد.
- لا revert تلقائي بسبب X حمراء: rollback فقط عند أثر مثبت وخطة متوافقة ومراجعة القائد وتفويض العملية. لا reset/seed/DROP أو restore DB من أجل CI.
- بعد نجاح merge checks، حالة CODE DONE. DEPLOYED تحتاج run ناجح بهوية المشروع/البيئة والإصدار؛ PROD VERIFIED تحتاج إثبات production المعني، لا green preview check أو آخر run مختلف.
- قبل LOCAL التالية: اقرأ main جديدًا من GitHub وأصدر بطاقة جديدة. propagation/cache mismatch لا يُحل بتخمين المرجع؛ أعد قراءة ref وcommit.

## 5. عقد النشر — مسار واحد معروف

- حدد مسارات النشر الفعلية: GitHub Actions وCloudflare Git integration. وجود green Cloudflare مع فشل Actions ليس إثبات أن gate عملت.
- لا مسار نشر يلتف على Quality/schema gate. حدد topology الفعلية والبيئة بالدليلأولاً؛ لا تفترض أنكلCloudflare check مسارproduction مستقل، ولا تعطل parallel path افتراضياً. جهز التصحيح الموافقعلىtopology فيrunbook؛ dashboard changes بتفويضالمالك فقط. نجاحActions وحدهلايثبتكلإعداداتdashboard.
- لا polling فوري لآخر run ثم الفشل لأن Quality لم تبدأ بعد؛ orchestration تنتظر workflow الصحيح/نفس commit وevent وتقيّم conclusion بعد completed مع timeout وخطأ واضح، وتحدد repo صراحةً حيث CLI لا تملك checkout.
- checkout/build/artifact/SHA المنتظر يجب أن يمثل النسخة نفسها. نجاح head لا يسمح نشر synthetic merge مختلف دون إثبات مطابق.
- preview/production bindings منفصلة كما في05 §7؛ لا أسرار production لكود fork غير موثوق.
- secrets غير مسموحة مباشرة في step if؛ استخدم الآلية الموثقة الآمنة (env/outputs مناسبة) دون طباعة القيم. actionlint أو validation مكافئ يراجع expressions/contexts وليس YAML فقط.
- schema readiness تبقى read-only، والتطبيق الخارجي وفق التفويض وrunbook، لا blind migrations أو bypass gates.

## 6. سجل إلزامي مختصر في 04

UNIT | PR | BASE | approved HEAD | tested candidate SHA/event | REMOTE | merge SHA | main Quality run/result | deploy run/environment/SHA | status/blocker | NEXT.

حالات مستقلة: LOCAL IN PROGRESS، REMOTE، APPROVED، MERGED، POST-MERGE BLOCKED، CODE DONE، DEPLOYED، PROD VERIFIED. وثيقة/تصميم لا تتطلب نشرًا وتغلق DOCS DONE بعد قراءة المحتوى المدموج؛ لا فرض CI المنصة على dueli-plan.

## 7. واقعة #81/#82 — أدلة محددة لا استنتاج واسع

Code main المقروء: cb80789b20c3f766b3deec8b16d7ed8393aa57ed.
- #81 merged: daa449b85d22704326a31d0d644ee45542dbc3b5؛ main Quality نجاح [run37084529534](https://github.com/Maelsh/dueli-opus/actions/runs/37084529534)، deploy [run37084528681](https://github.com/Maelsh/dueli-opus/actions/runs/37084528681) فشل.
- #82 merged: cb80789b20c3f766b3deec8b16d7ed8393aa57ed؛ PR Quality على head05b8c80 نجاح [run37117854306](https://github.com/Maelsh/dueli-opus/actions/runs/37117854306)، main Quality [run37125477474](https://github.com/Maelsh/dueli-opus/actions/runs/37125477474) فشل: 1114 passed/1 failed، assertion وقت في tests/api/turn-credentials.test.ts يتجاوز الحد ثانية واحدة. يرجح حساسية ساعة الاختبار؛ لا إثبات خلل خدمة TURN ولا جولة بوابة بث.
- deploy على cb80789 [run37125477000](https://github.com/Maelsh/dueli-opus/actions/runs/37125477000) فشل بلا jobs. deploy.yml تحتوي secrets.CLOUDFLARE_API_TOKEN مباشرة في if؛ هذا مخالف لسياق GitHub الموثق. سبب تشخيصي مثبت بالكود مع runs بلا jobs؛ لم نسترجع annotation parser نفسها.
- check Cloudflare Pages id111209903606 لنفس cb80789 سجّل successful deployment عند13:14:40Z، قبل انتهاء Quality الفاشلة13:15:12Z. هذا يثبت وجود مسار نشر Cloudflare لا ينتظر هذه Quality، لا يثبت نوع production/preview أو سلامتَها من الواجهة. يلزم حسم المسار قبل تشغيل الإصدار المعتاد.
- الصورة لا تثبت وحدها دمج فرع خاطئ أو فقد commits. لا اتهام rebase/force بلا دليل. المؤكد: success PR وحده لم يغلق main/release، وعقد النشر غير مكتمل.

**NEXT تاريخياً عند#82، وأُغلقت في#83: R-RELEASE-1-REM1**: صلاحية deploy expression، تنسيق انتظار Quality لنفس candidate، حسم مسار Cloudflare الموازي، ومعالجة فشل الساعة المستهدف في main دون تعديل TURN runtime أو gates التاريخية. LOCAL→REMOTE→merge→main CI→deploy evidence؛ لا feature merge تالية قبل حسم blocker. D0 تصميم قابل للاستمرار.

## 8. توثيق PR والمدخلات المنفصلة — ملزم

كل PR كود تشمل WORKLOG.md وPLAN-STATUS.md داخل نفس PR؛ تصف ما اختبر وحالة LOCAL VERIFIED / awaiting REMOTE، ولا تعلن DONE / DEPLOYED قبل حدوثهما. بعد الدمج والبوابات يحدث القائد 04 بالحالة المثبتة. لا PR توثيق شكلي منفصل لكل تغيير، ولا حالة متفائلة في main لإغلاق عمل ناقص.

كل LOCAL مكتفٍ بذاته: رابطا code وplan، commit الخطة، الملفات والأقسام وروابطها أو النص اللازم، BASE الحالي، UNIT والنطاق المحدد وقرارات المالك وDoD والاختبارات ومتطلبات السجل. لا يفترض رؤية repo الخطة من checkout الكود. إذا تغير BASE يعود للقائد لتحديث التكليف وفحص الأثر.

صلاحيات Cloudflare في repo secrets محدودة: Pages Edit + D1 Read للحساب المحدد وفق قرار المالك. لا Global API Key أو توسيع للصلاحيات لإسكات readiness. remote migrations/write/restore تتطلب تفويض المالك المحدد؛ بوابة النشر تقرأ الجاهزية فقط.

حادث #81/#82 عولج في #83، وmain gates خضراء في #84/#85؛ هذه القواعد مستمرة، ولا يعاد الحادث كعائق تاريخي. NEXT الحالي في 04 و05 §9.
