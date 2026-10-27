# Dueli — بوابة استئناف القيادة

## لقطة الاستئناف المعتمدة — 2026-10-27 (قرار المالك: UNIT32.2-REM1 NEXT)

- **CODE MAIN / actual merge SHA:** `603d826834e3f8490caff3a67db854fb6eedb647`؛ PR #142 / UNIT32.2 الأساسية؛ approved HEAD `5fa03f443c8c7dcf51f167afbdba45449beae92b`; BASE `3b1b6b64914cbfc861e00063643431c60539a284`.
- **Post-merge Quality Gate #386:** [run 40512334779](https://github.com/Maelsh/dueli-opus/actions/runs/40512334779) SUCCESS: 2107 passed / 1 skipped, G2 300≤310, routes251. **Deploy #615:** [run 40512334753](https://github.com/Maelsh/dueli-opus/actions/runs/40512334753) SUCCESS على SHA نفسه؛ production deploy step وread-only schema readiness نجحا. لا migration.
- **UNIT32.2 الأصلية / PR #142 = CODE MERGED / DEPLOYED**، لكن صف32.2 لا يُغلق تخطيطيًا حتى إتمام متابعة المالك REM1. لا قبول يدوي شامل على المتصفح/الجهاز/قارئ الشاشة/IME؛ لا `PROD VERIFIED`.
- **OWNER APPROVED — NEXT = UNIT32.2-REM1 ضمن الصف32.2 نفسه:** (A) pagination مستقرة حتى `hasMore=false` وإزالة سقف50؛ (B) تصحيح تمرير العنوان ذي الاقتباسات والمحارف الخاصة؛ (C) إزالة `.trim()` من قيم كلمة المرور؛ (D) التفريق بين OAuth مع/بدون hash كلمة مرور محلي؛ (E) تصحيح توثيق اختبارات #142 من14 إلى13 وإضافة العدد الفعلي لاختبارات REM1. (F) أدلة `db.batch` والاختبارات التسلسلية مقبولة، ولا اختبارات ضغط/تزامن جديدة مطلوبة. مواصفة النطاق في13§9، القرار في08، وسجل العناصر في12.
- **الاختبارات وحدودها:** مراجعان مستقلان وافقا HEAD الأصلي؛ اختبارات accept-first/delete-first تسلسلية لا تثبت طلبات D1 متوازية. لا توصف كاختبار تزامن حقيقي. لا اختبار Playwright مستقل أو قبول يدوي شامل مدّعى.
- **بعد إغلاق REM1:** المسار غير المتغير `32.2-REM1 → 33 → 33.1 → 34 → 35–42`; إجمالي الخطة58 UNIT ومعرفات33–43 محفوظة. PR #110 خارج النطاق. `14-UNIFIED-EXECUTION-PATH.md` هو المصدر الوحيد لترتيب/NEXT.
- **PLAN BASE قبل تحديث المالك:** `34758430f8e4aab987ba60abbf9abaccf94b561c`. المرجع النهائي هو PLAN MAIN الجديد بعد دمج PR التخطيط.

## لقطة تاريخية — 2026-10-26 (بعد دمج UNIT31؛ NEXT حينها UNIT32، استُبدلت في27أكتوبر)

