# Dueli — قوالب التكليف ومراجع الوحدات

**الترتيب والحالة وNEXT حصريًا في[14](14-UNIFIED-EXECUTION-PATH.md).** لا يصدر LOCAL لوحدة غير مدرجة فيه أو PR لها نشطة. أرقام الصفوف للعرض فقط؛UNIT ثابت.

## مواصفات الوحدات

| المجال | المرجع |
|---|---|
|العقود السابقة R2/R3|05،08،11؛ الحالة في14؛ لا تعاد|
|الرسائل/الحفظ/Home/DB/UX/cleanup/الإدارة|12 §§3/4/10.1–10.3، والتتبع في14 §§2/3|
|signaling/chunks/التنزيل/صفحة المنافسة|13 §§2–5 و15 §§2–6/10–12؛ ترتيب14|
|قوائم البروفايل32.1: المشاهدة لاحقًا والسجل|13§8 و08 قرار19أكتوبر؛ كل بند وDoD في14|
|GUIDE-1/2 والقبول المجمع|13 §5 و12 §7؛ إجراءات08؛ ترتيب14|
|تاريخ التوجيهات ومعاييرها السابقة|[نسخة03 السابقة](archive/03-PHASE-PROMPTS-before-unified-path.md)؛ ليست تكليفًا نافذًا|

MEDIA-ADMIN-ACCEPT السابق: الوسائط موزعة علىLIVE/CHUNK/COMP/DOWNLOAD؛ الإدارة فيADMIN-ACCEPT. UX-STATE توسعت إلىUX-I18N مع حفظ كلIDs في12. DB-MEASURE استكمالDoD DB-OPT لا إعادة0039. NOTIFY-CLEANUP إجراءمعتمدغيرمثبتالتنفيذ، لا receiver/starPR ثانية.

## قالب LOCAL

```text
DUELI — LOCAL — <UNIT / موضع14>
CODE: https://github.com/Maelsh/dueli-opus
PLAN: https://github.com/Maelsh/dueli-plan/tree/main/dueli-completion-plan
PLAN SHA: <current>; BASE: <current code main>
اقرأ14/04/08/10/11 ومواصفة<12/13/05 section>.
اقرأCODE AGENTS.md وdocs01/11/13/18 والعقودالمتأثرة.
نفذ<scope> فقط؛ DoD:<exact>; dependencies:<satisfied>.
قرارات08/H7ثابتة؛ لا تكررPRنشطة/مغلقة أوتوسعالنطاق.
MVC/OOP/SQL Models/ar-en/RTL/mobile/dark/CSP/a11y.
التحقق<T/B/S/H> محدد؛ لاAstra/full suiteبلاسبب.
التفويض:<explicit scope or no production writes>.
حدثWORKLOG/PLAN-STATUS فيPR بحالةصادقة؛ لاDONEقبلالدمجوالبوابات.
فرع+PR دوندمج/نشرذاتي؛ detailed evidence in repo.
RETURN STATUS/UNIT/BASE/HEAD/PR + ≤5 evidence + BLOCKERS/NEXT.
```

## قالب REMOTE

```text
DUELI — REMOTE — <UNIT / موضع14> — READ ONLY
CODE: https://github.com/Maelsh/dueli-opus
PLAN: https://github.com/Maelsh/dueli-plan/tree/main/dueli-completion-plan
PLAN SHA:<sha>; PR:<url>; BASE:<sha>; HEAD:<exact sha>
اقرأ14/08/10/11 و<spec section/DoD> وعقودCODEالحاكمة.
راجعexactHEAD/currentBASE مستقلاً؛ اختباراتمايتغيربقدركافٍ.
لاcode changes/merge/deploy/prod write أوإعادةبواباتمغلقة.
T/Bأولًا؛ الصوتوالصورةوالملفلاPASSمنAPI/وجودرابط.
RETURN APPROVE/REJECT/BLOCKED + HEAD + ≤5 findings + blockers.
```

## قالب تخطيط جديد / تغيير أولوية

