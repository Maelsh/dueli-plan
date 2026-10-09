# Dueli — قوالب التكليف ومراجع الوحدات

**الترتيب والحالة وNEXT حصريًا في[14](14-UNIFIED-EXECUTION-PATH.md).** لا يصدر LOCAL لوحدة غير مدرجة فيه أو PR لها نشطة. أرقام الصفوف للعرض فقط؛UNIT ثابت.

## مواصفات الوحدات

| المجال | المرجع |
|---|---|
|العقود السابقة R2/R3|05،08،11؛ الحالة في14؛ لا تعاد|
|الرسائل/الحفظ/Home/DB/UX/cleanup/الإدارة|12 §§3/4/10.1–10.3، والتتبع في14 §§2/3|
|signaling/chunks/التنزيل/صفحة المنافسة|13 §§2–5؛ ترتيب14|
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