- **CODE MAIN / actual merge SHA:** `3cee6e78ce0750536c474131363f80902b886c7d`؛ PR #139 / UNIT31 مدموجة من HEAD المعتمد `da437d6cc8ecee5c9e1fc600826f1fe89bb76ee3`.
- **Post-merge Quality Gate #378:** run 40371372964 SUCCESS. **Deploy to Cloudflare Pages #607:** run 40371372929 SUCCESS على SHA الدمج نفسه؛ فحص production bindings وread-only schema readiness ناجحان، وخطوة نشر الإنتاج ناجحة. لم تُطبّق migration.
- **UNIT31 / R4-MESSAGES-1 = CODE DONE / DEPLOYED.** تقريران مستقلان APPROVE؛ M-01..M-05 PASS ضمن نطاق المراجعة وF-1 مغلق باختبار RED→GREEN. حدّ فتح profile لمحادثة خارج أحدث100 قبل أول إرسال يبقى تحسينًا غير مانع، موثقًا في12 و14.
- **NOT TESTED / no overclaim:** لم يحدث نقر يدوي على متصفح/جهاز فعلي أو اختبار لوحة IME فعلية أو SSE حي؛ لا تسجل PROD VERIFIED. لا تغيير مخطط/هجرة أو كتابة بيانات D1؛ بوابة الإنتاج جمعت المخطط للقراءة فقط.
- **Gate 30–30.6 = ACCEPTED / CLOSED.** D-01 وD-02 وشواهد القبول السابق محفوظة. فروع UI لduplicate-409/scheduled-conflict وactive lease drain وupstream-invalid/no-DB تبقى NOT TESTED إنتاجيًا؛ D-03 يبقى UNIT35.
- **NEXT حينها = UNIT32 / R4-PROFILE-SAVE-1.** إجمالي الخطة 57 UNIT؛ لا إزاحة أو إعادة ترقيم 31–43. PR110 خارج النطاق ولا يدمج. المصدر الوحيد للترتيب وNEXT هو14.

في تلك اللقطة كان [14](14-UNIFIED-EXECUTION-PATH.md) مرجع NEXT؛ لقطة 27أكتوبر في أعلى الملف هي المرجع الحالي. قرارات [08](08-OWNER-DECISIONS.md)، ومواصفة [15§12](15-CHUNK-INDEX-UPLOAD-PLAYER-PLAN.md)، وقوائم البروفايل [13§8](13-LIVE-CHUNKS-UNIFIED-GUIDE-PLAN.md) معتمدة19أكتوبر.

## لقطة24أكتوبر (لاحقة) — اقتراح UNIT33.1 للاعتماديات الأمنية (PLAN PR، غير مدموج)