```text
DUELI — PLAN CHANGE — NO CODE
PLAN14:<current SHA>; new/change UNIT:<id>; source:<evidence/owner>
Old order:<units>; New order:<units>; displaced:<each UNIT→new position>.
Scope/DoD/dependencies/status/T-B-S-H:<exact>; owner decision:<if new>.
Update14 + relevant spec +08(if decision) +04(if handoff changes) in SAME PR.
Preserve all old IDs/DoD; no orphan addendum/hidden NEXT/drop.
No reopening closed work; no cancellation without explicit owner decision.
Return PR/HEAD/changed files + coverage before/after + NEXT per14.
```

R4/S موجهه سؤال حصري وجهاز/وسائطمتاحة وحساباتA/B/Cتسلمخاصًا؛ يجمعتجربةP2P→الجمهور→التسجيل→التنزيلوانقطاعالمضيففيجلسةواحدةعندالجاهزية. BLOCKEDDEVICEلايعنيفشلالخوادمولاPASS. قبولالهاتف/اللغة/النقربـB أولًا.

## بطاقة وحدات المقاطع الجديدة

ارفق15 §الوحدة المطلوبة +08 قرار11أكتوبر فيLOCAL وREMOTE؛ INDEX27/T-B،SAFE28/T-B+endpoint محدود،PLAYER29/T-B ثمS،DOWNLOAD30/T-B ثمMP4تشغيلفعلِي. T/B للmetadata/auth/race/cache لا يحتاجAstra؛S للأسئلةالصوتية/المرئية فقط. PR110 محفوظة؛ لا تكليف متنافس. الحقوق فيGUIDE38/39 والقبول41، وDB-MEASURE34 يضمmetadata. التفويضالخارجي محددلايفترض مندمجالخطة.


## ملحق بطاقة التكليف — اعتماد19أكتوبر

بالإضافة للقالب أعلاه، أرفق15§12.2/القسم الخاص بالUNIT وIDs منO19-01..21. لتعديل أدواتالبث اذكرمساراتhost.ts/guest.ts/test.css المرجعية صراحة؛ أيقوناتوألوانوأشكالالاختبار لا تصميمذاتي، دوننسخمنطقالاختبار. افصل CONFIRMED عنفرضيةالسبب قبلpatch، وحدد T/B للمنطق/الشبكة وS للحكم الصوتي/البصري فقط. اذكرCODE/PLAN/PRODUCTION وAGENTS/docs01/11/13/17/18 وقرارات08 وبروتوكول10؛ لا تفترض اطلاع الوكيل على مستودع الخطة. مراجعةREMOTE تشملربطالمستهلكالفعلي والroute لاModel/APIوحدهما؛ لا تدعيقبولوسائطمنmock. LOCAL→REMOTE→دمجوفق10، دونتوسيعنطاق مستقل أوتكليفينمتداخلين.

## بطاقة تحققFV2230 — اعتماد20أكتوبر

كلLOCALلـ28.3.1/28.4.1/28.5 يرفق15§13.2 والـIDsالمحددةوقرار08/20أكتوبر. حددمسبقًا: (أ) دليلbadpathوالسببقبلpatchمنLOCAL/T-B، (ب) الفرضيةالتيتحتاجtraceوالتصرفإنلمتثبت، (ج) اختباراتالإغلاقبعدالتنفيذ، (د) مايراجعهREMOTEعلىexactHEAD، (هـ) سؤالSالصوتي/البصريالحصري. لاجولةتشخيصمنفصلةمفروضة، لاPASSمنmockأوصورة، لاإعادةماجربونجحإلاإنأثرتغييرجديد.
REMOTEيفحصإصلاحcursorوالتصفيةوالتعافيبدفعاتمحدودةودونتسريب، التوستوالتفاوضمنالمسارالفعلي، عدمجمعoffsetمرتين، ثمend/الأجهزة/التصريف/marker بحسبالـUNIT. عقدmetadata/الذاكرةوD1محفوظ. التقاريرالمنقحةتفرقPROVEN/HYPOTHESIS/UNKNOWNوالمحليعنالإنتاج؛ الشبكةلاتسلممعأسرار.

## بطاقة متابعة قبول2242 — اعتماد21أكتوبر

