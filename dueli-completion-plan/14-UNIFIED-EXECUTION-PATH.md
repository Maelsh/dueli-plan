# Dueli — المسار التنفيذي الواحد حتى إطلاق الويب

**اعتماد المالك: 2026-10-09 — طلب مسار واحد وحفظ جميع البنود عند إعادة ترتيبها.**
هذا هو المصدر الوحيد **لترتيب العمل وحالته وNEXT**. 08 للقرارات، 11 لأوزان H7 المعتمدة، 10 للدمج والإصدار، 05/12/13/15 للمواصفات. 04 بوابة استئناف تشير إلى هذا المسار، وليست جدولًا منافسًا له.

## الحالة المعتمدة الأحدث — 2026-10-27 / UNIT32.2 + REM1 + UNIT32.3 test closure مدمجة؛ NEXT=UNIT33 (لم يبدأ تكليفها)

- **CODE MAIN / actual merge SHA:** 8e10cdc3ec1f5f2dd1c225feee88ab7d225411cd (PR #144 / UNIT32.3 candidate — test/evidence only). BASE bfa09aa57c38b59b7f55a5168dcd44ae41d6edb7؛ independently approved HEAD 1ebc73dc61c0c2eef74a06864de4f536384c794f.
- **Post-merge Quality Gate #392:** [run 40553795307](https://github.com/Maelsh/dueli-opus/actions/runs/40553795307) SUCCESS on exact merge SHA؛ 2122 tests passed, 1 skipped؛ G2 لم يزد فوق baseline 310؛ route inventory بقي252.
- **Deploy to Cloudflare Pages #621:** [run 40553795266](https://github.com/Maelsh/dueli-opus/actions/runs/40553795266) SUCCESS on the same SHA. Build, production bindings, read-only production schema collection, fail-closed release readiness, and actual production deploy succeeded. No migration was applied.
- **UNIT32.3 — R4-ACCOUNT-COMP-LIFECYCLE-EDGE-1 = CLOSED / TEST-EVIDENCE FOLLOW-UP.** PR #144 adds 9 focused tests (5 delete-title/confirmation/Load More markup; 4 settings-password loading). No production code, API, schema, route, or dependency change. Two independent REMOTE reviewers approved exact HEAD 1ebc73dc61c0c2eef74a06864de4f536384c794f.
- **Accepted evidence limits (do not overclaim):** the Load More test asserts appended markup but does not invoke confirmation/delete through the appended button; confirmation/cancel/DELETE are exercised through the shared handler from an SSR card. The harness uses a simplified card renderer, so these tests do not constitute full injection coverage for the production shared card renderer. The independent reviewers found no blocking gap within this scoped test-closure PR; no extra follow-up has been opened.
- **Settings loading:** SSR spinner-only, delayed settings GET, local-password/OAuth-only final states, and no password API call before the form is rendered are covered by the new tests.
- **Release state:** CODE DONE / DEPLOYED, but no manual browser/device/screen-reader/IME acceptance; do not record PROD VERIFIED.
- **Plan classification:** UNIT32.3 is a bounded subtask for test/evidence closure within row32.2, not an additional top-level UNIT. Total remains **58 UNIT**; IDs33–43 and their order remain unchanged. PR #110 remains out of scope.
- **Canonical NEXT remains UNIT33 / R4-HOME-UX-1**, but its execution prompt is deliberately not issued in this window; the owner will resume it in the next conversation.
- **PLAN BASE before this update:** f8e8fbbd6ab8a271f72dfb1f3b6c6e7cb69cd2ca.
### لقطة تاريخية — 2026-10-26 / Gate 30–30.6 مغلقة وUNIT31 مدمجة؛ NEXT وقتها UNIT32 (استبدلت في27أكتوبر)

- **CODE MAIN / actual merge SHA:** `3cee6e78ce0750536c474131363f80902b886c7d` (PR #139 / UNIT31). Merge parents: BASE `70ce057f34fc7c3e39506ee6c9e98ddb917d85fc` + independently approved HEAD `da437d6cc8ecee5c9e1fc600826f1fe89bb76ee3`.
- **Post-merge Quality Gate #378:** [run 40371372964](https://github.com/Maelsh/dueli-opus/actions/runs/40371372964) SUCCESS on the exact merge SHA. **Deploy to Cloudflare Pages #607:** [run 40371372929](https://github.com/Maelsh/dueli-opus/actions/runs/40371372929) SUCCESS on the same SHA; production bindings, read-only schema collection, and release-readiness checks passed, then the production deploy step succeeded. No migration was applied.
- **UNIT31 / R4-MESSAGES-1 — CODE DONE / DEPLOYED.** PR #139 merged after two independent REMOTE APPROVEs of exact HEAD `da437d6...`. M-01..M-05 PASS within reviewed scope; F-1 is closed with the new RED→GREEN regression test (previous `347e610` fails the history-read assertion; approved head passes). Actual production deployment is confirmed by Deploy #607 on this merge SHA.
- **Acceptance limits / not claimed:** no manual production/browser/device click-through, physical IME keyboard test, or live SSE-refresh test was performed; therefore do **not** record `PROD VERIFIED`. A profile `?user=` target outside the newest 100 can still open a named compose state before first send; both REMOTE reviewers classified this pre-open pagination boundary as a non-blocking future enhancement. No new API, migration, or schema change was added. PR #110 remains out of scope.
- **GATE 30–30.6 = ACCEPTED / CLOSED**; previous D-01/D-02 production evidence and untested branches remain as recorded below.
- **NEXT وقتها: UNIT32 / R4-PROFILE-SAVE-1**; أصبح NEXT الحالي UNIT32.1 بعد دمج UNIT32 ونشرها. Total plan remains 57 UNIT; no reordering or renumbering. PR110 must not be touched/merged.
- **PLAN BASE before this status update:** `db1e5f06d0747834e81d54fd1343be8ec51584eb`. This snapshot is historical; the newer 2026-10-27 state at the top is authoritative.

### سجل22أكتوبر — إغلاقUNIT28 (تاريخي؛ NEXT30 فيه استُكمل)


**UNIT28 ACCEPTED — 2026-10-22 (OWNER APPROVED / PRODUCTION VERIFIED).** CODE MAIN `a2579ce5f1f0d32077506b56553fe9a0f79619f8`; PR125/126/127 MERGED. Post-merge [Quality 39662569083](https://github.com/Maelsh/dueli-opus/actions/runs/39662569083) SUCCESS and [Deploy 39662569170](https://github.com/Maelsh/dueli-opus/actions/runs/39662569170) SUCCESS on exact SHA. Independent real-browser production acceptance: new competition **2253**, three authenticated contexts, two media sources, End while publishing, finalized 11/11 inline snapshot → verified tail 12 chunks / 134.554s, bounded automatic refresh, no reload/playback reset, duration/seekbar updated, polling stopped. Report: `A28-PR127-PRODUCTION-ACCEPTANCE-REPORT.md` (2026-10-22; owner-provided acceptance artifact). Earlier PR125/126 and competitions 2243/2244/2250/2251 remain historical evidence. A28-LEASE/SURFACE/TIME and 28.1–28.5 including children closed within tested scope. No re-test of accepted work without a new independently evidenced defect. **NEXT: UNIT30 R4-CHUNK-DOWNLOAD-1, option B**; PR110 remains OPEN/HOLD and must not be merged; inventory reusable work before clean replacement PR. Preserve 30.1→30.2→30.3→31→32→32.1→33–42, all 54 units and existing DoD.

> لقطة22أكتوبر تاريخية: أُنجزكود30–30.3، وNEXTالحالي30.4والقبولالمجمعحسبلقطة23أكتوبر أعلاه.

## أين نحن وكم بقي؟

- **تم:** Gate30–30.6 مغلقة؛ UNIT31 و32 و32.1 و32.2/REM1 وUNIT32.3 (متابعة اختبار/دليل) مدمجة ومنشورة. آخر merge SHA: 8e10cdc3ec1f5f2dd1c225feee88ab7d225411cd؛ Quality #392 40553795307 وDeploy #621 40553795266 SUCCESS على SHA نفسه؛ 2122 passed / 1 skipped.
- **الحالة الحالية:** A–E للوحدة32.2 مغلقة عبر PR #143، وملاحظتا UNIT32.3 أُغلقتا باختبارات فقط عبر PR #144 بعد موافقتين مستقلتين. لا migration أو dependency أو product-code change؛ لا قبول يدوي شامل ولا PROD VERIFIED. حدود الاختبار المقبولة موثقة أعلى الملف وفي13.
- **التالي المخطط فقط:** UNIT33 / R4-HOME-UX-1، ثم33.1 →34–42. لم يبدأ تكليف UNIT33 في هذه النافذة. إجمالي الخطة58 UNIT؛ IDs33–43 ثابتة.
- **بعد الويب:**43/R5، لا يحجب البيتا. PR110 خارج النطاق ولا يدمج.

## 1. لقطة المطابقة الحالية — 2026-10-21

- CODE MAIN `d0768783ede68c11aab9cc442c148d99349fead3`؛ PLAN BASE `d9744c8ce1ee06ac8f0503f56bf792891f88d0d4`.
- PR122/28.3.1 MERGED إلى`54a3380a3c2c06319d48b2be2f953134bba2302d`؛ PR123/28.4.1 إلى`a422f776381a91349e8e2b111dbe92734ed3e89a`؛ PR124/28.5 إلىMAIN الحالي.
- [Quality39551641343](https://github.com/Maelsh/dueli-opus/actions/runs/39551641343) و[Deploy39551641346](https://github.com/Maelsh/dueli-opus/actions/runs/39551641346) SUCCESS لنفسMAIN. WORKLOG/PLAN-STATUS المحلية القديمة تاريخ لاحالةدمج حالية.
- تجربة2242: نشرصريح/P2P/تسجيلمصدرين/LIVE وVODللمشاهد/حدثنهاية وإشعارات نجحت في حدودالتقرير؛ قبول28 NOT ACCEPTED. A28-LEASE/SURFACE/TIME متبقية؛SCREEN BLOCKED/PREVIEW OBS وتوقفخصمنشطعندend محفوظةبحدودها في15§14.
- **NEXT حزمةمتابعة قبول28**، بLOCALواحد ثمREMOTEمستقل؛ ترتيبها الداخليLEASE→SURFACE→TIME، لاوحدةجديدة ولا إعادة122–124. حدودالمتابعة والاختباراتقبل/بعد في15§14؛ بعدإغلاقالمتبقي قبول28 ثم30 وكلالمسارالمحفوظ.
- PR110 OPEN/HOLD كماهي؛ لا تنزيل30 أوNaN35 الآن. جميع54UNIT محفوظة؛ سجل§6 يوضحجمعالمتبقي دونإزاحةأيصف.

### لقطة2026-10-20 التاريخية — لا يستأنف منNEXT قديمة

- CODE MAIN `38ffa575e34d6912818f1ebc9e0a1a761d110da4`؛ PLAN BASE `c1ade66f863afb24937bf9e981536d33b62e8702`.
- PR120/28.3.1 MERGED إلى`2abf5ade279804d1ec07a4ece22cbf810b4c50ba`؛ PR121/28.4.1 MERGED إلىMAIN أعلاه. [Quality39416835180](https://github.com/Maelsh/dueli-opus/actions/runs/39416835180) و[Deploy39416835145](https://github.com/Maelsh/dueli-opus/actions/runs/39416835145) SUCCESS لنفسMAIN؛ لاqueued قديمة كحالةحالية.
- FV2230 واستكماله وصور15/16/23/24/25 معتمدة لتحديد المتابعة؛15§13 مصدر التصحيحات ومصفوفة التحقق قبل/بعد ومسؤولLOCAL/REMOTE وS الضرورية. لا نطلب تجربةتشخيصثالثة قبلالإصلاح.
- NEXT متابعة28.3.1 نفسها للنشر/الإشارة/replay، ثم متابعة28.4.1 نفسها للزمن، ثم28.5 القائمة؛ لاUNIT جديدة أوإعادةدمج120/121. كل54UNIT السابقة وDoD محفوظة.
- PR110 ما زالتOPEN/HOLD بنفسHEAD؛30 بالخيارB. لا تغييرH7 أوKEEP NOW أوDB أوالاستضافة.

### لقطة2026-10-19 التاريخية — لا يستأنف منNEXT قديمة

- CODE MAIN `ce5e0e728dfbac59f3cd1f4e15508e2c374fe6fe`؛ PLAN BASE `1a69fcd93c8e389075c6293502f0dfcd36468a70`.
- PR118 MERGED إلى`dcb56c707dd1d9dd06e7f1c1d9a157a427c0ca18`، وPR119 MERGED إلىMAIN الحالي. [Quality38733693451](https://github.com/Maelsh/dueli-opus/actions/runs/38733693451) و[Deploy38733693448](https://github.com/Maelsh/dueli-opus/actions/runs/38733693448) SUCCESS لنفسMAIN.
- PR119 أصلحت الانتظار عندfinalized دون مقاطع قابلة للتشغيل؛ لا تعني قبول كامل البث. WORKLOG/PLAN-STATUS قبل الدمج تاريخ محفوظ يحتاج إضافة تحديث الحالة الفعلية من قائد التنفيذ؛ لا إزالة التاريخ أوتسميةS PENDING قبولًا.
- تقرير المالك عن منافستين وصور15أكتوبر ثم موافقته19أكتوبر هو مصدر متابعة محددة. فحص المخطط الكود وعينة من الصور، لا جميع الصور ولا وسائط أوD1 إنتاجية مستقلة.
- قرار08 الأحدث ومواصفة15§12 يحفظان O19-01..21 وخصوصية§11؛ تحقق العرض والسبب قبلpatch. أدوات البث بأشكال وألوان صفحات الاختبار المحفوظة، لا تصميم بديل من الوكيل.
- PR110 OPEN/HOLD HEAD`6e7ca1039484980affbcaf6f0eab548a82c35d17`؛ التنزيل30 بالخيارB باقٍ، والتوافق اللازم للبث فقط يقدم إلى28.3.1/28.5.
- قوائم «المشاهدة لاحقًا» وسجل المشاهدات داخل بروفايل صاحبه مطلوبة قبل البيتا في32.1؛ لا خلط مع تذكير الموعد35. SEC07/08 وH7 وKEEP NOW والقبول41/42 محفوظة.

## 2. الطريق الكامل

| الترتيب | UNIT / المحطة | أين كنا / ماذا ننجز؟ | الحالة الحالية والدليل / شرط الخروج |
|---:|---|---|---|
| 01 | HIST-CORE | Beta Core والبنية الأساسية | CLOSED وفق قرار المالك وسجل الكود؛ لا إعادة بوابات |
| 02 | HIST-FOUNDATION | Foundation وMVC وSQL وتوحيد الوثائق | CLOSED وفق السجل والمالك؛ لا تنظيف شامل جديد |
| 03 | HIST-LIVE | Phase7 وP2P وTURN والخوادم وصفحات الاختبار | CLOSED في نطاقها السابق؛ ربط غرفة الإنتاج في24 لا يعيد هذه البوابة |
| 04 | HIST-FINANCE | الدفتر والأرباح وStripe والسحب والتبرعات والشفافية | CLOSED وفق WORKLOG/PLAN-STATUS والمالك؛ لا إعادة تحقق مالي |
| 05 | HIST-ADS-SECURITY | الإعلان والمعالجة الأمنية والتشغيلية اللاحقة | CLOSED وفق السجل والمالك؛ الملاحظات الأمنية القديمة تقرأ مع إغلاقاتها اللاحقة |
| 06 | R1 | إصلاحات الواجهات السابقة | CLOSED بتأكيد المالك؛ PR59–74؛ العيب المحدد اللاحق يعالج وحده |
| 07 | R3-B7 | جلسات Explore وcursor والاستمرار حتى النفاد | CODE DONE / DEPLOYED #75؛ بنية يعاد استخدامها |
| 08 | R3-GUEST-1 | استمرار Suggested للزائر | DONE #76 وقبول المالك مثبت؛ لا سقف15 نهائي |
| 09 | R2-AUTH-1 / EMAIL-DOMAIN | استعادة كلمة المرور وهوية البريد | CODE DONE #77/#78؛ تحقيق Inbox مؤجل بقرار المالك |
| 10 | DEPLOY-RECOVERY / EMAIL-UX | استعادة النشر وإرشاد Spam وتحقيق Home | CODE DONE #79/#80؛ UX ليس إصلاح deliverability |
| 11 | R-RELEASE-1 / R3-RAILS-1A/1B / MAINT | سلامة الإصدار واستمرار كل rails ثم معالجة الإصدار | CODE DONE / DEPLOYED #81–84 بعد remediation؛ حادث0033 عولج وفق السجل |
| 12 | R2-J | الدعوة والطلب والقبول والخصم الواحد | CODE DONE / DEPLOYED #85؛ معالجة N-03 لاحقًا في#106 لا تعيد J |
| 13 | R3-EXPLORE-CONTEXT-1 | View All والفرع والحالة وURL/session | CODE DONE / DEPLOYED #86 |
| 14 | R2-L1 / RELEASE-0034 | التعليقات والحضور والمشاهدة المؤهلة | CODE DONE / DEPLOYED #87–89؛ معالجة manifest/collector محفوظة |
| 15 | R2-V | 300s والتعديل والنتيجة وcutoff | CODE DONE / DEPLOYED #90؛ قبول الوسائط منفصل |
| 16 | R2-L2 | روابط غرفة الإنتاج وحالات الوسائط والتفاعل والتعليقات والإعلان | CODE DONE / DEPLOYED #91 ضمن نطاقه؛ S مؤجلة، وتكامل signaling/chunks/صفحة المنافسة قبوله المتبقي المستهدف في27–30/41 |
| 17 | R2-A | هوية الإدارة والحساب والأدوار ووثائق H9 | CODE DONE / DEPLOYED #92؛ الوصول الفعلي وقبول الرد وملاحظة stats في36/40 |
| 18 | R2-M | رسائل شخصية ونظام دعم إداري مستقل | CODE DONE / DEPLOYED #93؛ عيوب compose/mobile/history/read المرصودة في31 |
| 19 | R2-P | طرق الصرف المحفوظة وsnapshot | CODE DONE / DEPLOYED #94؛ البنك الحقيقي في40 |
| 20 | R2-F | بقية الرحلات الأصلية والإشراف والتبرع والمعلن | CODE DONE / DEPLOYED #95؛ لا يعد قبولًا لكل عيب استخدام اكتشف بعده |
| 21 | R3-D0/D1/D2 / D1-REM1 | اعتماد وتنفيذ H7 والبحث والمشابهات والمطابقة وProfile | DOCS APPROVED ثم CODE DONE / DEPLOYED #96–98؛ لا إعادة أوزان |
| 22 | R3-C1/C2/C3 / D1-BIND-HOTFIX | المساعدة والوثائق المدارة وتصميم التخليقي وحد100 binds | CODE/DOCS DONE / DEPLOYED #99–102؛ C3 تصميم فقط وKEEP NOW؛ GUIDE توسعة في38/39 |
| 23 | R4-TITLE / DB-DIAG/OPT / COLLECTOR / EVENTS | title، تشخيص وفهارس0039، إصلاح النشر، receiver/star/read/link/cascade | CODE DONE / DEPLOYED #103–106؛ DB-01 لا يغلق بالفهارس، cleanup غير مثبت التنفيذ:34/37 |
| 24 | R4-LIVE-INT-1 | عميل signaling مشترك صحيح بدل legacy | CLOSED / CODE DONE / DEPLOYED PR107؛ قبول A/B موثق في REMOTE؛ لا إعادة Phase7 |
| 25 | R4-CHUNK-PLAY-1 | استقبال الجمهور أثناء البث وبعده، القائمة والاستئناف والنهاية | CLOSED / CODE DONE / DEPLOYED PR108؛ T/B APPROVE مستقل، MEDIA S PASS مستقل لدى REMOTE الثاني (الأول BLOCKED بيئيًا)؛ actual-main Quality/Deploy SUCCESS على `8f3d194`؛13 §5 |
| 26 | R4-COMP-UNIFIED-1 | صفحة competition الموحدة لجميع الأدوار والحالات | CODE DONE / DEPLOYED PR109؛ actual-main Quality/Deploy SUCCESS على216e4b5؛ لا إعادة الوحدة؛ تحسينات مثبتة في27–30 |
| 27 | R4-CHUNK-INDEX-1 | DB metadata والقائمة والتوقيت والنهاية | CODE MERGED / DEPLOYED ضمنMAIN130e18b؛0041appliedحسبLOCAL؛لاLOCALمكرر؛قبولرحلةالتسجيلالمتبقي41 |
| **28** | **R4-CHUNK-UPLOAD-SAFE-1** | **كود الرفع وقبول رحلة البث؛ حزمة المتابعة الموحدة** | **ACCEPTED 2026-10-22؛ PR125/126/127؛ إنتاج2253؛** كودSAFE والتابعات محفوظ؛ A28-LEASE→SURFACE→TIME منمتبقي28/28.4.1/28.5 بملكيةواحدة؛15§14 قبل/بعد والقبولالمحدود؛ لا UNIT أوPRلكلعيب |
| 28.1 | R4-RELEASE-RECOVERY-C | استعادة الإصدار وmanifest/raw hash/lease/runbook | CODE DONE / DEPLOYED #114؛ تطبيق الهجرات بحسب LOCAL السابق؛ تحديثات116/117 محفوظة؛ لا عودة لحوادث مغلقة |
| 28.2 | R4-PROFILE-SEC11-1 | إزالة session query token وlegacy cookie في Profile | PR115 MERGED / CODE DEPLOYED؛ إصلاح منجز في نطاقه؛ بقية القراء في SEC07/30.1، لا مراجعة Auth كاملة |
| 28.3 | R4-LIVE-ENTRY-RECOVERY-1 | الاستعداد والنشر الصريح والتفاوض | PR118 CODE MERGED / DEPLOYED إلىdcb56c7؛ S غير مقبولة بعد؛ متابعة محددة28.3.1 دون إعادةPR أوPhase7؛ 15 §§11/12 |
| 28.3.1 | R4-LIVE-ENTRY-RECOVERY-REM1 | نشر/إشارة/replay مع حفظ الخصوصية والأدوات | PR120/122 CODE MERGED/DEPLOYED؛ نتائجSIG/TOAST/OFFER/REPLAY/PAIR في2242 محفوظة؛ متابعةpreview/screen وفق15§14 وحدودها، بلا تكليفإشارةمكرر أوإغلاقكلالقبول |
| 28.4 | R4-CHUNK-VIEW-RECOVERY-1 | خط المقاطع وready/playlist ونهاية الانتظار الفارغ | PR119 CODE MERGED / DEPLOYED إلىce5e0e7؛ قبول إنتاجي غير مكتمل؛ الإصلاح محفوظ والمتابعة28.4.1؛ 15 §§11/12 |
| 28.4.1 | R4-CHUNK-VIEW-RECOVERY-REM1 | زمن كامل وربط المشغل ونافذة التحميل | PR121/123 CODE MERGED/DEPLOYED؛ TIME الجاريFAIL في2242، START/total/window PASS بحدودها؛ A28-TIME فيحزمة28 وفق15§14؛ O19/DoD السابقةمحفوظة |
| 28.5 | R4-LIVE-END-RECOVERY-1 | النهاية وتحديث الحالات وانتقال الجميع للتسجيل | PR124 CODE MERGED/DEPLOYED؛ الحدثوصل/أجهزةالحالةالمجربةحررت، لكنSURFACE للمنافسينFAIL؛ تكملةA28-SURFACE واختبارendمعخصمنشط ضمنحزمة28،15§14؛ FINAL/resume/DoD القديمة محفوظة |
| 29 | R4-CHUNK-PLAYER-UX-1 | latest-ready/rewind/live edge/windowed VOD | PR113 CODE MERGED / DEPLOYED محفوظة؛ عيب ربط الزمن/الطلب المثبت يعالج في28.4.1، دون إعادة الوحدة أوقبولS مناختبارModel؛ 15§12 |
| 30 | R4-CHUNK-DOWNLOAD-1 | MP4 صالح وخدمة تنزيل مستقلة / الخيارB | PR129 MERGED/DEPLOYED إلى886026f9؛ PRODUCTION ACCEPTANCE PENDING فيالبوابةالمجمعةبعد30.4؛ كلDoD15§§6/10/12.6 محفوظة وPR110لايدمج |
| 30.1 | R4-SESSION-KEY-SEC07-1 | توحيد قراءة الجلسة وإزالةsession_id القديمة | PR130 MERGED/DEPLOYED إلىd12b7065؛ القبولالمجمع30–30.4 معلق؛15§10 وDoD السابقةمحفوظة |
| 30.2 | R4-SESSION-HTTPONLY-SEC08-1 | جلسةويبHttpOnly بدلlocalStorage/JS token | PR131 MERGED/DEPLOYED إلى312af270؛ القبولالمجمعمعلق؛ login/OAuth/CSRF/logout/SSE/signaling/upload وفق15§10 محفوظة |
| 30.3 | R4-SEC-GUARDS-DOCS-1 | حراس05/10 وحالةالوثائق | PR132 MERGED/DEPLOYED إلى85eec139؛ القبولالمجمعمعلق؛ لاCORSrebuild أوWebSocket جديد، DoD15§10 محفوظة |
| **30.4 / 30.5** | **R4-COMP-CONTROLS-EARLY-END-1 + settlement response guard** | **UNIT30.4 + UNIT30.5; PR #133–#137 merged** | **CODE MERGED**: #133 `4c3d960`; #134 `ca78323`; #135 `251da45`; #136 `a6d9dea`; #137 `20109dd5`. ID-19 APPROVED VIA T/B. Gate 30 successful evidence preserved; no broad retest. Post-merge Quality/Deploy and production acceptance are recorded in the current combined Gate 30–30.6 closure above. |
| **30.6** | **R4-COMP-ACCEPT-ZEROCHUNK-1** | **D-01 invitation acceptance 500; D-02 completed competition with 0 chunks and indefinite player wait** | **ACCEPTED / CLOSED 2026-10-26**: PR #138 merged at 70ce057f34fc7c3e39506ee6c9e98ddb917d85fc; post-merge Quality #374 (40313355068) and Deploy #603 (40313355093) SUCCESS on exact merge SHA; production deployment confirmed. D-01 and D-02 both PASS in production per owner acceptance report. UI duplicate-409, scheduled-conflict UI, active lease drain and upstream-invalid/no-DB remain NOT TESTED in production. Gate 30–30.6 CLOSED; at closure NEXT was UNIT31 (now complete), and current NEXT is UNIT32. D-03 remains UNIT35. |
| 31 | R4-MESSAGES-1 | Compose والتاريخ والاسم والعرض الفوري والترتيب وEnter والقراءة والهاتف | **CODE DONE / DEPLOYED 2026-10-26**؛ PR #139 merge SHA `3cee6e78ce0750536c474131363f80902b886c7d`؛ Quality #378 `40371372964` وDeploy #607 `40371372929` SUCCESS على SHA الدمج نفسه؛ M-01..M-05 PASS؛ F-1 مغلق بـRED→GREEN؛ ما قبل الإرسال خارج أحدث100 تحسين غير مانع لاحق؛ قبول يدوي/IME/SSE وPROD VERIFIED غير مدعى |
| 32 | R4-PROFILE-SAVE-1 | حفظ display_name/bio صادق | **CODE DONE / DEPLOYED 2026-10-27**؛ PR #140؛ approved HEAD `05bbfffc43bd58394798fc2a917f1002bbb783c5`؛ merge SHA `05f0f1f84c50a13be36b6d2111a628e14985d039`؛ Quality #381 `40422901712` وDeploy #610 `40422901631` SUCCESS على SHA نفسه؛ 2069 passed / 1 skipped؛ بلا schema/migration/route changes؛ PROD VERIFIED غير مدعى |
| 32.1 | R4-PROFILE-COLLECTIONS-1 | المشاهدة لاحقًا وسجل المشاهدات في قسم خاص داخل بروفايل صاحبه | **CODE DONE / DEPLOYED 2026-10-27**؛ PR #141؛ approved HEAD `b75c52beab12e0b06718bf71e0022352468600dd`؛ merge SHA `3b1b6b64914cbfc861e00063643431c60539a284`؛ Quality #384 `40498659504` وDeploy #613 `40498659503` SUCCESS على SHA نفسه؛ 2094 passed / 1 skipped؛ G2=300≤310؛ 251 route؛ no migration؛ known P3/non-manual acceptance documented; لا PROD VERIFIED |
| 32.2 | R4-ACCOUNT-COMP-LIFECYCLE-1 + REM1 | واجهة تغيير كلمة المرور، حذف المنافسة المؤهلة، وإصلاحات A–E | CODE DONE / DEPLOYED؛ PR #142 merge 603d826834e3f8490caff3a67db854fb6eedb647 ثم PR #143 merge bfa09aa57c38b59b7f55a5168dcd44ae41d6edb7؛ Quality #390 [40535579267](https://github.com/Maelsh/dueli-opus/actions/runs/40535579267) وDeploy #619 [40535579164](https://github.com/Maelsh/dueli-opus/actions/runs/40535579164) SUCCESS؛ 2113 passed / 1 skipped؛ G2=300≤310؛ route inventory252؛ no migration. |
| 32.3 | R4-ACCOUNT-COMP-LIFECYCLE-EDGE-1 — test/evidence closure only | التحقق من title/delete-confirm ومسار كلمة المرور أثناء تحميل الإعدادات | CLOSED / DEPLOYED؛ PR #144 approved HEAD 1ebc73dc61c0c2eef74a06864de4f536384c794f، merge SHA 8e10cdc3ec1f5f2dd1c225feee88ab7d225411cd؛ Quality #392 [40553795307](https://github.com/Maelsh/dueli-opus/actions/runs/40553795307) وDeploy #621 [40553795266](https://github.com/Maelsh/dueli-opus/actions/runs/40553795266) SUCCESS على SHA نفسه؛ 2122 passed / 1 skipped؛ 9 اختبارات جديدة؛ لا تغيير منتج. حدود التغطية المقبولة في13§UNIT32.3. Subtask ضمن32.2؛ لا يغيّر إجمالي58 UNIT. PROD VERIFIED غير مدعى. |
| 33 | R4-HOME-UX-1 | رسم كل rail عند جاهزيته مع loading/retry ومنع الطلب والرسم القديم المكرر | CODE DONE / MERGED + DEPLOYED؛ PR #145 merge SHA `20c16dc7bbda3af1aa3b0597f0f147a59c44b1c4`; Quality Gate [40599735765](https://github.com/Maelsh/dueli-opus/actions/runs/40599735765) SUCCESS وDeploy [40599735788](https://github.com/Maelsh/dueli-opus/actions/runs/40599735788) SUCCESS على SHA نفسه. UNIT33.1 كذلك مدمجة ضمن PR #145؛ بلاغات القبول الحي 2026-10-28 مسجلة في08 وتقرير التخطيط؛ لا PROD VERIFIED شامل، ولا إعادة فتح تلقائية؛ لا يبدأ34 قبل توثيق الإغلاق وفق10 |
| 33.1 | R4-DEPS-SEC-1 | تحديث Hono/Zod، سجل الاعتماديات وبوابة npm audit مانعة | CODE DONE / MERGED + DEPLOYED ضمن PR #145؛ merge SHA `20c16dc7bbda3af1aa3b0597f0f147a59c44b1c4`; Quality Gate [40599735765](https://github.com/Maelsh/dueli-opus/actions/runs/40599735765) وDeploy [40599735788](https://github.com/Maelsh/dueli-opus/actions/runs/40599735788) SUCCESS على SHA نفسه. تحصين DUELI_AUDIT_CMD دفاعي اختياري غير حاجب؛ لا يعاد فتح PR لهذا السبب وحده. UNIT34 بعد توثيق الإغلاق؛ لا MySQL قبل البيتا |
| 34 | R4-DB-MEASURE-1 | إغلاق DB-01 بقياس فعلي قبل/بعد لـT0/continuation/search/SSE/notifications/chunk_index/playlist/seek (rowsRead/rowsWritten/executions + EXPLAIN)، requestId وstructured logging، وكاش عام معزول آمن واختبار degraded UI/retry على المعمارية الهجينة | PLANNED بعد إغلاق33 و33.1؛ مواصفة12 §§3/6 و15 §7 وقرار08 بتاريخ2026-10-27؛ تقرير رقمي لكل رحلة + ميزانية استهلاك يعتمدها المالك وقائد التخطيط قبل UNIT40؛ لا MySQL migration قبل البيتا؛ 58 UNIT ثابتة |
| 35 | R4-UX-I18N-1 | UX-STATE والترجمة والتذكير وحصيلة التقييم والإتاحة؛ I-01/FV20-SMALL وVIS-04 | PLANNED؛ 12/13 ومصفوفة34 موضعًا؛ O19-17/18 في15§12.7؛ I-01 يمنع mojibake وNaN% ويعرض «غير متاح / Unavailable» دون مساس H7؛ VIS-04 يضبط z-index/stacking context/overflow بين InvitePanel وinviteHoverCard وToast، ويبني public/static/styles.css بـnpm run build:css؛ اختبار AR/EN mobile/desktop؛ reminder يظل مستقلًا عن Watch Later |
| 36 | R4-ADMIN-ACCEPT-1 | قبول الدعم الإداري بحساب مخول، وتتبع ملاحظة stats500 | BLOCKED ACCESS / TARGETED؛ الجزء الإداري من MEDIA-ADMIN-ACCEPT؛12 وWORKLOG/R2-A؛ افحص /api/admin/stats موضعيًا، أصلح المتبقي إن ثبت أو ALREADY DONE بدليل؛ لا إعادة مالية/أدوار |
| 37 | R4-NOTIFY-CLEANUP-1 | تعليم الإشعارات القديمة مقروءة مرة واحدة | OWNER APPROVED / NOT EXECUTED EVIDENCED؛12 §10.2 وrunbook #106؛ cutoff2026-10-08T03:31:39Z، counts/schema/guard؛ لا إذن مكرر أو مساس رسائل/دعوات |
| 38 | R4-GUIDE-1 | مركز عن Dueli والمساعدة والتنقل وإدارة المحتوى | PLANNED؛13 §5 و15 §7؛ notice/versioned terms وsubscriber acceptance، إعادة استعمال C1/C2 والوثائق المدارة،8 أقسام، الروابط القديمة واللغة والأجزاء والصلاحيات |
| 39 | R4-GUIDE-2 | الرسالة والتقنيات ومساهمات AI والسياسات والتواصل والدعم | PLANNED + OWNER CONTENT APPROVAL داخلها؛13 §5 و15 §7؛ حقوق الطرفين ونص الشروط، محتوى موثق AR/EN، لا ادعاء وعي AI أو كيان قانوني أو قناة تبرع غير مثبتة |
| 40 | R0-LAUNCH-READINESS | إجراءات البنك والمزود والكيان إن لزم، الوصول الإداري، SEC-02، ومتطلبات الإطلاق الفعلية | OPEN / HUMAN؛08؛ طابق SEC-02 في `docs/12-SECURITY-REMEDIATION.md` مع أدلة تنفيذ المال الفعلية من8.A/8.D/#94؛ سجل لكل جزء evidenced/done/open ولا تعِد فتح المالي المغلق بلا عيب جديد. حسم جاهزية الإطلاق يظل قرارًا بشريًا؛ H9 محفوظة |
| 41 | R4-ACCEPT-REM-1 | قبول مجمع للرحلات الفاشلة والمعدلة والوسائط والتنزيل والميزانية | PLANNED بعد المعالجات؛12/13؛ T/B أولًا ثم S محددة؛ إذا شمل الإطلاق عمليات مالية، أضف withdrawal-path smoke test آمنًا ببيئة/حسابات اختبار غير إنتاجية: إنشاء الطلب والتحقق من الحالة والرصيد المعلق، ثم رفض/إلغاء أو الإكمال في بيئة اختبار مع idempotency؛ لا صرف حقيقي أو كتابة مالية على الإنتاج دون تفويض؛ طابق SEC-02 في `docs/12-SECURITY-REMEDIATION.md` مع نتائج المال السابقة. BLOCKED ليس PASS |
| 42 | R0-WEB-LAUNCH | عرض الجاهزية الموثقة ثم قرار المالك وإطلاق بيتا الويب | OWNER DECISION عند الجاهزية؛ لا قرار آلي أو ادعاء تشغيل دفع حقيقي دون البنك/المزود |
| 43 | R5 | PWA وAndroid وiOS وTV والتقنيات والتكلفة وقيود المتاجر | DEFERRED AFTER WEB؛ يعتمد المالك النطاق والترتيب لاحقًا |

**قاعدة السير الحالية:** 31 → 32 → 32.1 → 32.2 (CODE MERGED / DEPLOYED) → **قرار المالك بشأن ملاحظات المراجعة غير المسندة** → 33 → 33.1 → 34–42. لا تعتبر D-50 محققًا: حد50 يخالف شرط discoverability في13§9. بقية الملاحظات موثقة في12/13 ولم توزع على وحدة. العدد58؛ IDs33–43 ثابتة؛ PR110 خارج النطاق.

## 3. ضمان بقاء جميع العيوب

- **تحديث 2026-10-26:** D-01 وD-02 مسندان حصراً إلى UNIT30.6 وفق 15 §15.10؛ D-03 (NaN% / FV20-SMALL) يبقى في UNIT35 ولا يحجب Gate 30. تحفظ شواهد القبول الناجحة ولا تعاد.

| المصدر / المجموعة | أين تعالج أو تحفظ؟ |
|---|---|
| DB-01 وقراءات الصفوف والتكرار وT0 والبحث وSSE وتعطل الخدمة |33/34؛104/105 منجزة، لا وعد بسعة من EXPLAIN وحده |
| N-01/02/03/05/06/07 وreceiver/star/replay/cascade، بنود PDF الخاصة بالإشعارات |23/#106؛ لا إعادة الإصلاح؛ N-04 الخاص بعرض الحالة/اللغة إن بقي ففي35، cleanup37 |
| M-01/02/03/04/05 للرسائل الشخصية والإدارية |31؛ لا تخلط رقم M-4 في PDF الخاص بالعداد مع M-04 في سجل الخطة الخاص بالعرض الفوري وEnter |
| P-01 profile |32 |
| واجهة تغيير كلمة المرور + حذف المنافسة قبل انضمام خصم |32.2؛ لا تعِد #77؛ تأكيد نهائي وحارس ذري مع سباق قبول الدعوة |
| H-01 Home |33/34 |
| S-01/S-02 title/doubleescaping |23/#103؛ لا تكرار |
| I-01؛ U-01..U-05؛ VIS-01/02/03/04؛ DATA-01 |35 والموضع المتأثر25/26/31/33؛ I-01 يضمن UTF-8 وUnavailable بدل NaN؛ VIS-04 يختبر طبقات نافذة الدعوة وبطاقة التفاصيل وToast بعد بناء CSS؛ VIS-02 لم يتكرر في العينة الأحدث، لا تعديل CSS افتراضي؛ لا حذف demo أو مخالفة KEEP NOW |
| VOD-01/02، C-1 signaling، D-1 حقيقة التسجيل، انقطاع المضيف والاستئناف والنهاية والتنزيل، handoff107: finalize/drain/upload queue/sequence |24–30؛ لغة المشغل ضمن35؛ لا PASS من وجود vod_url |
| ADM-01/AUTH-OBS-01؛ ملاحظة /api/admin/stats من سجل الكود |36/40؛ حساب مخول خاص؛ لا username-login أو bootstrap إنتاجي بلا قرار |
| التقرير الأحدث: showToast16/fullscreen/namespaces/34 موضعًا/score/login/create/help/icons |35؛ مصفوفة13 §4 بكاملها |
| SEC-15 (نظافة الاعتماديات) وadvisories Hono GHSA-5r4p-p66f-jhc7 وZod GHSA-mrhx-c7xc-m3w5 وسجل 16 ثغرة audit (12 high/4 moderate؛ الإنتاج: hono وzod فقط) | 33.1 (18)؛ دفعات سلسلة البناء/الاختبار تبقى OPEN-TRACKED في سجل 33.1 ج؛ لا تسقط ولا تُنفذ بصمت |
| دليل Dueli ومساهمات AI والأقسام الثمانية |38/39؛ توسعة منتج معتمدة، لا إعادة C1/C2 |
| إجراءات المالك أو سياسة دائمة غير محسومة أو خدمة مدفوعة/نقل DB |40 أو الصف المتأثر مع OWNER DECISION؛ لا اعتماد آلي |

كل تفصيل في12/13 باقٍ؛ الجدول لا يسمح باعتبار المجموعة DONE من إصلاح عنصر واحد. يقفل القائد كل ID بدليل موضعي أو ALREADY DONE، أو يسجله OPEN/BLOCKED. ليست هذه دعوة لإعادة اختبار البوابات التاريخية.

### تغطية تقرير المالك19أكتوبر

التفصيل الكامل O19-01..21 في15§12.2، ولا يستبدل به ملخص قائد التنفيذ. O19-01..09/16 →28.3.1؛ O19-07/12/13/14/21 →28.4.1؛ O19-10/11/21 →28.5؛ O19-15 →30؛ O19-19/20 →32.1؛ O19-17/18 →35. الصلة المشتركة لا تفوض تنفيذين متداخلين.

## 4. مطابقة الخطة القديمة دون إسقاط أو إعادة تنفيذ

المجلد dueli-master-plan **تاريخي مستبدل، لا مرحلة سابقة مكتملة كليًا ولا مسار تكليف ثانٍ**. PR1 للخطة الحالية يثبت الانتقال إلى المتبقي؛ قرارات08/11 اللاحقة تستبدل المقترحات المتعارضة.

| أصل النطاق | المسار الحالي / معنى المطابقة |
|---|---|
| M0 القرارات والتشغيل |08 و10 و40/42؛ ما تم تشغيليًا مغلق وفق قرار المالك، وتبقى الإجراءات الفعلية |
| M1 أساس الواجهة |06/R1؛ S0-4 room/leave لم يثبت قبول تكامله في91 ويعالج24؛ لا إعادة R1 |
| M2 الرحلات والبث والاجتماعي والإدارة |12–20؛ النواقص المحددة في24–32/36/41؛ code-done لا يعادل قبول الوسائط |
| M3 الاكتشاف والسلوك والتخليقي |07/08/11/13/21/22؛ KEEP NOW استبدلت مقترح التقاعد التنفيذي؛ أداء وUX في33/34، لا إعادة H7 |
| M4 المال والإعلان |04/05/19/20 ثم40؛ البنك والمزود الفعليان يختلفان عن الواجهة |
| M5 المساعدة واللغة والقانون والرؤية |22/35/38/39/40؛ H9 تحدد إدخال المحتوى الحقيقي، لا اعتماد للنصوص المقترحة قديمًا |
| M6 القبول |41؛ قبول متبقٍ محدد للوسائط والواجهة؛ التدقيق الشامل المتكرر استبدل بقرار المالك T/B أولًا |
| M7 جاهزية الإنتاج |10 و11/14/23 ثم34/40/41/42؛ التشغيل التاريخي المغلق لا يعاد، وأي حاجب جديد يسجل |
| M8 المنصات |43/R5 بعد الويب |

المطابقة بحسب نطاق المراحل والأدلة الموجودة، **لا تزعم إثبات كل تفصيل قديم** أو تبني المقترحات القديمة كمتطلبات جديدة. إن وجد شرط معتمد بعينه لا يعرف مصيره، يربط بالدليل القائم أو بصف متبقٍ وفق§5؛ لا يحذف ولا يفترض DONE ولا يأمر بتدقيق شامل. الترخيص والوثائق القانونية المطلوبة ضمن40، والأدلة التشغيلية وrunbook الحالية في10/WORKLOG؛ المقترح القديم أو ما استبدله قرار ليس feature واجبة تلقائيًا.

## 5. محظور التخطيط خارج المسار — ملزم لكل مخطط وقائد

1. **ممنوع دمج أي تخطيط جديد أو موجه قابل للتنفيذ لا يندمج في هذا التسلسل.** لكل إضافة/إصلاح/تحقيق/قبول/قرار: UNIT ثابت، موضع عرض، مصدر، نطاق، تبعيات، حالة، DoD، ونوع تحقق T/B/S/H.
2. PR الخطة نفسه يعدل14، ومواصفة الوحدة، و08 عند قرار مالك جديد، و04 عند تغير لقطة الاستئناف. ملف ملحق وحده أو تعليق أو محادثة لا يفوض الانطلاق.
3. عند تقديم مهمة للأهمية: سجل الترتيب قبل→بعد والسبب وكل UNIT أزيح وموضعه الجديد؛ **يحظر سقوط أي بند مزاح أو إعادة إنشائه باسم مختلف**. الإلغاء/تقليص النطاق يحتاج قرار مالك صريح ومصدره؛ يبقى صف CANCELLED OWNER DECISION تاريخيًا.
4. لا يعاد ترقيم UNIT؛ يعاد ترقيم موضع العرض فقط. split/merge يربط الآباء والأبناء ويحفظ كل DoD/ID؛ المجموعات القديمة CLOSED لا تصبح OPEN لمجرد التنظيم.
5. قبل دمج خطة: مراجعة تغطية يدوية تقارن البنود قبل/بعد، والروابط والتبعيات وتضارب NEXT وإزاحة كل صف؛ ليست بوابة CI كود جديدة. توثق النتيجة في PR.
6. وحدة ACTIVE لها PR أو LOCAL/REMOTE قائم **تستكمل دون تكليف مكرر**. تغير الأولوية يحفظ PR/HEAD والمراجعة والحالة؛ حادث release يتبع10. المخطط لا ينفذ code.
7. بعد كل تقدم: يحدث القائد حالة الصف وروابط HEAD/PR/merge/run/SHA والقبول المتبقي. لا يسجل بنكًا أو دورًا أو كاميرا أو استهلاكًا DONE من وجود واجهة أو اختبار نصي.
8. كل handoff يشير إلى14 و04 و08 و10 و11 ومواصفة الصف؛ المحادثة ليست سجل العمل. لا NEXT منافس في ملف آخر.
9. الأصل T/B الأرخص؛ S للحكم الصوتي/البصري/الجهاز الذي لا يحسمه T/B؛ H للقرارات والإجراءات البشرية. لا يعاد المغلق ولا تضاف full suite بدون تغير أو فشل جديد مبرر.

## 6. سجل ترتيب المسار

### إغلاق تشغيلي UNIT32.2 — 2026-10-27 / قرار موضع مراجعات مفتوح

PR #142 merged at `603d826834e3f8490caff3a67db854fb6eedb647`; Quality #386 `40512334779` SUCCESS and Deploy #615 `40512334753` SUCCESS on the exact merge SHA. Unit code is deployed; reviewer findings were added to12 and13. Because the latest-50 owner competitions list conflicts with13§9's no-hard-cap discoverability criterion, the owner must disposition the follow-ups before this unit is represented as fully acceptance-closed and before issuing the next LOCAL prompt. The approved future route remains33→33.1→34→35–42; total58 UNIT, no renumbering.

### اعتماد المالك 2026-10-27 — إغلاق UNIT32.1 وإضافة UNIT32.2 وتوسعات 34/35/40/41

قبل: `NEXT=32.1`, 57 UNIT. بعد: PR #141 merged at `3b1b6b64914cbfc861e00063643431c60539a284`, Quality #384 `40498659504` and Deploy #613 `40498659503` SUCCESS on that exact merge SHA; `NEXT=32.2`, 58 UNIT. أضيفت وحدة واحدة بعد32.1 وقبل33 دون renumber أو حذف أي من33–43. أضيف VIS-04 إلى مواصفة35، requestId/structured error logging إلى34، وSEC-02/withdrawal smoke gate إلى40/41. مراجعات P3 وحدود عدم إجراء قبول يدوي محفوظة في اللقطة الحالية أعلاه. PLAN PR هذه توثيقية؛ لا تنفذ أي كود أو كتابة إنتاجية.

### قرار 2026-10-26 — تحديث المسار بعد قبول Gate 30 الجزئي
قبل: 56 UNIT، NEXT 30.4، قبول مجمع 30–30.4. بعد: **57 UNIT، NEXT 30.6، قبول مجمع 30–30.6**؛ لا إزاحة أو إعادة ترقيم 31–43. حُفظت شواهد Gate 30 الناجحة، وحُسم ID-19 عبر T/B، وأضيف D-01/D-02 إلى 30.6، بينما بقي D-03 في 35.

| التاريخ | التغيير | حفظ البنود المزاحة |
|---|---|---|
|2026-10-09|توحيد مصادر NEXT في هذا المسار؛ ACTIVE107 محفوظة؛ LIVE/CHUNK/COMP/DOWNLOAD ثم بقية الاستعادة وGUIDE والقبول|DB/MESSAGES/PROFILE/HOME/UX/ADMIN/cleanup/R0 بقيت في28–39؛ MEDIA وزعت24–27/33، وUX-STATE توسعت32؛ لا وحدة قديمة سقطت |
|2026-10-11|إغلاق الصفين24/25 بعد PR107/108؛ اعتماد MEDIA S من REMOTE الثاني؛ Quality/Deploy actual-main `8f3d194` ناجحتان؛ NEXT الصف26|لم تُزح أي وحدة ولم تتغير DoD للصفوف26–40|
|2026-10-09|فصل قياس DB-01 عن104 المغلق؛ DB-MEASURE متابعة DoD OPT؛ فصل cleanup والإدارة لإظهار الحالة|لا إعادة DIAG/0039/receiver/star؛ stats ملاحظة موثقة من#92 وليست إعادة مالية؛ لا بوابة تاريخية إضافية |

تحديث11أكتوبر الحالي: PR109 منجزة؛ NEXT27 INDEX؛ PR110 محفوظة في30 REMOTE REJECT. لقطةNEXT26 السابقة تاريخية.

### إعادة الترتيب المعتمدة — 2026-10-11

السبب: تقريرPR110 وقراراتالمالك ونصupload.php أثبتت أن الفهرس/الرفع/المشغل prerequisites مستقلة للتنزيل. القديم26COMP أُغلق109؛ القديم27DOWNLOAD→30 بنفسUNIT وPR110. الجديد27INDEX→28SAFE→29PLAYER يسبقها. [15](15-CHUNK-INDEX-UPLOAD-PLAYER-PLAN.md) مواصفةالعقودوالDoD والتحققوالحقوق؛ لا إعادةPhase7 أوH7.

| UNIT المحفوظة | قبل | بعد |
|---|---:|---:|
|R4-CHUNK-DOWNLOAD-1 / PR110|27|30|
|R4-MESSAGES-1|28|31|
|R4-PROFILE-SAVE-1|29|32|
|R4-HOME-UX-1|30|33|
|R4-DB-MEASURE-1|31|34|
|R4-UX-I18N-1|32|35|
|R4-ADMIN-ACCEPT-1|33|36|
|R4-NOTIFY-CLEANUP-1|34|37|
|R4-GUIDE-1|35|38|
|R4-GUIDE-2|36|39|
|R0-LAUNCH-READINESS|37|40|
|R4-ACCEPT-REM-1|38|41|
|R0-WEB-LAUNCH|39|42|
|R5|40|43|

التبعيات:27بعد26؛28بعد27؛29بعد27/28؛30بعد27–29؛41يشملmetadata/upload/playback/download والميزانيةوالحقوقضمنالرحلاتالمعدلة. كل شروط12/13 القديمةالمتوافقة باقية، وثلاث وحداتتضيف عقودًا لا تلغيclosed. GUIDE38/39 يحفظالشروطوقبولنسختها؛34يبقىقياسDB-01 وموضعمتابعةDBhosting المستقبلي، لاهجرةDB الآن.

### محاذاة حادث الإصدار — 2026-10-12 / مقترح مفتوح فقط

السبب: MAINd778090 mergedSAFEبmanifest0039 وفشلDeploy؛العقدالخارجيغيرمطابق؛Profilequerysessiontoken مثبتة. RecoveryC ترتبطبالأب28بالslot28.1؛Profilefixبالslot28.2. لا renumber للصف29/30 أو31–43. جميع43UNITالسابقةباقية، Recoverychild+securityfixاثنتان فقط؛لاgovernancecleanupمفوضة.

| القديم | الموضع الحالي | التصحيح |
|---|---|---|
|27 INDEX/PR111|27ثابت|MERGED،إثباتتطبيق/قبولproductionمتبقٍ|
|28 SAFE/PR112|28ثابت|MERGED/POST-MERGE BLOCKED،RecoveryCمعالجة28.1|
|29 PLAYER/PR113|29ثابت|OPEN،لاstashclaim،REMOTE/Sمتبقية|
|30 DOWNLOAD/PR110|30ثابت|OPEN/HOLD،عملمحفوظ|
|31–43جميعUNITs|31–43دونإزاحة|جميعDoDوالملاحظاتمحفوظة|
|ProfileSave القديم32|32ثابت|لايحل28.2مكانه؛securitysessionمصدرمختلفعنحفظbio|

الملكية/mergeorder/التبعيات/rawintegrity/productionauthorization/rollback في15 §9؛04 مطابق. لاNEXTمنافس في10/15. بعدكلتقدم القائد يحدثexactSHA/PR/verdict/run،لاتسقطأيشرطبنجاحT/B.

### اعتمادB دونزيادةبواباتالإنتاج — 2026-10-12

08 قرارالمالكالأحدث و15 §10 يعلوانعلىقواعدانتظارالقبولالخارجيالقديمةالمتعارضة. NEXT30منMAINحالي،بقية110تحفظبقائمةنقلقبلالإغلاق. مواضعجديدة30.1/30.2/30.3 قبل31؛جميعUNITs السابقة45 محفوظةوصفوف31–43 لمتُزح. لا إعادةSEC05/10 أوH7/Phase7/Finance/Ads.

| البند | قبل | بعد / حفظالنطاق |
|---|---|---|
|28/28.1 معقبولPHP|حاجبإصدارقديم|الكودMERGED/DEPLOYED؛العيوبالخارجيةالمحددةضمنهما،بالتوازي،قبول41|
|29 PR113|OPEN|MERGED،المشغللايعاد؛شواهدSتحفظفي41|
|30 /110|استكمالPR110نفسها|PRنظيفةللUNITنفسها؛حصرنقلثمإغلاق110،لاتحذفميزةمفيدة|
|SEC07|دينتحذيريبدونموضع|30.1قبل31|
|SEC08|دينتحذيريبدونموضع|30.2بعدتوحيدالمصدر|
|05/10falsepositives|تحذيراتقديمة|30.3حارس/توثيقفقط|
|31–43|31–43|مواضعهاوشروطها كماهي|

أيproposalمستقبليلايضيفgateقبلبيتابلاسببمثبتوإدراجفي14؛إكمالمنتجحقيقيليسفحصًاشكليًا. الصف41/R0يبقيانقبولالنسخةوقرارالإطلاق.

### إغلاق رحلة28 والاستعداد الخاص — اعتماد 2026-10-14

حفظ جميع 48 وحدة سابقة، وإضافة 28.3/28.4/28.5 فقط؛ أرقام 29–43 لم تتغير. أصبحت 51 وحدة. لا ميزة ضائعة: يقدم فقط status/transitions/live compatibility/role wiring اللازم من30 إلى28.5؛ التنزيل والتجميع والحقوق تبقى30. الصف41 لا يكرر قبولًا حديثًا سليمًا بلا تغيير أو عيب جديد.

| المصدر | الموضع الحالي |
|---|---|
| A غياب0001؛ B ملفات لا تعرض؛ E lease/drop |28.4 مع سبب التسجيل في28.3؛ لا فرض فساد MP4 أو فشل الرفع كله |
| C offer/answer/ontrack؛ D timeout/429؛ F اختلاف المسارين؛ G camera/Refresh |28.3؛ تحقق ثم إصلاح موضعي؛ أصول24/26 محفوظة |
| H النهاية لا تصل؛ I تأخر/end؛ J حالة LIVE أو spinner خاطئة |28.5 وجزء المشغل في28.4؛ أصول25/29 محفوظة؛ ينقل من30 نطاق الحالة فقط |
| الاستعداد الخاص لكل متنافس |28.3 بقرار08؛ متطلب خصوصية جديد معتمد |
| ad-placeholder404 |35؛ منخفض الأولوية ولا يحجب28 |
| Apache400؛ lock صفري؛ صلاحية0600 |400 محلول بشهادة المالك؛ البقية ليست عيوبًا دون دليل من المسار الفعلي |

لا انتقال إلى30 قبل حسم رحلة28 الآن، وفق قرار المالك الأحدث. ليست بوابة إنتاج عامة أو إعادة مراحل مغلقة. الحزم الثلاث لا تفرض ثلاث PRs.

### متابعة التجربتين وحفظ الترتيب — اعتماد2026-10-19

جميع51UNIT السابقة محفوظة مرة واحدة في الجدول؛ أضيفت ثلاث وحدات محددة فأصبح54. لا إعادة ترقيم29–43 أوإسقاطDoD. أرقام المواضع هنا للعرض،UNIT ثابت. حالاتNEXT القديمة في سجل§6 تاريخية؛ الحالي§2 فقط.

| الأصل | الموضع الحالي / ما حفظ |
|---|---|
|28.3 / PR118|28.3 CODE MERGED/DEPLOYED؛ قبولالعرضوالخصوصيةالمتبقي فيchild28.3.1 |
|28.4 / PR119|28.4 CODE MERGED/DEPLOYED؛ إصلاحfinalized محفوظ؛ ربطالمشغل/الزمنالمتبقي فيchild28.4.1 |
|28.5|الموضعنفسه بعدالمتابعتين؛ نهايةكلالأدواروالتسجيلللمتنافسين؛ لاchildمكررة |
|30 وPR110|تنزيلMP4باقٍ؛ التوافق الضروري للبث مننطاقه إلى28.3.1/28.5 فقط؛ لاfeatureمفقودة |
|29PLAYER|كود113محفوظ؛ لاrebuild، أمانالنافذةوالسلاسةيبقيانDoD؛ ربطالزمنالمثبت28.4.1 |
|32PROFILE-SAVE|باقٍبكاملDoD؛ بعده32.1للقوائمالشخصيةالجديدة، لايحلأحدهمامحلالآخر |
|35UX-I18N|كلالملاحظاتالسابقةمحفوظة؛ أدواتالبثالأساسيةتقدم28.3.1،الباقيوالحصيلةوالتذكير35 |
|31–43 وSEC07/08|معرفاتهاومواضعهاودليلهاوشروطهاباقية؛ إضافاتsubslots لا تسقطشيئًا |
|41ACCEPT|قبولالرحلاتالمتبقيةودمجشواهدالقبولالحديثة؛ لاإعادةقبولصحيحبلاسبب |

تبعياتالمسار في§2؛ تحضيرالقراءةالمستقلةممكن،لكنلاتكليفاتمتداخلةأوتنفيذقوائم32.1أوالتنزيل30قبلأوانهما. لاstageإنتاجعامةجديدة. القائديلتزم02/03/10وأدوارLOCAL/REMOTE؛ أيخطرجديديسجلبالدليلويعرضللمراجع/التخطيطبدلاتوسيعScopeذاتي.

### اعتماد20أكتوبر — FV2230 واستكمال الأدلة

الترتيب قبل→بعد ثابت:28.3.1 →28.4.1 →28.5 →قبول28 →30 →بقية§2. لاوحدةمزاحة/ملغاة/مضافة؛54UNIT كماهي. ما تغير حالة120/121 إلىCODE MERGED/DEPLOYED، ونطاق متابعة مثبَت ومصفوفة15§13 قبل/بعد ومنيتحقق.
showToastفيالمسارالمعطل وSIG/replay→28.3.1؛ الطوابعوالعداد→28.4.1؛ end/drain/marker/leave→28.5؛ NaN%→35. مرورالأدواتولغةالشعاروالنافذةمحفوظ، الهيدرأثرتصوير/nullلميتكرر؛ لاإصلاحافتراضي.
الملاحظاتالقديمةعنWebM و404وفشلP2Pالمطلقمصَححةفي15§13؛ تسجيلالمالكالسابقبمصدرينمحفوظ. لا إعادةcompositor دونإثبات، ولا تأخيرللـbisect. ماتمإصلاحهمنجرد35يسجلليُستثنىمنالإعادة، والباقيباقٍ.

### اعتماد21أكتوبر — متابعة قبول2242 دون مسار إضافي

قبل: متابعات28.3.1→28.4.1→28.5→قبول28. بعد: الكود122/123/124 مدمج؛ متبقيعقودها يجمع في **حزمة28 بملكيةLOCALواحدة**: A28-LEASE→A28-SURFACE→A28-TIME ثم قبولمحدد، وبعده30 كماكان.
لاإضافة/حذف/إزاحةUNIT؛54معرفًا محفوظةبنفسالترتيب، وأرقام29–43 وDoD كماهي. جمعالمتبقيلايعنيقبولالآباءأومحوإخفاقاتهم. 28.4.1/28.5 تبقيانمراجعالعقودلاNEXTينافسحزمة28.
المصدرتقريرFV-UNIT28-ACCEPTANCE-REPORT(1).md وموافقةالمالك21أكتوبر.15§14 يثبتالحدودوالفروضوالـbefore/after والمسؤولوالتحققSالأقل، ويحفظنجاحالمصدرينوأدلة2230المصححة. لا إعادةاختبارشامل أوتصميمبثجديد، ولا تقديم30/35/32.1.

### اعتماد23أكتوبر — إضافة30.4 قبلبوابةالقبولالمجمعة

قبل: قبولواحد30–30.3 →31 →32 →32.1 →33–42. بعد: **30.4 →قبولواحد30–30.4 →نفسالبقية**. تأخرتالبوابةو31ومابعدهابإضافةواحدةفقط دونإعادةترقيمأوإسقاطأيDoD. بقيت54UNITمرةواحدة، وأضيفR4-COMP-CONTROLS-EARLY-END-1ليصبح55.
المصدرملاحظاتالمالك23أكتوبروموافقتهعلىكاملالمقترح، بمافيه10نجومنظاميةللخصمفيprofile،0للمنهي، جودة0للقصيرةوطبقةظهوربعدالأطولمعالبحثالمباشر.15§15يفصلالتنفيذوالتحقققبل/بعدوالحقوقوالاستثناءات. الهجرةوالنشرالخارجيليسامفوضينمنهذاالتحديث.
أجزاءالألوانالمحددةالمنجزةتخصمكتكرارمن31/35بعدتوثيققبولها، لايسقطcompose/historyأوبقيةUX. H7الرقميةلايعاداعتمادها؛طبقةshortأولويةجديدةمعتمدة. PR110محفوظةإلىحصرالاستبدال؛لاcodechangesمنالمخطط.

### اعتماد24أكتوبر — ملحق متطلبين على 30.4 (PLAN PR #43)

قبل: مواصفة 30.4 = 15§§15.1–15.6. بعد: **15§§15.1–15.9** — أُضيف §15.7 (تبادل زر بدء البث وزر إنهائه) و§15.8 (حالات المربع الكبير/الصغير للمتنافس) و§15.9 (اختبارات A/B/M ومعايير القبول). لا إضافة/حذف/إزاحة UNIT؛ 55 UNIT بنفس الترتيب؛ 30.4 → قبول واحد 30–30.4 → 31 → 32 → 32.1 → 33–42 كما هو. لا تغيير في H7 أو قواعد التمويل أو أي وحدة غير متعلقة؛ 15§§15.1–15.6 وقرارات 23 أكتوبر محفوظة، والأسبقية الوحيدة المنصوص عليها في 15.7.6 (إظهار/إخفاء زرّي البدء والإنهاء).
المصدر: طلب المالك 24 أكتوبر وقراراته الحاسمة الثلاثة (08): زر الإنهاء = إنهاء المنافسة كاملة بلا تغيير وبلا زر إيقاف نشر جديد؛ لا مسار خروج جديد ولا تغيير سلوك قائم؛ الحالة قبل وصول فيديو الخصم = معاينة الكاميرا المحلية أو صورة الملف، ثم الحالات الأربع ديناميكية بوصول الفيديو الفعلي. أُضيفت أسبقية الحالة النهائية للخادم على التخطيط (15§15.8.4، ملاحظة مراجعة Codex P2).
**الحالة ≠ تنفيذ:** الملحق يُعد معتمدًا في الخطة بعد دمج PLAN PR والتحقق من SHA الدمج الفعلي على main. لا يعني تنفيذ كود ولا قبولًا. بعده: مراجعة القائد التقني للتحديث ثم موجه LOCAL تكميلي ثم REMOTE مستقل ثم القبول المجمع. لا موجه تنفيذي صدر من هذا التحديث، ولا مساس بكود أو بـPR #133.

### اقتراح 24 أكتوبر — وحدة 33.1 للاعتماديات الأمنية (PLAN PR هذا؛ لا يُعد معتمدًا قبل الدمج)

قبل: 30.4 → قبول مجمع 30–30.4 → 31 → 32 → 32.1 → 33 → 34 → 35–42 (55 UNIT). بعد: **… → 33 → 33.1 → 34 → 35–42 (56 UNIT)**. الإضافة R4-DEPS-SEC-1 فقط؛ لا إزاحة ولا حذف ولا إعادة ترقيم؛ كل DoD والبنود السابقة محفوظة، ولا NEXT منافس (NEXT = 30.4).
السبب: Hono وZod ثغرتان غير قابلتين للاستغلال في الكود الحالي (serveStatic غير مستخدم؛ Zod بلا مستورد للوحدة الوحيدة)، لكن فترة السماح (`continue-on-error` في quality-gate) لا تُقبل أجلًا مفتوحًا. الموضع قبل 34 يثبت الإطار قبل قياس DB-01 وقبل أي نقل MySQL (لا UNIT له بعد) ويعزل المتغيرات؛ ولا يلوّث القبول المجمع 30–30.4 ولا PR #133. التفصيل والأدلة والمخاطر والبدائل في [18](18-DEPS-SECURITY-UNIT33-1-SPEC.md). صمامات إعادة التقييم: استخدام جديد لـserveStatic/JWT/zod/validate() قبل 33.1، أو advisory عالٍ قابل للاستغلال.
تغطية: لا بند سقط؛ دفعات سلسلة البناء/الاختبار (vite/rollup/postcss، wrangler/miniflare/vitest-pool-workers، عابرات lockfile) تبقى مسجلة OPEN-TRACKED في سجل 33.1 ج. حالة PR #133 لم تتغير ولا يمسّها هذا التحديث (HEAD المعلن في صفحته العامة `6ac358a0dd4fadd74c469ecfee2992a03799c2c0`؛ غير متحقق عبر API).

### سجل استثناءات `npm audit` الإنتاجي (18§6 — قرار المالك D-1 = YES)

| GHSA | الحزمة / نطاق النسخة | سبب غياب المصحح | دليل عدم الوصول | مالك الاستثناء / قرار المالك | ينتهي / شرط إعادة التقييم | الحالة |
|---|---|---|---|---|---|---|
| — | — | — | — | — | — | **لا استثناء قائم.** Hono (4.13.11) وZod (4.6.6) لهما إصلاح منشور فلا يؤهلان؛ تعالجان في A وB. يطابق هذا الجدول `dev-tools/audit-exceptions.json` حرفيًا عند إنشائه في 33.1 |


## تحديث الحالة المعتمدة — 2026-10-28 / UNIT33 + UNIT33.1

- **CODE MAIN / actual merge SHA:** `20c16dc7bbda3af1aa3b0597f0f147a59c44b1c4` (PR #145).
- **Post-merge Quality Gate:** [run 40599735765](https://github.com/Maelsh/dueli-opus/actions/runs/40599735765) SUCCESS على SHA الدمج نفسه.
- **Deploy to Cloudflare Pages:** [run 40599735788](https://github.com/Maelsh/dueli-opus/actions/runs/40599735788) SUCCESS على SHA نفسه؛ job Quality Gate dependency وDeploy كلاهما SUCCESS. هذا يثبت نجاح مسار النشر، ولا يساوي قبولًا يدويًا شاملًا للرحلات الحية.
- **UNIT33 + UNIT33.1:** merged/deployed. أُغلقت ملاحظات P3 الموثقة قبل الدمج. التحصين الاختياري DUELI_AUDIT_CMD لا يفتح PR145 من جديد وحده.
- **بلاغات المالك من المنافسة الحية 2026-10-28:** أزرار العين/الكاميرا، fullscreen، اتجاه AR/EN، نص Reminder، تزاحم الهيدر وخروج العناصر عن إطار الهاتف، انتقال المقاطع، وتجميع فيديو تنزيل مدته الأصلية دقيقتان إلى ملف يقارب10 دقائق مع بطء/تقطع. سجل التفاصيل في08 وتقرير قائد التخطيط. السبب الجذري لم يُثبت؛ لا تُسجل هذه البنود كإصلاحات ولا تعاد وحدة مغلقة بلا دليل. يحدد القائد موضع كل بند في الوحدات القائمة مع بقاء PR #110 OPEN/HOLD.
- **NEXT:** توثيق الإغلاق الفعلي في سجلات الخطة/التسليم وفق بروتوكول10، ثم UNIT34 فقط بعد اكتمال التوثيق. لا يبدأ LOCAL تنفيذ34 قبل دمج تحديث الخطة واعتماد PLAN SHA الجديد. إجمالي58 UNIT وترتيب33→33.1→34→35–42 ثابتان.