- PLAN BASE `f5e9d39cafb6b6eab68d089a4b42e7a1663de143` (دمج PR #43)؛ CODE MAIN `85eec139893f3b8f783befb8b119f709f8e40b33`. PR #133 مفتوح وفق صفحته العامة (HEAD `6ac358a0dd4fadd74c469ecfee2992a03799c2c0`؛ لم يتحقق عبر API).
- أُضيف اقتراح وحدة **33.1 / R4-DEPS-SEC-1** بين 33 و34 (Hono + Zod + سجل اعتماديات؛ 14 و[18](18-DEPS-SECURITY-UNIT33-1-SPEC.md)؛ قرار المالك D-1 = YES في 08). 55→56 UNIT؛ لا إزاحة. **NEXT لم يتغير: 30.4** — لا تكليف LOCAL ولا ترقية ولا مساس بـPR #133 أو بوابة 30–30.4.

## لقطة24أكتوبر — ملحق UNIT30.4 (PLAN PR #43؛ معتمد في الخطة بالدمج)

- PLAN BASE `32dbdd09994fc96bd847bb75233d80609b23c626`؛ CODE MAIN `85eec139893f3b8f783befb8b119f709f8e40b33` (متحقق من الحي). PR #133 HEAD وفق ref: `547e756e81a5069344f4332e2091091a996d36f9`؛ حالته open/merged غير متحققة من التخطيط.
- أُضيف لـ30.4: تبادل زرّي بدء/إنهاء البث وحالات المربع الكبير/الصغير للمتنافس (15§§15.7–15.9، 08/24أكتوبر). لا UNIT جديدة، لا بوابة، لا تغيير ترتيب؛ المرجع 14.
- لا تكليف LOCAL قبل: مراجعة القائد التقني للتحديث ← موجه تكميلي (الدمج والتحقق من SHA تمّا في تقرير التسليم). PR #133 لا يُراجع/يُدمج على أنه مطابق للملحق.
- قرارات المالك الثلاثة (زر الإنهاء = إنهاء المنافسة كاملة بلا زر إيقاف نشر؛ لا مسار خروج جديد؛ معاينة الكاميرا/صورة الملف قبل وصول فيديو الخصم ثم حالات ديناميكية) مسجلة في 08 كقرارات نهائية؛ لا أسئلة مفتوحة.

## لقطة23أكتوبر — استئنافUNIT30.4

- PLAN BASE `1a7caf10fae9e2d332c6c08b166fcffdb441f7d7`؛ CODE MAIN `85eec139893f3b8f783befb8b119f709f8e40b33`.
- UNIT28 ACCEPTED/CLOSED كمافي22أكتوبر؛ لاتعاد. PR129/30،130/30.1،131/30.2،132/30.3 MERGED؛ actual-main Quality39995222613 وDeploy39995222476 SUCCESS؛ **PRODUCTION ACCEPTANCE PENDING** للوحداتالأربع.
- مصدرNEXTوالترتيب14: الإضافةالمعتمدة30.4 قبلقبولواحدمجمّع30–30.4 ثم31وبقيةالمسار. المواصفة15§15 وقرار08/23أكتوبر. لايستأنفمنNEXT30 التاريخيةأويبدأ31أوالقبولقبلالإضافة.
- المتطلبات: برجواحديجمعالإجراءالمناسببدءًا/نشرًامعصلاحيةوموافقةصريحة، expandغيرfullscreen؛ fullscreenبأدواتوخروجظاهر، هاتفملائم، ألوانdownload/comment/message كتدرجالمنصة.
- إنهاءصريحقبل300s: تأكيد، خسارةالمنهي، رصيدنظامي10للخصم/0للمنهييدخلالتقييمالعام مرةواحدة؛ لاfakeviews/voters. كلقصيرةجودتها0وتعرضبعدالبدائلالأطولمعالبحثالمباشر؛ وقتالخادمهوالمرجع، لاانقطاعكإنهاء.
-55UNITبعدإضافةواحدة،54السابقةمحفوظة. PR110 OPEN/HOLD ببديلPR129،يحصرالاستبدالقبلإغلاقهالاتُدمج.
- الخطةفقط؛لاcode/PHP/D1/إعداداتنشرمعدلة. تحققLOCALقبلpatchوREMOTEبعدهثمقبولمجمعبالأدواروالهاتفوالحدودالزمنيةوفق15§15.6.

## لقطة2026-10-22 التاريخية — NEXT30 فيها استُكملت


**UNIT28 ACCEPTED — 2026-10-22 (OWNER APPROVED / PRODUCTION VERIFIED).** CODE MAIN `a2579ce5f1f0d32077506b56553fe9a0f79619f8`; PR125/126/127 MERGED. Post-merge [Quality 39662569083](https://github.com/Maelsh/dueli-opus/actions/runs/39662569083) SUCCESS and [Deploy 39662569170](https://github.com/Maelsh/dueli-opus/actions/runs/39662569170) SUCCESS on exact SHA. Independent real-browser production acceptance: new competition **2253**, three authenticated contexts, two media sources, End while publishing, finalized 11/11 inline snapshot → verified tail 12 chunks / 134.554s, bounded automatic refresh, no reload/playback reset, duration/seekbar updated, polling stopped. Report: `A28-PR127-PRODUCTION-ACCEPTANCE-REPORT.md` (2026-10-22; owner-provided acceptance artifact). Earlier PR125/126 and competitions 2243/2244/2250/2251 remain historical evidence. A28-LEASE/SURFACE/TIME and 28.1–28.5 including children closed within tested scope. No re-test of accepted work without a new independently evidenced defect. **NEXT: UNIT30 R4-CHUNK-DOWNLOAD-1, option B**; PR110 remains OPEN/HOLD and must not be merged; inventory reusable work before clean replacement PR. Preserve 30.1→30.2→30.3→31→32→32.1→33–42, all 54 units and existing DoD.

تبدأ المهمة التالية UNIT30 من CODE MAIN المثبت، وفق14 و15 §§6/10/12.6، مع احترام PR110 HOLD وعدم نقل كوده عشوائيًا. لا تكليف UNIT28 جديد.

## لقطة2026-10-21 — تاريخية وليست حالة الاستئناف

- CODE MAIN `d0768783ede68c11aab9cc442c148d99349fead3`؛ PLAN BASE `d9744c8ce1ee06ac8f0503f56bf792891f88d0d4`.
- PR122→`54a3380a3c2c06319d48b2be2f953134bba2302d`؛ PR123→`a422f776381a91349e8e2b111dbe92734ed3e89a`؛ PR124→MAIN الحالي؛ كلهاMERGED. Quality39551641343 وDeploy39551641346 SUCCESS.
- **UNIT28 NOT ACCEPTED** بتقرير2242. كودمدمج/منشور لايساويقبولًا. المصدرانظهرافعليًافيالتسجيل، والإشارة/النشر/التوست/replay وLIVE/VODللمشاهد نجحتفيحدودها وتحفظ.
- الحالةوالترتيبوالـNEXT في14 وحده: حزمةمتابعة28 بملكيةواحدة، وعقودهاومصفوفةالتثبتقبلpatch والمراجعةبعده في15§14. لاوحدةجديدة أوإعادةالوحداتالمدمجة.
- المتبقي: تعافيالتسجيل بعدفشلleaseعابر، سطحVODللمنافسين دونRefresh، قراءةالوقتالجارية؛ أسبابالمسارالمفترضةتثبتقبلpatch.
- preview>40s ملاحظةتتبع؛ screenBLOCKED لاتغلقبـPASS؛ endمعخصمنشطغيرمختبرفي2242 يكملبموضعه. قبولSواحدمحددبعدالإصلاح،لاكلالنجاحاتالقديمة.
- 54UNIT محفوظة؛PR110 OPEN/HOLD،30بموضعهاو35/32.1بمواضعهما. لاتغييرH7/المال/الاستضافة/D1/PHP.

## لقطة2026-10-20 التاريخية — ليست حالة الاستئناف

- CODE MAIN `38ffa575e34d6912818f1ebc9e0a1a761d110da4`؛ PLAN BASE `c1ade66f863afb24937bf9e981536d33b62e8702`.
- PR120/28.3.1 MERGED إلى`2abf5ade279804d1ec07a4ece22cbf810b4c50ba`؛ PR121/28.4.1 MERGED إلىMAIN أعلاه. Quality39416835180 وDeploy39416835145 SUCCESS. CODE MERGED/DEPLOYED لايعنيACCEPTED.
- المصدرالحالي للحالةوالترتيب14؛ مواصفةالمتابعةومصفوفةقبل/بعد ومسؤولLOCAL/REMOTE في15§13، إضافةإلى§12. لاNEXTجديدفي04.
- FV2230 واستكماله مصححان: SIGمشروط؛ توستمسارالنشرعائق؛ MP4حقيقيبطوابعغيرصفرية؛ لاfinalizeHTTPمتوقعولا404موثق؛ غيابمصدرالخصمليسإثباتفسادcompositor.
- حفظPASSلأدواتالمرجع/المعاينة/لغةالشعار/إخفاءdebug/القفزوالنافذةغيرالمتأثرة. nullلميتكرر، الهيدرأثرتصوير. رفضميزةleave-and-return لايلغيreconnectأوصلاحياتendالقائمة.
- لاوحداتجديدة ولاإزاحة؛54UNITمحفوظة؛30/32.1/35وبقيةالمساركماهي. PR110 OPEN/HOLD بنفسHEAD القديم.
- LOCALيثبتسببالـpatchفيالمهمةنفسها؛ REMOTEمستقلعلىHEADبعدها؛ Sللوسائطفعليًا. لاجولةتشخيصإنتاجيةثالثةقبلالإصلاح؛ ماتعذرمنأدلةيعالجموضعيًاأثناءالتنفيذولايمحى.

## لقطة2026-10-19 التاريخية — ليست حالة الاستئناف

- CODE MAIN: `ce5e0e728dfbac59f3cd1f4e15508e2c374fe6fe`؛ PLAN BASE: `1a69fcd93c8e389075c6293502f0dfcd36468a70`.
- PR118/28.3 MERGED إلىdcb56c7؛ PR119/28.4 MERGED إلىMAIN الحالي. Quality38733693451 وDeploy38733693448 SUCCESS لنفسMAIN. القبول الحقيقي للبث ما زال مفتوحًا.
- PR119 أصلحت نهاية انتظارLIVE عندfinalized بلا مقاطع قابلة للتشغيل؛ لا تعيدها ولا تعمم نجاحها على كل الأعراض.
- NEXT28.3.1 متابعة الدخول/الخصوصية/مصادر الوسائط/أدوات الاختبار؛ ثم28.4.1 للزمن والتشغيل؛ ثم28.5 للنهاية وانتقال الجميع للتسجيل؛ قبول رحلة28؛ ثم30 وبقية14.
- المالك اعتمد كل تفاصيل تجربتي البث وتصحيحين: أدوات التحكم بأشكال وألوان صفحات الاختبار المحفوظة؛ وwatchlater/history مطلوبان في قسم خاص بالبروفايل في32.1، بعد32 وقبل33.
- مرجع الأدوات: src/modules/pages/live/views/host.ts وguest.ts وstyles/test.css؛ أيقونات فقط وtitle/aria؛ لا تصميم بديل أو نسخ منطق اختبار قديم.
- O19-01..21 في15§12 تربط كل عرض بموضعه؛ لا اختزالها في ملخص القائد. تحقق كل عيب وسببه قبلpatch؛ ALREADY DONE/NOT REPRODUCED محليًا لا يغلقان فشل الإنتاج.
- PR110 OPEN/HOLD، HEAD`6e7ca1039484980affbcaf6f0eab548a82c35d17`. التنزيل30 بالخيارB مستقل عنcache المشغل؛ لا دمجHEAD القديم. ينقل فقط التوافق اللازم للبث إلى28.3.1/28.5.
- جميع51UNIT السابقة محفوظة؛3 إضافات ترفعها إلى54. الصفوف29–43 وSEC07/08 وH7 وKEEP NOW ثابتة.
- سجلاتWORKLOG/PLAN-STATUS التاريخية قبلدمج118/119 لا تثبت أنهما مفتوحتان الآن؛ يسجل قائد التنفيذ أحدث حالة دون حذف التاريخ.

## قواعد الاستئناف

اقرأ02/03/08/10/11/14/15§12 و13§8 عند32.1، وAGENTS وتعليمات الكود ذات الصلة. كلLOCAL/REMOTE موجه مكتفٍ بذاته يتضمن المستودعات والموقع وPLAN SHA/BASE/HEAD/UNIT والنطاق وملكية الملفات وDoD والتفويض والملفات الواجب قراءتها.

LOCAL ينفذ؛ REMOTE مستقل يراجع؛ القائد ينسق ويدمج وفق10 ولا ينفذ أويراجع نهائيًا أويوسع النطاق ذاتيًا. يتابع أيعملنشط بدليله بدل تكليف مكرر؛ لا يفترض أن غيابPR يعني غيابWIP محلي.

حالة PR الكود صادقة معWORKLOG/PLAN-STATUS، ثم14 بالأدلة وروابطHEAD/merge/Quality/Deploy والقبول المتبقي. queued/pending ليستنجاحًا. اختباراتالمنطقوالشبكة أولًا ثم S للصوتوالصورةفقط؛ قبولواحدللرحلةالمعدلة، وقبول41 للمتبقي دون إعادةشاهد سليم.

التحديث تخطيط فقط؛ لاcode/PHP/D1/نشر أوإعادةفتحمراحل مغلقة. Apache400 محلول وشهادةالمالكعنالمقاطعالصالحة محفوظة.