موجهLOCAL التالي يشيرإلىحزمةUNIT28 في14 و15§14: A28-LEASE→SURFACE→TIME، بملكيةواحدة وبلاعملمتداخل؛ BASEحديثومقتطفالتقريروالعيوبوالـDoD والأدلةالمتاحة. قبلpatch يثبتمساراتnetwork/expired/takeover، استثناءاتterminalteardown، ومستهلكtimeDisplay الفعلي. موجهREMOTE يطلباختباراتالاستحواذوالكتابةالقديمةوالاستئنافappend، نهايةمعمسجلسليم/محبط، والزمنبعدseekعلىMSE/blobإنمستخدم؛ لااكتفاءبمعادلةغيرموصولةللواجهة.
التكليفS بعدالنشر محدود15§14.4: انقطاع→تسجيلمستأنف، endوالطرفانينشران→VODلكلأدوار، وقتصحيح، وصوت/انتقالبقدرالتعديل. SCREEN يتبنىدليلًامناسبًاغيرمتأثرأويختبرالنقطةالمفقودةفقطبمتصفحcapture؛ BLOCKED ليسPASS. previewملاحظةتتبعلاجولةتشخيصمفروضة. اقرأAGENTS/docs01/11/13/17/18ذاتالصلة و08/10/14/15؛ كلPR يحدثWORKLOG/PLAN-STATUSبحالةصادقة.

## بطاقةUNIT30.4 — معتمدة23أكتوبر

المواصفة15§15 وقرار08/23أكتوبر، الموضع14. LOCALواحدبBASEحديثوملكيةملفاتونطاقودليلواجهةالمالك. اقرأAGENTS/docs01/11/13/17/18المتأثرةو08/10/11/14/15؛ احترمMVC/SQLModels/CSP/ar-en/RTL/mobile/a11y. قبلpatch: جردوظائفالأزراروحاوياتfullscreen، ومصدرgradient، وend/rating/winner/مدةالخادم/الاكتشافوالـcursor. لا يستبدلstartبـpublishأويجعلbonusأصواتًابشريةأويخلطqualityالمنافسةبتقييمالخصم.
REMOTEعلىexactHEADيفحص15§15.6:299.999/300/300.001حسبدقةالساعة، retry/race/end/autofinish، الرصيدوالفائزatomic مرةواحدة، حفظقواعدالمشاهدبعد5دقائق، طبقتيالترتيب/filters/cursorوالبحثالمباشر؛ثمfullscreen/exit/mobile/ألوانفيقبولواحد30–30.4. WORKLOG/PLAN-STATUSفيPRصادقتان؛لاادعاءPRODACCEPTEDمنT/B. لا تكليفمكرر/مساسبالـ28المغلقة، ولاوظائفرسائل31أوUX35خارجالألوانالمحددة.

**ملحق 24 أكتوبر على بطاقة 30.4 (معتمد بدمج PLAN PR #43؛ التكليف بعد مراجعة القائد التقني):** المواصفة 15§§15.7–15.9 وقرار 08/24أكتوبر. يضيف على نفس LOCAL/REMOTE والبوابة: تنافي زرّي بدء البث وإنهاء المنافسة (الإنهاء = إنهاء المنافسة كاملة بلا تغيير وظيفة، بلا زر إيقاف نشر جديد) وفق حالة النشر الفعلية، وحالات المربع الكبير/الصغير الأربع (معاينة الكاميرا المحلية أو صورة الملف قبل وصول فيديو الخصم) من وصول الفيديو الفعلي، مع أسبقية حالة نهاية الخادم (15.8.4). قبل patch يجرد LOCAL أسماء الأزرار والحالات والإشارات الفعلية (مصدر حقيقة الزر، إشارة وصول فيديو الخصم، أي swap/expand يدوي). لا إعادة بناء P2P/التسجيل/lease؛ لا مسار خروج جديد ولا تغيير مسار قائم. REMOTE يختبر A-01..A-13 وB-01..B-12 وM-01 على exactHEAD؛ M-02 (لمس حقيقي) في البوابة المجمعة وإلا NOT TESTED. لا يُدّعى PASS لجهاز لم يُنفَّذ.
