# Dueli — فهرس المقاطع وأمان الرفع والمشغل والتنزيل

**OWNER APPROVED — 2026-10-11.** المالك وافق على التقسيم والترتيب والمعالجات وطلب تثبيتها ودمج الخطة، وسلم نص upload.php الحالي. ترتيب وحالة وNEXT حصريًا في[14](14-UNIFIED-EXECUTION-PATH.md). هذا ملف عقود وDoD، وليس مسارًا ثانيًا. 08 للقرارات و10 للإصدار؛ لا إعادة H7 أو مراحل مغلقة.

## إغلاق قبول UNIT28 — 2026-10-22

**UNIT28 ACCEPTED — 2026-10-22 (OWNER APPROVED / PRODUCTION VERIFIED).** CODE MAIN `a2579ce5f1f0d32077506b56553fe9a0f79619f8`; PR125/126/127 MERGED. Post-merge [Quality 39662569083](https://github.com/Maelsh/dueli-opus/actions/runs/39662569083) SUCCESS and [Deploy 39662569170](https://github.com/Maelsh/dueli-opus/actions/runs/39662569170) SUCCESS on exact SHA. Independent real-browser production acceptance: new competition **2253**, three authenticated contexts, two media sources, End while publishing, finalized 11/11 inline snapshot → verified tail 12 chunks / 134.554s, bounded automatic refresh, no reload/playback reset, duration/seekbar updated, polling stopped. Report: `A28-PR127-PRODUCTION-ACCEPTANCE-REPORT.md` (2026-10-22; owner-provided acceptance artifact). Earlier PR125/126 and competitions 2243/2244/2250/2251 remain historical evidence. A28-LEASE/SURFACE/TIME and 28.1–28.5 including children closed within tested scope. No re-test of accepted work without a new independently evidenced defect. **NEXT: UNIT30 R4-CHUNK-DOWNLOAD-1, option B**; PR110 remains OPEN/HOLD and must not be merged; inventory reusable work before clean replacement PR. Preserve 30.1→30.2→30.3→31→32→32.1→33–42, all 54 units and existing DoD.

هذا التحديث يغلق معيار القبول في §14 ولا يغير عقود الوحدة 30 أو شروطها. النصوص الأقدم عن NOT ACCEPTED وNEXT28 لقطات تاريخية لا تسري على الحالة الحالية في14.

## 1. المصدر وحدود الأدلة

- CODE MAIN `216e4b5d60beb9f5870b2baa2cc6200b2b2d3e7b` بعد PR109؛ Quality38113484659 وDeploy38113484655 SUCCESS على نفس SHA.
- PR110 OPEN / NOT MERGED؛ HEAD `6e7ca1039484980affbcaf6f0eab548a82c35d17`. تقرير REMOTE المستقل R4-CHUNK-DOWNLOAD-1-REMOTE-FINAL-GATE-REPORT.md: REJECT بسبب فشل تحميل FFmpeg.wasm والتعامل مع الخطأ؛ اختبارات T/B خضراء لا تثبت ملف MP4. lease اختبرت على المنصة، أما upload/finalize الخارجيان فاختبرا بستب، لا بالخادم الحقيقي. لا نسمي جميع الملاحظات blockers صادرة عن REMOTE الأصلي.
- تحليل القائد: historical player يستعمل عنصرين وتحضير التالي وحandoff قريبًا من0.6s مع كتم/إيقاف القديم؛ الحالي لا يحقق التنظيف نفسه. المالك شهد سلاسة الانتقال القديم؛ نعالج الخلل الحالي فقط. penultimate-live احتياط غير مقاس؛ VOD يحمل كل المقاطع مسبقًا. playlist.php فارغ بحسب المالك، وليس قراءة مستقلة للخادم.
- **upload.php — نص المالك مقروء كاملًا في11أكتوبر؛ لم يعدل أو يشغل على الاستضافة:** التحقق اختياري عند وجود chunk_key، ثم valid فقط، دون ربط مثبت competition/sequence/generation/holder. يحفظ إلى chunk_%04d في مسار ثابت، قابل للاستبدال. metadata.json قراءة→تعديل→كتابة دون قفل؛ last_chunk آخر طلب وليس أعلى sequence موثق. حذف المفتاح بعد الحفظ عبرDELETE مع تجاهل الفشل ليس استهلاكًا ذريًا للمفتاح. لا تحقق حجم/نوع فعلي أو duration؛ امتداد العميل ليس إثبات container. offset لأول قطعة فقط. CORS=* ليس مصادقة. URL الافتراضي قديم ويقرأ .env بصيغة بسيطة؛ يلزم إعداد موثق لا تخمين الرابط.
- finalize.php/stream.php/watcher.js/end-stream.php/old_playlist.php تحتاج usage/security inventory قبل تعديل/إزالة. خبر server FFmpeg وحذف القطع مصدره التحقيق المنقول؛ لا ندعي قراءة نسخ الإنتاج كلها. لا حذف من مجرد غياب مستدعٍ في المستودع ولا طلب أسرار/cPanel URLs.
- القرارات الجديدة أدناه تتقدم على وصف «عقد FFmpeg الخارجي» التاريخي في13؛ **ممنوع FFmpeg على الاستضافة**.

## 2. العقد المشترك

الاستضافة تخزن وتقدم ملفات المقاطع فقط؛ لا دمج/تحويل/FFmpeg ولا حذف قطع عند الإنهاء. المنصة تملك سلطة الدور والlease وsequence ونهاية المنافسة ونشر metadata. browser/app يشغل ويجمع التنزيل باستخدام FFmpeg.wasm؛ playback لا يشترط تحويل كل الفيديو مسبقًا.

المضيف وحده يسجل الطرفين، وانقطاعه ليس end. الاستئناف append مع sequence جديد من الخادم، دون overwrite أو إعادة مؤقت المنافسة. نهاية المنافسة وcutoff فوريان وفق العقد القائم؛ final recording marker يتبع آخر رفع مخول ضمن مهلة drain محدودة موثقة، لا يفتح رفعًا غير محدود ولا يؤخر النتائج.

كل وحدة تحدث WORKLOG/PLAN-STATUS داخل PR بحالة صادقة. SQL فيModels؛ migrations additive وrequired_schema/readiness وrunbook وفق10. التوثيق هنا يفوض إعداد الكود والاختبار المعزول، ولا يشغل migration بعيدة أو يغير الاستضافة تلقائيًا.

## 3. R4-CHUNK-INDEX-1 — metadata وتوقيت مرجعي واحد

**التبعية:** COMP109 منجز؛ **الخروج:** عقد فهرس DB قابل لاستخدام uploader/player/download. التنفيذ الأول يحفظ توافق القراءة الحالي ولا يفعّل رفعًا جديدًا غير محمي قبل وحدة SAFE.

- D1 المصدر الحاسم: competition، sequence، generation/holder، مسار immutable، container/codec، bytes، مدة موثقة، بداية timeline، upload state/confirmed-ready، finalization state. حدّد الحقول الأساسية والتحقق ومن يكتبها قبل التنفيذ؛ مدة أو حجم يرسله العميل غير موثق لا يكفي لإعلانready.
- فرّق uploaded/pending/ready/failed وانتهاء المنافسة عن اكتمال القائمة. sequence عالي وصل أولًا لا يعني جاهزية كل السابق. مسار قديم أو فارغ لا يمسح تسجيلًا موجودًا.
- public playlist endpoint بعقد توافق صغير يستمد DB، وليس ملف PHP/metadata.json سلطة موازية. snapshot/version/range أو cursor للزيادات؛ lookup زمان→chunk/offset عبر فهرس، لا تنزيل القائمة كلها عند كلpoll.
- gap بسبب انقطاع المضيف يظل موثقًا؛ اختر mapping consistent يحفظ المنافسة والتعليقات/video_offset مع seek، دون خلق فيديو أو إسقاط المدة صامتًا. اعرض تعارضًا حقيقيًا فقط على المالك، لا قاعدة انتهاء جديدة.
- Model portable لـMySQL لاحقًا؛ لا D1 APIs فيUI/PHP، ولا MySQL migration الآن. ملفات الفيديو تبقى خارجDB.
- أي استيراد metadata قديمة: إعداد mapping/runbook read-only أولًا، لا حذف/إعادة ترميز تاريخية من هذه الخطة.

**T/B:** ordered/unordered/retry/gap/resume/end/manual+cron، time lookup، ready بعد إثبات تخزين، توافق route، permissions، تكلفة range/continuation وعدمfull scan لكلviewer. لا S/Astra لتصميمSQL.

## 4. R4-CHUNK-UPLOAD-SAFE-1 — منع الكتابة والاستبدال غير المخولين

**التبعية:** INDEX؛ هذا هو موضع lease/fencing المستخرج منPR110 عند الحاجة، لا lease موازٍ.

- مفتاح إلزامي قصير الصلاحية، مربوط بالمضيف/المنافسة/الlease generation/sequence/object identity والحدود. إصدار المفتاح يرفض stale-generation؛ تحقق الاستضافة يثبت العقد كاملًا، لا valid مجردة ولا صلاحية منCORS.
- لا unsigned optional upload أو legacy fallback عند lease_unavailable. readiness/migration تسبق التفعيل؛ إذا غاب شرط الأمان يفشل مغلقًا بخطأ واضح، دون إيقاف نتيجة المنافسة.
- تحقق حديث عند قبول الرفع **وعند نشر ready**؛ signature وحدها لا تلغي مفتاح الجيل القديم بعدtakeover. طلب قيد النقل قد يترك object معزولًا، لكنه لا يستبدل القديم ولا يدخل القائمة العامة؛ لا وعد بمنع كلbyte سبق دخوله للشبكة.
- تخزين immutable مع temporary/quarantine ثم إتمام مؤكد؛ exclusive/atomic publish ومنع overwrite، مع idempotent retries لنفسbytes وإخفاق conflict المختلف. لا يعلن نجاح قبل وثوق الحفظ وreceipt خادمي مصادق ومطابقةsize/hash/object.
- استهلاك/حجز المفتاح والتأكيد لهما state machine مقاومة للتكرار والسباق؛ حذف best-effort بعد النقل ليس fencing. لا تخزين مفاتيح فيURL/log عام حيث يمكن تجنبه.
- تحقق file error/حجم/نوع/حدودsequence والهوية والمسار؛ bounds/timeouts/backpressure/cleanup مؤقتات واضحة. لا منطق FFmpeg علىPHP؛ noXSS/path traversal، CORS لأصول موثقة إذا احتاجت دون اعتبارهاauth.
- أوقف finalize serverFFmpeg/deletion، وانقل الإنهاء لـplatform final marker مصادق idempotent مع drain محدودة. end/cron/release/takeover لا تقبل finalize لغير generation المخول.
- inventory ملف→مستدعين/URL/cron/الغرض/المخاطر/قرار بقاء أو توافق أو إزالة. احتفظ بالنسخ والتراجع، لا إزالة عمياء. افصل deploy الكود عن تطبيقPHP/DB بمراجعةrunbook وتفويض التشغيل المحدد. المالك لا يحتاج إرسال أسرار.

**T/B:** missing/invalid/expired/wrong competition/wrongsequence/stalegeneration، إصدار مفتاح بعدtakeover، replay/overwrite، concurrentuploads، lateoldholder، storagefail/receiptfail، end+drain، فشلreadiness. **دليل خارجي محدود لازم:** اختبار endpoint الحقيقي المخول أو بيئة مماثلة موثقة، لا stub فقط؛ تثبت خطة النشر عدمالنافذة بينclient/PHP/schema. لا camera vision لهذاالجزء.

## 5. R4-CHUNK-PLAYER-UX-1 — تحسين المشغل الموجود

**التبعية:** INDEX+SAFE؛ يستعمل نفس double-buffer الموجود؛ لا rebuild أو MSE من غير شاهد focused يبرره.

- LIVE يبدأ **أحدث confirmed-ready chunk**، مع backward seek وعودة واضحة للحافة الحية؛ لا penultimate افتراضيًا. انتظار nextready يعرضbuffering صادقًا.
- VOD للجمهور/Guest؛ unifiedtimeline وtime→chunk/offset وseek البداية/المنتصف/النهاية. bounded preloading حول الموضع الحالي؛ لاfetchALL أوcache كامل مؤبد.
- تحضير التالي والتحويل عند حد صحيح قابل للقياس؛ الرقم0.6s شاهد تاريخي وليس حدًا يفرض قطع آخر الفيديو. أوقف/اكتم القديم ونظفhandlers/objectURLs ولاaudiooverlap. stalled/late/gap/retry/backoff/cancel والتنقل بينlive/rewind آمنة.
- التعليقات مرتبطة بـtimeline الصحيح، لاcreated_at كبديل؛ لا تغير أهلية300s/cutoff. سياسة تفاعلالمشاهد القائمة محفوظة.
- UX ar/en،RTL/mobile/desktop، controls/keyboard/aria، لا pollingstorm؛ قياسnetwork/memory/D1 مختصر ينقل نتيجته لـDB-MEASURE دون انتظار قياس شامل قبل الإصلاح.

**T/B:** seek offsets/duration/finalmarker، حدودmemory/cache، rapidseek/retry/tail، تنظيفaudio/objects ومنعالطلبالمكرر. **S مركزة:** انتقالات فعلية مع صورةوصوتالطرفين، liveedge→rewind→live، VOD seek، hostdisconnect/resume. المالك أو وكيلcomputer بوسائط مناسبة؛ لا إعادةTURN/Finance/Ads ولا اشتراطAstra.

## 6. R4-CHUNK-DOWNLOAD-1 — استكمال الوحدة الأصلية / PR110

**التبعية:** الوحدات الثلاث؛ UNIT ثابت نقل من27 إلى30. PR110 محفوظ OPEN / HOLD — REMOTE REJECT، لا دمجHEAD الحالي ولا تكليفdownload منافس.

القائد يوثق extraction اللازمة للprerequisites معpaths/commits، ثم يحدّثbase/HEAD لـPR110 بعددمجها ويراجعdiff المتبقي مستقلًا. لا ضياع auto-transitions/lease/التوثيق الصحيح ولا تكراره؛ إزالةfeature منdiff لأنهاmerged فيprerequisite تربط بالدليل، لا إسقاط.

- FFmpeg.wasm تحميل صالح: package/worker/core/assets بإصداراتمتوافقة وطريق/CSP مثبتين؛ packaging/own-origin مناسب بدل إصلاحURL فقط. streaming playback لا يلزم wasm، assembly فقط؛ لاserverFFmpeg.
- إصلاحshowToast فيمساراتdownload/lease المتأثرة الآن، errors/progress/cancel/cleanup واضحة AR/EN. باقي جردtoast فيUX-I18N محفوظ؛ سجل المواضع المنجزة هناك لتجنبإعادتها.
- ملفMP4 حقيقي مترتب بمدة وصورتين وصوتين وseek صحيح؛ اختبار الناتج نفسه لاURL أوstub. قيدmemory/browser/size المثبت يعرض دونsilentlypartialdownload؛ no indefinitewhile.
- Guest يشاهدLIVE/VOD، **يخفىdownloadbutton فقط**؛ لاDRM أو منعنسخ تقني مزعوم. المشترك المخول ينزل معrightsnotice.

**T/B ثمS محدودة:** loadworker/CSP/error/cancel، ترتيب/format/sizelimits، ثم إنتاجMP4 وتشغيله وصوت/seek/مدة مثبتة؛ يضم لجلسةplayer إن أمكن. no PASS منgreenCI وحده.

## 7. الحقوق والوثائق والقياس — داخل الوحدات الموجودة

كلا المتنافسين يجوزلهما إعادةنشرموادالمنافسة وتحقيقالربح؛ المشاهد يحتاجإذنالمنصة لإعادةالنشر. notice قربdownload في30؛ نصشروطversioned وآليةقبولموثقةللمشترك باستخدامmanaged_documents/H9 فيGUIDE-1/2 (38/39)، ثم قبولR4/R0. لاTerms UI وحدها تعنيقبولًا تعاقديًا، ولا صياغةنهائية مختلقة أوDRM أو بوابةدفعجديدة.

DB-MEASURE في34 يحفظDB-01 ويضيف metadata: rowsread/written لكلupload/confirmation/timelinepoll/seek/session وتزايدالمشاهدين؛ indexedranges/incrementalread/cache للpublicmetadata،لا مفاتيحprivatecache. indexwrites تدخلالميزانية. مثال5sلمدةساعتين=1440قطعة **مثال فقط ليسconfig**؛ لا عددDAU مجاني مضمون.

قرارMySQLالمستقبلي محفوظفي08؛ التنفيذ يبقىفي موضعقرارDB/hosting الموجود ضمنمتابعةDB/R0، وليس prerequisite للمقاطع أو تفويضنقلالآن. عندتفعيلالهجرة يجبإعطاؤهاUNIT وموضعفي14 معكلالبنودالمزاحة؛ لا مسارخفي. PortableModel الآن فقط.

## 8. تسليم القائد والتفويض

NEXT يقرأ من14 فقط؛ لقطة INDEX/SAFE القديمة تاريخية، وتحديث§9 هو عقد معالجة الإصدار. OWNER APPROVED لخطة/كود/اختبار هذهالمعالجات؛ تطبيقremoteDB/PHP/إعداداستضافة يحتاجartifactراجع وتفويضالنطاق وفق10/02، لا تغير credentials أوتحذفقطعًا. لاإعادةطلبقراراتالبنية/H7. نسخةupload.php المعطاةكافيةلتحليلها؛ اطلبنسخ الملفاتالأخرىمنزوعةالأسرارعندلزومinventoryفقط.

مرجعFFmpeg الرسمي: https://ffmpegwasm.netlify.app/docs/getting-started/installation/ ؛ مرجعD1pricing: https://developers.cloudflare.com/d1/platform/pricing/ . يستوثقالمنفذمنversions الفعليةوعقدworkerقبلالتنفيذ.

## 9. معالجة إصدار الصف28 — 2026-10-12 / مقترح PR فقط

هذا التحديث يصف الحادث والتصحيح، ولا يمنح إذن نشر أو تكليفًا جديدًا قبل اعتماد PR الخطة. UNIT `R4-RELEASE-RECOVERY-C` تابع لمعالجة28 (الموضع28.1)، وليس إعادة تنفيذ SAFE. UNIT `R4-PROFILE-SEC11-1` موضع28.2 قبل النشر الإنتاجي التالي. الصفوف29–43 لم تزح.

### الحالة والمصادر

MAIN `d778090edc339fc1e9f12c1dd06b1d2af1e164c6`؛ PR111/112 MERGED، وليس هذا إثبات DEPLOYED. Quality38176712697 SUCCESS وDeploy38176712714 FAILURE قبل pages deploy. PR113/ROW29 OPEN HEAD `ef7383a8633719beba420a87197e16f2110d45dd`؛ PR Quality38205955323 وPreview38205955359 SUCCESS، لا تثبت الصوت أوVOD أوproduction. PR110/HOLD HEAD `6e7ca1039484980affbcaf6f0eab548a82c35d17` محفوظة. Recovery C LOCAL بحسب تقرير المالك، HEAD المختصر222576e غير منشور؛ لا مراجعة مستقلة أواعتماد لكود غير متاح.

المقروء فعليًا منMAIN: manifest baseline0039،0040/0041 history-only،0042 غائبة،schema لا تغطيها؛ upload runbook يسمح Phase1/PHP القديم وfinalize ويقترحDROP/restore rollback. الملف الجديد فيRecovery محلي غير مقروء؛ إصلاح هذه العيوب يحتاج إثباتdiff مستقل، لا تقرير نجاح فقط. profile-page يقبل query token وsession_id عند حل own profile؛ middleware يعتمدBearer/sessionId. لا ادعاءاختراق أوفسادبيانات.

### 28.1 — R4-RELEASE-RECOVERY-C / ملكية واحدة

- نطاق: manifest/readiness/runbook، client lease والخدمات/الroutes اللازمة لتكاملها، مع الأخطاء503 الصادقة ورفضkeyless/stalegeneration/finalize غيرالمخول. لاplayer/download أو إعادة111/112؛ احفظ استخراجlease منPR110 وأثره.
- manifest يحصر0040/0041/0042 كrequired بأختامها الخام الصحيحة منGit المعتمد، مع جداول/أعمدة/فهارس يعتمد عليها الإصدار. history membership وحده لايكفي. preserve جميع الدبابيس التاريخية؛ لا تعديلSQL تاريخي أوhash لإخفاءcheckoutCRLF.
- integrity على **raw bytes**؛ ضبطcheckoutLF للملفاتSQL فيبيئةالفحص بدلnormalization فيsha256File. تعديلpolicy/اختبارلتغييرcontent يرفض؛ إثباتLF/CRLF وcontent mutation بمراجعGit، لااتهامخرقdocs18 كأنها تحدد خوارزميةhash.
- runbook مصحح: لا Phase «Worker آمن/PHP قديم يسمحkeyless»، لاcall serverFFmpeg أوحذفchunks، لاrollback بـDROP أوrestoreDB تلقائي أوPHPkeyless.
- حدودlease: acquire/heartbeat/expiry/takeover/reconnect مربوطةبالمضيففعليًا، والإصدار/الreceipt يفحصانالجيلالحالي والهويةالمخولة؛ لاوجودclass وحده دليلintegration.
- REQUIRED T/B: manifests missing/partial/applied/hashMismatch+schema coverage،lease failure/ownership/takeover/retry/finalize،client→PHPverifyHMAC/receiptcontract ببيئةمماثلةموثقة. REMOTE مستقلةexactHEAD/currentBASE؛ أيكودغيرمنشور BLOCKED SUBMISSION.
- لا S أوAstra لفحصschema/auth/Windows؛ PHP الحقيقي أوfaithfulequivalent للدليل الخارجي وفق§4، productionacceptance تسجلمنفصلة.

### 28.2 — R4-PROFILE-SEC11-1 / إصلاح محدد

- المصدر: الفحص المباشر لـprofile-page.ts علىMAIN؛ لا إعادةAuthphase أوالمالية. owner requested register before release؛ التنفيذ بعداعتمادموضعهفي14.
- إزالة اعتماد own profile علىsession query token وcookielegacy، باستعمالمصدرauthالمعتمد بدلمنطقينمختلفين. Bearer/sessionId الصحيح يعمل، session_id/querytoken وحدهما لايصادقان.
- حارسSEC11 يغطيقارئsessiontoken فيالصفحاتوالmiddleware، ويفرقemailverificationtokens وrealtimetickets المشروعة؛ لاحذفtokenqueryعام أوfalsepositive يدفعلتعطيلgate.
- تحديثحالةSEC11 الحقيقية فيAGENTS/CI وتعليقاتها ذاتالصلة فقط؛ لا تفعيل جميعcontinue-on-error أوتدقيق44publicroutes. لاحاجةsecretrotation عامة دونشاهدتسريبفعلي.
- DoD T/B: صالحBearer/cookie،غياب/invalidsession،querytokenalone مرفوض،مستخدمusername public صحيح،emailverify/ticket محفوظة،الحارسيلتقطقراءةجلسةURL. لاSQLأوProfileSavefeatureبالتكليف.
- ملكية: وكيلمستقللهذهالوحدة عندالتكليف؛ لايكلفوكيلRecovery/playerبها ضمنيًا. مشاركةWORKLOG/PLANSTATUS append بحفظالمدخلين؛ صف32PROFILE-SAVE محفوظبنطاقه.

### التبعيات وملكية الملفات

| العمل | الملكية والنطاق | الاعتماد |
|---|---|---|
|28.1Recovery|وكيلRecovery الحالي؛lease/client/routes/manifest/readiness/runbook؛PRبعدالنشر|SAFE28والINDEX27،صلاحيةrawhashوالcutover|
|28.2Profile|منفذمحددبعداعتمادالخطة؛profile/auth-source/SEC11guard/docsذاتالصلة|مستقلبالكود؛يجبضمنreleasecandidateقبلالنشرالتالي|
|29/PR113|وكيلplayer الحالي؛playlist/timeline/player/page/i18n واختباراتالنطاق|لاoverwritelease/client؛REMOTEبالتوازي،ثمrecheckالتكاملبعدRecovery|
|30/PR110|PR110المحفوظة؛downloadوالباقيالصحيحمنها|بعد28.1/28.2/29،لاتنزيلموازٍ|
|WORKLOG/PLANSTATUS|كلمنفذيسجلتغييره؛القائديفحصmerge يحفظمدخلاتالجميع|تعارضprepend ميكانيكيلاسببreset/stash/dropعمل|

ملكيةfiles تحددبالpaths الفعليةفيPRs قبلأيتعديل؛عندتعرضأيملفمشترككpage/Model تسلسلصريح،لافرض أنالتداخل دائمًاوثيقتانفقط. ROW29يبقىمحفوظًا ولاstashclaim من تقريرقديم؛ef7383a هوالدليل الحالي.

### ترتيب الدمج والإنتاج — لا تنفيذ من PR الخطة

1. نشرRecovery C والتحقق المستقل منexactHEAD، ومراجعةProfile المحدودة. ROW29 REMOTEبالتوازي؛ S الناقصةBLOCKED/PENDING لاPASS.
2. جهزcandidate/releaseSHA واضحًا يجمعRecovery+Profile قبلأينشرإنتاجي، وخطةmerge/deployمراجعة. ترتيبmergeالكود: Recovery ثمProfile، ثم29بعدزوالPOST-MERGE BLOCKED وتجديدتكاملالHEAD. **لا يسمحنشرRecoveryبينهما قبلProfile**؛ يجبحاجزنشرصريحمراجع،لااستغلالreadinessالفاشلةكتنسيقضمني. إذااحتاجتطريقةالدمجدمجProfileأولًالتجنبنافذة،يثبتالقائدالطريقةفيrunbookمعexactcandidateقبلالتشغيل؛لاbypass أوblindrerun.
3. readinessproductionقراءةفعلية: dueli-db/UUID/target وبaseline0039/hash/pendingexact0040–0042؛ الغيابأوالزيادةSTOP. لاافتراضproductionمنreport أوpreview.
4. احترام10 §9 التفويضالدائمداخلحدوده. حزمةثلاثهجراتبعددمججزئياتها/تغييرPHP/نافذةصيانة ليستتلقائيًاهجرةواحدةpending؛ يثبتالتفويضالمحددالموجودأويطلباعتمادالنطاقغيرالمغطى فقط. لاعادةسؤاللتفويضمطابقتحققتشروطه.
5. بعدartifact/runbook/REMOTE/CIوموافقةالنطاقاللازمة: حظررفعوتوثيقإنهاءخارجيقديمقابلللFFmpeg،drainلطلباتجارية،backupوحصرقبلالتغيير؛لاقطعنتيجةالمنافسة/cutoff. طريقةالحظرواستعادةالتشغيليحددهاالمشغّلولايفترضوجودswitchلميبن.
6. apply0040→0041→0042 بالترتيبوالتحققبعدكلخطوة؛ additiveلايشغلكودًاوحده ولاهيtransactionذريةواحدةمضمونة. لاsubsetactivation، ولاDDLrollbackآلي.
7. WorkercandidateالذييشملProfileعبرQuality/readinessثمPHPمحصنتحتحظرالرفع؛ ترتيبالتثبيتيمكنالتحضيرلهقبلًالكنلاتفتحخدمةغيرمتوافقة. لامفتاحHMACفيالمحادثة/الlogs ولاheadertrustمنCORS.
8. endpointقبولحقيقي: missing/wrongbinding/stalegeneration/replay/overwrite/receiptfailure ورفعصحيح→ready؛ تأكيدnoFFmpeg/nodeletion. ثمإعادةفتحالرفعوتحديثDEPLOYED/PROD VERIFIED.
9. فشلأيخطوة: إبقاءالرفعالمتأثرمحظورًا، حفظschemaوالchunks/history،fixforwardأوكودمتوافقمراجع؛ لاrestorelegacykeyless أوDROP. تعافيالنشرلايساويإغلاق29/S أوDB-01.
10. لاmergefeaturesلاحقةقبلQuality/DeployلنفسreleaseSHAوقبولخارجيلازم؛لاحاجةانتظاراكتملplayer29لتصحيحالإصدار،ولاحاجةلاعادةبواباتمغلقة.

### ما لا يتحول إلى تكليف

SQLالمحددفيControllers/BaseModelexceptions وSEC05/07/08/10 وG5/UNGUARDED وtsbuildinfo/importscript: تحفظ كملاحظاتتحتاجتتبعدليل/استثناء/إغلاققديم وتصنيف، لا implementationrows أوإزالةعشوائية. لا «آخرتعديلملف» كإثباتتاريخإدخالالمخالفة. Report .tmpمحذوفلايدعيكودمفقود؛ مايهمrawdiffوcontent محفوظ.

## 10. المسار الحالي المعتمد — الخيارB قبلالبيتا — 2026-10-12

**08قرارالمالكالأحدث نافذ:** يتقدمهذاالقسمعلى§6 «استكمالPR110نفسها» وعلى§9 الذيجعلقبولPHPبوابةتسبقكلتقدمميديا. لايعادclosedcode؛ترتيبNEXTوحالته في14فقط.

### ROW30 — PRنظيفة وحفظكلعمل110

ابدأمنMAIN130e18bأوأحدثبعدقراءةGitHub؛لاrebaseشاملل110 أونسخshared.tsالقديمفوق113. بطاقةالنقلداخلWORKLOG/PLANSTATUS:
- المستبدل:metadata111،lease/server112،clientlease/rawhash114،Profile115،player113؛ربطبpaths/commits.
- القابلللنقل:fetchretry/errors/cancel/assembly/UI/i18nواختبارات110المفيدة،معتصحيحها للعقودالحالية.
- المتبقيغيرالمستبدل:livecompatredirect،statuspublisher/automatictransitions/rolewiring والاستعمالالصحيحلصفحةالمنافسة؛تحققموضعيًاوانقلالصحيحضمننطاق30المعتمد،لاتسقطهبدعوى«110كلهاsuperseded».
- بعدوجودالبديلوcoverageواضحة يغلقالقائد110supersededبرابطPRالبديلةوالقائمة؛لايغلقالمخططالكودمنPRخطة،ولايفقدكلfeaturesذاتالنطاقغيرdownload.

DownloadService مستقلةعنloadedChunks/windowedcache:manifest ثابتللتنزيلمنDB،orderedreadychunks/duration/format/hash/size/finalstate وجميعصفحاتالمؤهل. liveavailableclipإنأتيحيميزعنcompletefinalrecording؛لاوعدملفكاملقبلfinalmarker أوحذفmissingبصمت. failed/gap/resumeformat/timestamps معلنة،ولاinventedمدة.

Remux دونreencode للcodecالمتوافق إذااثبتMP4seekable وصوتوصورةوتوقيتصحاح؛FFmpeg.wasmالمعتمد عندالحاجةمنown-origin package/worker/coreمتوافقةCSP. لاrawBlobconcat ولاغيرMIMEظاهر. WebCodecs+muxerبديلعميللدراسةمحدودةفقطإنمنعتهالموارد؛لالزومrebuildللبث.

الموارد:preflightestimate،fetchنافذةمحدودة،write تدريجية/تخزينمتصفحإذايدعم،تنظيفinputs/temp/objectURLs/worker،timeout/retry/cancelفعليأثناءfetch والمعالجة. سقف512MBالقديمليسownerproductpolicy؛لايعتمدكحدنهائيدونقياس،ولايخفىdownloadpartialعلىأنهfull. قيدمتصفح/ذاكرةمثبتيعرضAR/EN معمسارعملمناسب؛لاوعدغيرمقاسلتسجيلساعتينعلىكلجهاز.

Guestشاهدعاموالزرhiddenفقط؛تحققUIفيالحالاتالفعلية. loggeduserdownload معrightsnotice؛طرفاالمنافسةلهماrepublish/monetize،viewerبإذن؛الشروط/النسخة/قبولالمشتركضمنGUIDE38/39/H9القائمة،لاتنشأبوابةpay/DRM.

DoDمركز:mediaواقعMP4/WebM fixturesتوافقpipelineinitprepend،hostresume/gap/containerchanges،ملفطويلممثل،duration+seek+صوتالطرفينوصورتهما وnooverlapaudio،إلغاءcleanup/timeout/CSPfailednetwork،RTL/mobile/desktop. السلاسةالصوتية/الملفSمحددة؛T/BليسPASSMP4،ولاfullhistoricalsuiteإضافية.

### SEC07/08 وترتيبالحراس

-30.1 SEC07: حصرالقراءوالكتابالفعليةلsession_id/sessionId فيUI/AuthService/admin/advertiser وغيرهاالمتأثرة؛مصدرواحدومفاتيحصحيحة،لاتقدمالقديمعلىالجديد،حراسةnull/transient429/5xxبدونlogoutكاذب. serverroles/Auth/Ads/Finance لايعادبناءها. Profile115منجز.
-30.2 SEC08:HttpOnly/Secure/SameSiteكوكيويبخادميةبالخصائصالمناسبةللبيئة؛حددمسارlogin/logout/session/OAuth/expiry والحذف،لاJScookiewrite أوlocalStorage/State/windowلrawsessionsecret،ولافرضBearerعلىfetchالمتصفحبعدmigration. Server-to-serverHMAC والticketsمنفصلةولا تزال؛CSRFمتوافقويختبر،لااعتبارCORSمصادقة. تحققبقدرالتغيّرSSEticket/signaling/upload/admin/messages/rate-limit/sessiontransient والجلساتالمتعددة،لاإعادةكلالمنصة.
-API/appمستقبلية:لايفرضقرارHttpOnlyللويبإلغاءعقدBearerالشرعيلعميلغيرمتصفح،ولاعقودمستقبليةموازيةالآن.
-30.3:05corsallowlistموجودةفيmain؛10getWebSocketsموجودةوتجهيزغيرنشط. الحراسالحاليةgrepتلتقطcomments،فتصححبفحصتنفيذي/اختباراتسلوكموضعيةولايحذفgateلإسكاتها.07/08تتحولالحراسةذاتالصلةإلىمانعةبعدالإصلاح،لاكلgraceperiod مرةواحدة. SEC11إصلاح115منجز،تعليقاتCIالتاريخيةتصححلاexecutionجديدة.

### عيوبPHP/receipt تبقىضمن28 — لابوابةجديدة

بالقراءةعلى130e18b:runbookpatch يستدعيhelpersغيرمعرفة ولايرسlduration_ms؛file_exists→move_uploaded_fileغيرحصريبالسباق؛receiptcontractلايمرالgenerationأوفحصهعندready؛rollbackيتناقضمعnoDROP وfinalizeالخارجيمازالlegacytrigger. هذهعيوبمحددةلاتساويإعادةSAFEأوإثباتفشلproductionكلها.

يعالجالقائدمايتأكدداخل28/28.1 معrunbookوالاختباراتالمباشرة،ويمكنمتابعة30فيالوقتنفسه. لايوضع«ProductionAcceptancePhase»مستقلولاوقفكافةmergefeaturesلهذهالملاحظات. مايحتاجstorage/durationreceipt حقيقييشهدلهعندالجاهزيةويحفظقبول41؛لاreadyمصطنعولتسهيلالتجربة.

UPLOADS_FROZEN الحاليةتمنعإصدارمفاتيحWorker فقط،لاتضمنمنعkeylessPHPخارجيقديم؛لاتجعلهاgateلكلPR أوتفترضحالةsecretمنالكود. عندتغييراستضافةفعليمععيبمثبت،تحددخطوةالتطبيقالمحدودةوالتفويضالموجود،لاfreeze/maintenance افتراضيًالأعمالالتنزيل.

لاserverFFmpeg،nodeletion/overwrite،rawmigrationhash/readiness،LOCAL→REMOTE→merge→actualSHAQuality/Deployباقةالقواعدالقائمة. عودةDeployالأخضر لايغلقacceptanceالملفقبلشاهد؛وبنفسالوقتmissingPHPproofلايحظرالعملمسبقًا. المالكيريدسرعةإكمالماقبلالبيتاوأصغرإصلاحفعلي،لاقيودإصدارعاممبكرًا.

## 11. إغلاق الرحلة والاستعداد الخاص — اعتماد المالك 2026-10-14

**OWNER APPROVED:** اعتمد المالك الحزم الثلاث، والتحقق من وجود كل عيب وسببه قبل الإصلاح، والاستعداد الخاص لكل متنافس. هذا القسم وقرار 08 الأحدث يستبدلان ترتيب NEXT30 السابق. الترتيب والحالة حصريًا في 14؛ لا تنفيذ كود من المخطط.

### الأدلة وحدود الاستنتاج

CODE MAIN: `23b8b69baa56f57da5e8b76a363f7aaaaf8d48da`. PR116/117 مدمجتان؛ Quality 38431849525 وDeploy 38431849479 ناجحتان لنفس MAIN. ROW28 لم تصبح ACCEPTED بذلك.

المصدر تقرير المالك بتاريخ 2026-10-14 وعينة 2225 وملاحظاته:
- المقاطع المنزّلة تعمل. عدم ظهور طلبها في Console لا يثبت غياب الطلب؛ Network والمسار الفعلي يحسمان ذلك.
- Apache400 عولج بدعم الاستضافة ووصلت ملفات كبيرة؛ لا إعادة تحقيق عام في حجم الرفع.
- غياب 0001 من القائمة لا يثبت فقد التسجيل أو سبب توقف المشغل. ملف قفل صفري قد يكون طبيعيًا، وصلاحية 0600 وحدها لا تثبت 403.
- زر الضيف وRefresh واختلاف الأدوات أعراض يثبتها الوكيل على النسخة الحالية. اختلاف موضع الأدوات ورد حسب ذاكرة المالك؛ الصور لم تُقرأ لدى المخطط.
- أعراض التفاوض والاتصال وlease وready والنهاية في A–J محفوظة. لا قراءة مستقلة لإنتاج D1 من المخطط، ولا سبب مفترض واحد لكل الأعراض.

### شرط قبل أي إصلاح

لكل عيب، يسجل LOCAL على BASE الحالي والمسار والدور والحالة: **CONFIRMED** مع الدليل والسبب؛ **ALREADY DONE** بدليل؛ **NOT REPRODUCED**؛ أو **BLOCKED** مع المدخل الناقص. لا patch لكود سليم بسبب فرضية. عدم التكرار لا يمحو شهادة المالك أو يغلق الرحلة كلها.

التشخيص الأدنى داخل وحدة الإصلاح نفسها؛ لا PR تشخيص شكلية أو تدقيق شامل. الاستعداد الخاص متطلب معتمد: يعاد استخدام الموجود إذا وفّى بالعقد، وإلا يستكمل؛ لا يسقط تحت NOT REPRODUCED.

كل تكليف يلزم بقراءة AGENTS وdocs/01/11/13/17/18 وتعليمات الكود ذات الصلة وPLAN02/03/08/10/14/15؛ ويحدد UNIT وBASE وHEAD وملكية الملفات وDoD والتفويض. LOCAL ينفذ، REMOTE المستقل يراجع، والقائد ينسق ويدمج وفق 10 دون توسيع نطاق مستقل. T/B أولًا، وS لما يحتاج حكمًا بصريًا أو صوتيًا. لا إعادة اختبارات مراحل مغلقة لمجرد المزامنة.

### 28.3 — R4-LIVE-ENTRY-RECOVERY-1 / الاستعداد والدخول والتفاوض

يحفظ C/D/E/F/G وأصول التكامل 24/26 دون إعادة Phase7. تعديلات P2PConnection وSignalingManager وVideoCompositor وربط lease والصفحتين بحسب السبب المثبت.

**عقد الخصوصية:**
- معاينة محلية خاصة للمضيف والضيف؛ يرى كل طرف نفسه ويختار الكاميرا والميكروفون ويضبط الإعدادات المتاحة قبل النشر. تصميم الأدوات موحد، والإجراءات تختلف بحسب الصلاحية. لا محرر أو فلاتر تجميل جديدة من هذا الطلب.
- إذن getUserMedia ليس إذن نشر. **قبل الضغط الصريح لا يرسل المتنافس صوته أو صورته للخصم أو المشاهدين، ولا تدخل معاينته التسجيل أو الرفع أو التركيب العام.** إخفاء الفيديو أو كتمه محليًا مع استمرار sender لا يكفي.
- المضيف يبدأ المنافسة بحسب سلطته القائمة مع تأكيد نشره، والضيف يؤكد نشره/انضمامه بنفسه. انتقال الحالة إلى live ليس موافقة عنه. لا يضاف شرط يلزم ضغط الطرفين معًا لبدء المنافسة.
- الاستعداد ثم إجراء «بدء البث» واضح لكل طرف؛ قبل بدء المضيف يرى الضيف حالة انتظار صريحة، لا زر بلا نتيجة. الأخطاء والمحاولة مجددًا AR/EN.
- Refresh أو التعافي لا يكشفان وسائط جلسة جديدة دون إجراء صريح؛ لا PC/recorder/lease/polling مكرر. المعاينة ليست مشاهدة حية محتسبة للتقييم.
- الخروج من الاستعداد يوقف الأجهزة المحلية دون إنهاء المنافسة. اختبار الميكروفون محلي دون إرسال أو echo.

**التحقق المستهدف:** زر الضيف وRefresh والكاميرا واختلاف الأدوات؛ إجابات متكررة/متأخرة عند signalingState=stable؛ ontrack/start المكرر؛ timeouts و429؛ ربط lease بين /live وصفحة المنافسة؛ timers/listeners/generation/Retry-After. لا تنسب 429 polling إلى heartbeat بلا دليل، ولا تعطل rate-limit أو تعيد TURN.

**DoD:** منع الوسائط الخارجة والتسجيل قبل قرار كل طرف؛ معاينة وبدء/انضمام دون Refresh وبمرة واحدة؛ تعافي تفاوض وlease بلا تكرار؛ cleanup/backoff صحيحان. قبول بصري/صوتي مركز للمضيف والضيف AR/EN وعلى الهاتف؛ لكل إصلاح دليل السبب قبل التعديل.

### 28.4 — R4-CHUNK-VIEW-RECOVERY-1 / المقاطع واعتمادها وطلبها

بعد 28.3؛ يحفظ A/B/E وعقود 25/27/28/29 دون إعادة PRs الصحيحة.

تتبع عينة 2225 أو عينة حديثة حتى أول نقطة فشل:
dataavailable → enqueue → number/register → upload → ack/receipt → measured duration/D1 ready → playlist → player creation → stream request → decode/play.

سجل sequence وgeneration والتوقيت والحالة لأول وآخر مقطع دون أسرار. عند غياب 0001 ميّز pure-init المحتجز عن مقطع مرقم فشل، وعن resumeBase أو مسار/جلسة أخرى. لا تملأ فجوة بوسائط وهمية ولا تفترض سبب توقف المشغل. تشغيل الملف خارجيًا لا يثبت ready.

Range ونوع المحتوى والصلاحيات وCORS تفحص عند نقطة الفشل فقط؛ لا chmod عام أو نقل مسارات أو إعادة Apache400.

**DoD:** لكل رقم مصير موثق أو فجوة صريحة؛ الإقرار الفاشل بعد الحفظ قابل للتعافي دون overwrite؛ لا drop صامت أو enqueue غير مخول؛ مدة فعلية وready صادقة؛ القائمة والمشغل يطلبان القطع الصحيحة ويعمل LIVE/VOD على العينة. لا انتظار مؤبد لمقطع مفقود؛ retry محدودة بحالة مرئية. أمان PR116/117 وتوافق upload-config/storage محفوظان.

### 28.5 — R4-LIVE-END-RECOVERY-1 / النهاية والحالة والتعافي

بعد 28.4؛ يحفظ H/I/J. يقدم فقط status publication/transitions/role wiring/live compatibility اللازمة من 15 §10 وPR110. **التنزيل والتجميع والحقوق تبقى في ROW30.** يفحص الموجود وينقل الصحيح أو يكتب أصغر تكييف على MAIN؛ لا يدمج HEAD القديم لـPR110.

- /end لا ينتظر destroy/drain انتظارًا غير محدود، وفشل destroy لا يمنعه. حفظ آخر dataavailable وdrain المحدودة وlease يتسق مع cutoff والنتيجة والمال؛ لا حذف الانتظار دون حفظ الذيل المخول.
- نشر الحالة لكل الأدوار في النهاية اليدوية والتلقائية؛ listener يحدّث الواجهة. عند انقطاع SSE يستعيد GET الحالة الرسمية. الخروج من جلسة أو انقطاع المضيف ليس نهاية.
- الانتقال دون Refresh إلى VOD/processing/not-recorded الصحيح؛ متابعة ready منضبطة، دون spinner دائم أو listeners/recorders مكررة.
- مسار التوافق يحترم الاستعداد وينقل للمكون الموحد، مع بقاء صفحات الاختبار؛ redirect لا يبدأ الكاميرا أو التسجيل دون القرار الصريح.

**DoD:** طلب النهاية دون انتظار رفع فاشل طويل؛ وصول الحالة لكل دور دون Refresh؛ نهاية idempotent وحفظ آخر المقاطع المخولة؛ لا بث وهمي أو نهاية بانقطاع؛ انتقال LIVE→VOD مثبت.

### إغلاق الرحلة وحفظ بقية المسار

ثلاث حزم، لا عدد PRs مفروض؛ يجمع المتماسك مع ملكية واضحة دون منفذين متداخلين. LOCAL ثم REMOTE لكل PR وفق 10، دون تجاوز متطلباته أو تسمية queued/pending نجاحًا.

قبول واحد للرحلة المعدلة: استعداد ونشر صريح؛ اتصال الطرفين؛ المقاطع والتخزين وready؛ مشاهد LIVE ثم VOD؛ انقطاع المضيف والاستئناف؛ نهاية لجميع الأدوار دون Refresh أو انتظار رفع فاشل. BLOCKED لمدخل/جهاز ليس PASS ولا عيب منتج مثبتًا.

ROW28 تصبح ACCEPTED بعد حسم الحزم والقبول، ثم ROW30 بالخيار B. ROW41 يحفظ القبول النهائي ولا يكرر جلسة سليمة بلا تغيير أو عيب جديد. ad-placeholder404 في 35 منخفض الأولوية، وDB-MEASURE34 لميزانية المنصة. لا إعادة Phase7/Finance/Ads/R1/H7 أو الفهارس المغلقة.

## 12. نتائج تجربتي البث وتعديلات المالك — معتمد 2026-10-19

**OWNER APPROVED:** اعتمد المالك مقترح المعالجة والتوزيع بعد المناقشة، مع تعديلين ملزمين: أشكال وألوان أدوات البث تطابق صفحات الاختبار المحفوظة، و«المشاهدة لاحقًا» وسجل المشاهدات يظهران في قسم خاص داخل بروفايل صاحبه. المرجع 08، والترتيب الوحيد في14. هذا تحديث خطة لا تنفيذ كود/استضافة/D1.

### 12.1 الحالة ومصدر الأدلة

- CODE MAIN `ce5e0e728dfbac59f3cd1f4e15508e2c374fe6fe`. PR118 (28.3) MERGED إلى `dcb56c707dd1d9dd06e7f1c1d9a157a427c0ca18`؛ PR119 (28.4) MERGED إلى MAIN الحالي. Quality [38733693451](https://github.com/Maelsh/dueli-opus/actions/runs/38733693451) وDeploy [38733693448](https://github.com/Maelsh/dueli-opus/actions/runs/38733693448) SUCCESS لنفس MAIN.
- PR119 أصلحت انتقال علامة finalized إلى مشغل LIVE وإنهاء انتظار أول مقطع عند نهاية تسجيل بلا مقاطع قابلة للتشغيل. يحفظ الإصلاح؛ لا يعمم بأنه أغلق كل spinner أو قبل رحلة الإنتاج.
- تقرير المالك عن منافستين حيتين، ومنها «منافستي للتجربة12»، وصور15أكتوبر هو مصدر الأعراض. فحص المخطط عينة من الصور الأصلية والكود على MAIN؛ ليس اختبار وسائط مستقلًا ولا قراءة D1 إنتاجية. لا ادعاء فحص جميع الصور أو أن كل اللقطات من نسخة متصفح واحدة.
- موجه قائد التنفيذ الذي قال إن28.4 لم تُدمج أصبح قديمًا؛ GitHub يثبت الدمج. WORKLOG/PLAN-STATUS تحتويان سجلات ما قبل الدمج؛ يحتفظ بتاريخها مع إضافة حالة أحدث صادقة. 28.3/28.4 CODE MERGED/DEPLOYED لا تعني ACCEPTED.
- التحقق قبل patch في§11 باقٍ: تقرير المالك دليل عرض، لا إثبات تلقائي للسبب. ALREADY DONE/NOT REPRODUCED محليًا لا يمحوان فشل الإنتاج ولا يبرران إعادة بناء مكون صحيح.

### 12.2 حصر التقرير كاملًا وربطه بالمسار

هذه معرّفات تتبع للأعراض/المتطلبات، وليست PR لكل صف. كل معرّف يأخذ disposition ودليلًا موضعيًا وفق§11.

| ID | الملاحظة/المتطلب | الموضع والحد |
|---|---|---|
| O19-01 | القبول وتغير الخصم/الحالة لا يظهران دون Refresh؛ زر البداية يتأخر |28.3.1؛ تحديث الحدث والحالة وGET resync دون إعادة الدعوات J |
| O19-02 | start ينقل إلى /live ورابط join-live ظاهر؛ المضيف والضيف في واجهتين |28.3.1 مع توافق28.5؛ صفحة المنافسة هي الإنتاج، اختباراته لا تحذف |
| O19-03 | شهادة انتقال الوسائط قبل ضغط النشر |28.3.1 أولوية خصوصية؛ أثبت المصدر والجلسة والموافقة والوسائط الخارجة؛ صورة ثابتة أو وجود زر لا يثبتان السبب |
| O19-04 | أشكال/ألوان/اكتمال الأدوات وغياب شرح واضح ونص داخل الأزرار |28.3.1 وفق صفحات الاختبار في§12.3؛ بقية UX العامة في35 |
| O19-05 | غياب التكبير داخل الصفحة وملء الشاشة وتبديل الكبير/الصغير؛ ظهور مربع إضافي؛ حجم/موضع/زوايا غير مناسبة |28.3.1؛ عرضان فقط مع تبديل آمن ونافذة صغيرة متحركة قابلة للإخفاء وحجم نسبي |
| O19-06 | LIVE قبل النشر، زر إنهاء في الاستعداد، نص نشر زائد؛ أدوات لا تتغير بعد النشر |28.3.1؛ حالات نشر منفصلة؛ نهاية المنافسة وفق صلاحياتها القائمة ولا تغيّر سياسة الخادم بالصمت |
| O19-07 | كشف عدد القطع/الرفع/التحميل وmedia:waiting للمستخدم |28.3.1 لأدوات المرسل و28.4.1 للمشغل؛ diagnostics خارج الواجهة العادية |
| O19-08 | سهم الرجوع أثناء البث بلا حماية |28.3.1؛ تحذير مغادرة وتنظيف، لا حبس مستخدم ولا end بسبب الرجوع |
| O19-09 | فشل مشاركة الشاشة؛ اشتراط كاميرا وميكروفون؛ رسالة خطأ مضللة |28.3.1؛ مصدر شاشة مستقل أثناء الاستعداد دون نشر حتى الموافقة |
| O19-10 | الطرف الآخر يبقى يبث بعد /end؛ واجهات التقييم تبقى مفتوحة |28.5؛ تحديث جميع الأدوار ووقف الوسائط وإغلاق التقييم؛ رفض الخادم للتقييم بعد النهاية سلوك صحيح يحفظ |
| O19-11 | المتنافسان لا يشاهدان تسجيلهما بعد النهاية |28.5؛ اختيار سطح VOD بعد النهاية لجميع الأدوار؛ التنزيل نفسه في30 |
| O19-12 | الشريط يقفز بزمن مقطع بدل التسجيل، اختلاف4:10 و0:13 |28.4.1؛ زمن كامل موحد، تحقق واجهة المستهلك مع المشغل لاModel وحده |
| O19-13 | قطع متفاوتة المدة/الحجم؛23 مقابل22؛24/24 في الأخرى |28.4.1؛ مقارنة IDs/الحالات/المدد والفجوات؛ اختلاف الحجم أو أعلى sequence ليس إثبات فقد |
| O19-14 | تحميل محدود حول الموضع؛ عدم تكرار الطلب عند الرجوع |28.4.1؛ ذاكرة محدودة وتخزين متصفح متاح، لا fetchALL أو احتفاظ كامل مؤبد |
| O19-15 | زر التنزيل لا يكمل تحميل بقية المقاطع ولا ينتج الملف |30 بالخيارB؛ مستقل عن cache المشغل؛ لا تقديم تنزيل أو دمج110 القديم |
| O19-16 | شعار إنجليزي مسجل في منافسة عربية مقابل شعار صحيح في الأخرى |28.3.1؛ تثبيت لغة الهوية عند تركيب التسجيل، لا تغيير تسجيل قديم |
| O19-17 | عرض حصيلة التقييم بالأرقام غير مناسب؛ طلب شريط بلونين وعدد المقيمين وشعارين |35؛ تغيير عرض فقط وفق§12.7 دون تعديل الفوز/H7 |
| O19-18 | ذكرني ظاهر على مكتملة؛ أيقونة فقط؛ ما أثره؟ |35؛ تذكير موعد مجدول مستقل عن شاهد لاحقًا؛ حراسة خادم/واجهة وتسليم الإشعار وفق القائم |
| O19-19 | مشاهدة لاحقًا ومكانها في بروفايل صاحبها |32.1؛ متطلب معتمد، تفاصيل13 §8؛ لا خلط reminders أو likes |
| O19-20 | سجل مشاهدات المستخدم ومكانه في البروفايل |32.1؛ إعادة استخدام WatchHistoryModel والعقود الصحيحة، لا إسقاط أهلية التقييم |
| O19-21 | Stream not available/media:waiting، أسود/تحميل، LIVE ظاهر مع VOD |28.4.1 للطلب/التشغيل؛28.5 لانتقال الحالة؛ افصل overlay الواجهة عن أي LIVE مطبوع داخل التسجيل |

### 12.3 28.3.1 — R4-LIVE-ENTRY-RECOVERY-REM1

**التبعية:** PR118/119 مدمجتان؛ لا إعادة تنفيذهما. متابعة قبول محددة للأب28.3 وبنود O19-01..09 وO19-16، مع حفظ DoD§11.

**مرجع التصميم الملزم من المالك:** ملفات الاختبار الموجودة:
- `src/modules/pages/live/views/host.ts`
- `src/modules/pages/live/views/guest.ts`
- `src/modules/pages/live/styles/test.css`

ينقل شكل الأدوات والأيقونات وألوانها وحالاتها من هذه المراجع إلى المكون الإنتاجي؛ لا تصميم جديد من الوكيل ولا نسخ منطق اختبار قديم. مصدر الشاشة أزرق، الكاميرا بنفسجي، تبديلها نيلي، الميكروفون أخضر، السماعة فيروزي، إظهار المحلي رمادي، وأفعال البدء/التعافي/الإيقاف بحسب حالات المرجع الأخضر/الكهرماني/الأحمر. المرجع الفعلي يحدد الأصناف والأبعاد والأيقونات؛ العناصر الجديدة تستعمل نفس نظامه. يراجع الوظائف المقابلة، ومنها صوت الخصم وإخفاء المحلي، دون إظهار أداة غير عاملة. أيقونات فقط داخل الأزرار مع title وaria مترجمين وfocus واضح؛ tooltip مناسب للهاتف/لوحة المفاتيح عند الحاجة. لا تظهر إحصاءات القطع أو أدوات debug.

- المنافسة pending/accepted/live/completed مصدرها الخادم، بينما المستخدم قد يكون مستعدًا ولم ينشر بعد. حدث القبول والحالة يحدث الواجهة والأفعال دون Refresh؛ SSE القائم مع GET resync محدود عند التعافي، دون WebSocket جديد أو poll سريع. تحديث عنصر لا يعيد PC/recorder أو يهدم مصدر المعاينة.
- لا start redirect إلى واجهة بث ثانية. صفحة المنافسة نقطة الإنتاج الوحيدة. يحسم توافق /live/:id مبكرًا بالقدر اللازم لهذه الرحلة؛ إكمال انتقالات النهاية في28.5. صفحات host/guest/viewer الاختبارية تبقى متاحة منفصلة، ولا ينسخ منطق بث موازٍ.
- مبدأ§11 نافذ: لكل طرف معاينة وموافقة نشر مستقلة؛ إذن الجهاز/قبول الدعوة/دخول route/حالةlive/Refresh لا تنشر بدلاً عنه. اختبر track/sender والوسائط عند الطرف الآخر والتسجيل بعلامة مصدر واضحة قبل وبعد موافقة كل طرف. افحص الجلسة الفعلية والمستدعين بدل افتراض أن رؤية remote تعني أن المحلي أرسل.
- الاستعداد يعرض علامة صفراء/كهرمانية وحالة مفهومة. LIVE للمنافسة لا يدعي أن المستخدم ينشر. لا أفعال بث مضللة أو زر نهاية قبل بدء المنافسة؛ ما يلزم إتاحته أثناءlive يحترم حق الطرفين في الإنهاء القائم. إزالة النص الزائد بجوار النشر دون إلغاء الأخطاء الضرورية أو شرح الوصول.
- مصدر الوسائط يختار في الاستعداد: كاميرا و/أو ميكروفون بحسب المتاح، أو شاشة دون اشتراط أي منهما. التقاط الشاشة بإجراء المستخدم معاينة محلية حتى النشر؛ يعاد ربط المصدر عند التبديل أو stop-sharing دون نشر خفي أو فرض عودة للكاميرا المفقودة. دعم صوت الشاشة حسب قدرات المتصفح، لا وعد بصوت غير متاح ولا تغيير قواعد حسابات AI.
- الأدوات موحدة للطرفين مع اختلاف الصلاحيات. وضع عادي، وتوسيع داخل الصفحة مع تخطيط يناسبه (نحو نصف الشاشة حيث يسمح المقاس)، وملء الشاشة. صورتان فقط، والتبديل يبادل دوريهما لا ينشئ عنصرًا ثالثًا؛ الصغيرة فيها إجراء تكبير/إعادة وتصغير وإظهار/إخفاء، وتتحرك داخل حدود الفيديو وحجمها يتناسب معه على الهاتف والسطح. التبديل البصري لا يبدل هوية المضيف/الضيف أو مصادر التسجيل والصوت.
- الرجوع أو المغادرة أثناء النشر يعرض تحذيرًا مناسبًا حيث يسمح المتصفح، وينظف الوسائط/المؤقتات. لا منع مطلق للمغادرة ولا end للمنافسة من beforeunload. قبل النشر يمكن الخروج من المعاينة دون إنهاء المنافسة.
- هوية التسجيل بحسب لغة واجهة المضيف المعتمدة، لا استنتاج من أسماء الطرفين. مرر app_title/rtl للشعار في كل مدخل فعلي؛ /live الحالي لا يمررهما وVideoCompositor يرجع إلىDueli. ثبّت السبب بعينة واحفظ التسجيلات القديمة.

**DoD T/B ثم S موضعية:** رابط القبول وstart الحقيقي؛ معاينة/نشر مستقلان للطرفين؛ شاشة دون أجهزة؛ أدوات المرجع العاملة؛ تبديل/إخفاء/تحريك/توسيع دون فقد tracks أو consent؛ شعار صحيح؛ AR/EN وRTL/mobile/dark/keyboard في الجزء المعدل. لا تعادTURN/Finance/Ads. اختبارات mock أو صورة ثابتة لا تغلق شهادة تسرب وسائط.

### 12.4 28.4.1 — R4-CHUNK-VIEW-RECOVERY-REM1

**التبعية:**28.3.1 للرحلة الوسائطية؛ تحضير قراءة metadata ممكن دون تكليف متداخل. الأب28.4 وPR119 محفوظان. نطاق O19-07/12/13/14/21 وDoD§11.

- تتبع أول نقطة فشل من القطعة إلىready والقائمة وطلب المشغل وفكها؛ لا تطلب إعادة رفع ملفات المالك لمجرد غياب console. S جزئية ناجحة لا تعني صحة كل المقاطع.
- كشف الكود: embeddedSetupVodControls يفضّل videoEl.duration/currentTime، وهما للمقطع الحالي، ثم يمرر target إلىseekTo الذي يتوقع زمنًا كاملًا. يستخدم حدث المستهلك زمنًا عالميًا واحدًا: بداية المقطع الموثقة+موضعه؛ الإجمالي من فهرس التسجيل، لا مدة videoElement ولا مدة المحمّل فقط. start/seek/replay وحركة الشريط والتعليقات المؤقتة تتفق مع المرجع نفسه.
- يحفظ ms→s مرة واحدة، ويستخدم مدة كل قطعة الفعلية وحدودها؛ لا توزيع متساوٍ لمجموع المدة إذا توفرت مدد مختلفة. يحفظ خط LIVE المتزايد والرجوع والعودة للحافة؛ VOD بداية/منتصف/نهاية. ضبط listeners والـdouble-buffer يمنع إعادة ربط الزمن القديم بعد التبديل أو rapid seek.
- لا يُفرض تساوي حجم القطع أو مدتها تمامًا. cadence تسجيل مستهدفة مع قياس الانحرافات الكبيرة والتوقف/الاستئناف، لا timeslice مفترض مرجعًا للمدة. رقم مثل4/24 فيonProgress يعني موضع القطعة/عدد القائمة، لا22 ملفًا محملًا. قارن sequence IDs وعدد الصفوف المؤهلة/الفاشلة/الفجوات والملفات الفعلية قبل وصف فقد. لا حذف gap أو اختلاق قطعة لتطابق العداد.
- نافذة جلب افتراضية: الحالي+سابق+اثنان تاليان؛ تعديل محدود إلىثلاثة تالين عند حاجة تشغيل مقاسة، لا تحميل كامل تلقائي. dedupe يشمل طلبًا قيد التنفيذ؛ يحتفظ بالمحمّل داخل الحدود ويستعمل browser cache/storage المتاح للعودة دون طلب مكرر غير لازم. لا ذاكرة متنامية بلا حد ولا ضمان تخزين دائم بكل متصفح.
- إعادةseek تحرك نافذة التحميل إلى الهدف؛ تمنع الاستجابات المتأخرة من إعادة نافذة قديمة أو تلويث cache. لا يتم تنزيل MP4 الكامل من زر المشاهدة أو لتهيئةseek.
- حالات waiting/error/processing/unavailable/playing واضحة مترجمة؛ لا media:waiting أوchunk counts في واجهة المستخدم. افصل LIVE المطبوع داخل صور التسجيل عن شارة المشغل؛ التسجيل المكتمل لا يعرض أدوات/شارة LIVE خاطئة.

**DoD:** مقاطع ممثلة بمدد مختلفة، seek عبر حدودها وبعيدًا عن نافذة البداية، زمن كامل صحيح قبل تحميل الجميع، rapid seek/فشل شبكة/رجوع لا يكرر الطلبات بلا حاجة، نافذة memory/network محدودة، LIVE→rewind→live وVOD بهوية الأدوار الصحيحة. T/B على الربط المنبعث الفعلي ثم S للصورة/الصوت والسلاسة فقط؛ لا قبول منModel أوAPI وحده.

### 12.5 استكمال28.5 — النهاية لجميع الأدوار

أضف O19-10/11/21 إلى§11 دون UNIT مكررة. /end وcutoff مستقلان عنdrain، وتحديث الحالة يصل للطرف الآخر والمشاهد دونRefresh. توقف الإرسال/الأجهزة والأدوات المناسبة بعد قرار النهاية، ولا ينتظر كل طرف ضغطend منفصلًا. SSE+GET resync يستعيد الحالة بعد الانقطاع.

بعد النهاية يعامل المضيف والضيف كمشاهدين للتسجيل. احذف الاستثناء المنطقي الذي يمنعهما من initEmbeddedViewer فيcompleted، مع عدم تشغيل صوت الجمهور لهما أثناءP2P الحي. VOD/processing/not-recorded من قائمة وحالة صادقتين، لا منالدور القديم أوvod_url وحده. زر التنزيل للدور المخول يربط بالخدمة30 عند إنجازها؛ لا ادعاء إصلاحه هنا.

واجهة التقييم تغلق فور الحالة الرسمية وتثبت الحصيلة؛ رفض الخادم للتقييم المتأخر محفوظ ولا يعاد بناءR2-V أوالمال. التعليقات تبقى وفق08. manual/autoend، انقطاع مضيف ليسend، آخررفع مخول محفوظ.

### 12.6 ROW30 محفوظة — لا تقديم للتنزيل

العيب المحدد فيMAIN: mergeChunks ينتظر isFullyLoaded بينما SmartVodPlayer يخليcache خارجنافذته؛ قد لا يكتمل الانتظار أصلًا. ليس الحل تحميل كل التسجيل أثناء المشاهدة أوإلغاءحدالذاكرة. OptionB وDownloadService المنفصلة وملفMP4صالح/progress/cancel/retry/حقوق/Guest تبقى§10. تحميل الباقي عند طلب التنزيل، إعادة استعمال البايتات المتاحة بأمان، وتجميع عميل لاserverFFmpeg. PR110 تحفظ حتىحصرالنقلوالبديل؛ لا دمجرأسها القديم.

### 12.7 ROW35 — العرض والتذكير، مع حفظ بقيةUX

- حصيلة النجوم شريط بلون لكل متنافس وفق **مقياس النتيجة/الفوز المعتمد**؛ لا تغيير للفائز أوH7. نجوم الإدخال تبقى كما هي. حالة مؤقتة أثناءlive ثم نهائية، وصفر/تعادل واضحان. تحته عدد المقيمين الفريدين للمنافسة، لا جمع صوتي الشخص إذا قيّم الطرفين، وبين شعاري ديولي. لا عداد مختلق منAPI لا يحمله؛ استكمل أصغر قراءة Model إذا لزم. AR/EN وRTL وkeyboard/contrast.
- تذكير الموعد مستقل عن «المشاهدة لاحقًا». تحقق مما ينفذ فعلًا: الموعد المجدول، الوقت القائم (30دقيقة افتراضيًا)، الحفظ/الإلغاء، والإشعار بالقناة القائمة. تتبعendpoint المركب والكرون/التسليم بأقل نطاق؛ وجودScheduleController لا يثبت وصول الإشعار.
- reminder أيقونة فقط معtitle/aria؛ إخفاء/تعطيل غير المؤهل علىlive/completed وفق العقد وحراسة الخادم. لا قاعدةpending-only جديدة تستبعدaccepted scheduled. جميعU/N/I/VIS/DATA والـ34موضعًا السابقين محفوظة.
- لا تؤخر إصلاح خصوصية البث بعرض الحصيلة أوالتذكير؛ موضعهما35. قوائم البروفايل32.1 وتفاصيلها13§8.

### 12.8 أقل تحقق وإغلاق

لا تدقيق شامل أوPR لكل عرض. LOCAL يثبتbad path قبلpatch، وREMOTE مستقل وفق10. بعد الحزم، قبول واحد يجمع طرفين ومشاهدًا، والقبول دونRefresh، والنشر المنفصل، ومصدر شاشة دون أجهزة، والمقاطع والزمن والقفز، ثمend واحدًا وتحول جميع الأدوار للتسجيل. اختبار المنطق والشبكة آليًا أولًا؛ S للصوت والصورة والحكم البصري. التنزيل وشاشات32.1/35 تقبل عند موضعها؛ BLOCKED بيئي ليسPASS.

كل المتطلبات الماضية محفوظة. الثوابت: no serverFFmpeg/no deletion/no overwrite؛ تسجيل المضيف، انقطاعه ليسend، resume append؛ H7 وKEEP NOW؛ لا تغييرDB/استضافة من تحديث الخطة. الترتيب التفصيلي في14 فقط.

## 13. اعتماد20أكتوبر — FV2230 وتصحيحه وخريطة التحقق

**OWNER APPROVED — 2026-10-20.** المصدر: تقرير FV2230 واستكمال أدلة التسجيل، والصور15/16/23/24/25، وموافقة المالك على المتابعات المحددة. هذا القسم يصحح الاستنتاجات المتعارضة في التقرير الأول، ويكمل §§11–12 دون إسقاط متطلب أو إنشاء UNIT جديدة. ترتيب وحالة العمل في14 فقط.

### 13.1 حدود الأدلة والتقدم المحفوظ

- CODE BASE التجربة `38ffa575e34d6912818f1ebc9e0a1a761d110da4`، بعد PR120/28.3.1 (`2abf5ade279804d1ec07a4ece22cbf810b4c50ba`) وPR121/28.4.1. Quality39416835180 وDeploy39416835145 SUCCESS علىactual main. شاهد النشر لا يساوي قبول رحلة28.
- تقرير الوكيل يثبت مطابقة app.js محلي/إنتاج، 154 قطعةready وتشغيل LIVE/VOD بمصدر المضيف. هذه نتائج تشغيلية محدودة؛ لا تثبت تسجيل الطرفين والصوت والسلاسة أو كل المتصفحات.
- نجاح أدوات المرجع والتبديل والتوسعة، المعاينة/مصدر الشاشة، لغة الشعار، إزالة البيانات التقنية، الإجمالي من الفهرس، القفز والنافذة المحدودة يحفظ. يتحقق المراجع مما يتأثر بالتعديل فقط؛ لا إعادة PR120/121 أوكل أدواتها.
- الهيدر وسط الصفحة أثر full-page screenshot في التجربة، ليس إصلاحCSS مفوضًا. null/@null لم يعد إنتاجه في2230؛ يبقى الدليل التاريخي ولا يعتبر FIXED بلا سبب/دليل. أسماء[QA] أسماءعرض وليست بذاتها تسرب دعوة.
- R1 في التقرير = عمى مؤشر الإشارة المشروط بتراكم أحداث مصفاة؛ لا يعني فشل كل منافسة تاريخيًا. R2 =showToast في مسار النشر؛ المقارنة حددت إدخاله بين نشر المصدر والتفاوض فيPR118، ولا تحدد إصدار نجاح المالك السابق. لا bisect/تجربة جديدة لمجرد تسميةregression.
- قطعة0050 المحفوظة بحسب ffprobe في الاستكمال **MP4/ISO-BMFF حقيقية، VP9+Opus**؛ دعوىWebM باسمMP4 ملغاة. الطوابع تبدأ قرب517.74s والوسائط نحو10.38s؛ تعريف duration/start/seek يجب قياسه، لا فرض فساد الحاوية أوتحويلها.
- لا طلبfinalize شبكي متوقع في التصميم الحالي: finalize المحلي يصرف الرفع، والنهاية الخادمية تسجلmarker. لا دليل محفوظ على طلب404 أوplaylist النهائية؛ لا يثبت فقد بيانات أوfinalized defect. تتبع التصريف/الإيصالات/العلامة الفعلية أثناء الإصلاح؛ لا اختراعendpoint finalize أوعودةfinalize.php.
- ملاحظةR6 «offer يسقط صامتًا» فرضية مدعومة فقط؛ conn/ICE/new أوsignalingState=stable فيلقطة لا تثبتان وحدهما عدم استلامoffer عبر التاريخ. الشبكة الكاملة/النداء الفعلي هي الدليل المطلوب.
- شهادة المالك بنجاح تسجيل الطرفين سابقًا محفوظة. غيابremoteVideo في2230 يبرر إصلاح النشر/الإشارة أولًا، ولا يثبت سلامة كل حالاتcompositor ولا يفوض إعادة بنائه.

### 13.2 مصفوفة تحقق قبل الإصلاح وبعده — ملزمة في LOCAL وREMOTE

T/B = كود/اختبارمنطق/شبكة أرخص؛ S = متصفح/وسائط فعلية وحكم بصري أوصوتي عند الحاجة. لا تكليف جديد شامل للمختبر قبل الإصلاح. **LOCAL يتحقق قبلpatch ضمن مهمة الإصلاح نفسها؛ REMOTE مستقل يتحقق بعد التنفيذ علىexact HEAD.** يسلم قائد التنفيذ مقتطف الأدلة اللازمة أوالتقرير نفسه، ولا يفترض أن ملفات qa المحلية متاحة للجميع. missing evidence يوسم BLOCKED/UNKNOWN موضعيًا، لا PASS ولا إسقاط بند.

| ID / موضع | ما يثبت قبلpatch ومن المسؤول | بعدالتنفيذ — REMOTE مستقل وما يحتاجS |
|---|---|---|
| FV20-SIG /28.3.1 | LOCAL/T-B: trace منالroute المستدعاة إلىgetAfter/visibleSignals ومؤشرالعميل؛ إثبات نافذة50حدثًا غيرإشاري، والمستلم الصحيح؛ لا اختبارTURN جديد | T/B: تقدم المؤشر حتىمعsignals فارغة، الوصول لإشارة خلفدفعاتمصفاة/موجهةللغير، استمراردفعات محدودة، reconnect/replay وعدمضياع/تكرار، حفظالصلاحيات؛ ثمS موضعية ضمنرحلة28 لإثبات اتصالطرفين |
| FV20-TOAST /28.3.1 | LOCAL/T-B: تنفيذpublishMedia الفعلي وإظهارReferenceError وترتيبالتفاوض؛ النطاق المقصودwindow.dueli/تعريفمحلي آمن وفقالمشروع لا إصلاحاسم افتراضي | تنفيذsuccess/error الفعليين بلاReferenceError أوإخفاءالخطأالأصلي؛ offer/requestReoffer بعدالموافقة، لااكتفاءبحثنصي؛ باقيجردtoast في35 ويحذفمنهفقطماوثقإصلاحه |
| FV20-OFFER /28.3.1 | LOCAL/T-B: تتبعsendSignal/manager lifecycle/isConnected وofferInFlight معشبكةغيرمقصوصة؛ لاpatchللسباقالمفترض قبلإثباته | إنثبتأصلحموضعيًا واختبرjoin/reconnect/نشرمتقارب وعدمsilent drop؛ وإنلميثبتسجلNOT REPRODUCED/UNKNOWN ودليلًامحددًا ولايمنعقبولالرحلةالسليمةلمجردفرضية |
| FV20-REPLAY /28.3.1 | LOCAL/T-B: تثبيتإعادةإشعاراتقديمةعندالتحميل، وفصلقناةالمستخدمعنsignaling وسياسةlast-event-id القائمة | تحميل/إعادةاتصاللاتنتجانتوستدعوةقديمةكجديدة؛ الحدثالجديديصل، unread/history يبقيان، replayاللازمللتعافيمحفوظ؛ لاتعليمجماعيقديممقروءبديلًاولاإعادةcleanup37 |
| FV20-PAIR /قبول28.3.1 ثم28 | LOCAL: مصدرانمميزان وموافقةنشرمستقلة، offer/answer وontrack/RTP ثمremoteVideo ثممدخلcompositor؛ لاتحكمالمركبمنإطارواحد | S واحدةمحددة: يرىكلطرفمصدرالآخر، ويظهرالمصدرانللمشاهدوالتسجيلمعصوتيهما بلاecho؛ حفظالخصوصيةقبلالنشر؛ المصادرالمزيفةالمميزةصالحةللمسارلكنلايعادلذلكاختبارأجهزةبشريةإنلمتستخدم |
| FV20-TIME /28.4.1 | LOCAL/T-B: عينةMP4بطوابعغيرصفرية، currentTime/MSE مقابلraw timestamps والفهرس؛ تمييزmediatime عنcompetition time وdurationالفعلية | الزمنالحاليلايجمعoffsetمرتين، totalمنالفهرس، seekبداية/حد/بعيد/سريع، LIVErewind→edge، تعليقاتالزمن، تبديلعناصر/صوتونافذةمحدودة؛ S للصوتوالانتقالفقط؛ لااشتراطزررجوعمقطعمستقل |
| FV20-START /28.4.1 | LOCAL/T-B: إنبقيwaiting معready التقطقراراختيارالمقطعوالطلبوالاستجابةوالdecode؛ لا تنسبمشاهدالمقاطعلفشلP2Pبلاtrace | تأكيدأولفريموتعافيشبكةموضعي؛ لا fetchALL/انتظاراكتمالالتسجيل؛ فرضيةغيرمتكررةتوثقدونpatchاحتياطي |
| FV20-END /28.5 | LOCAL/T-B: مسارend الفعلي، persisted status/ended_at، أحداثالقناة، handlerوالاستعادة؛ الزروالصلاحياتقائمان ولاقرارإنهاءجديد | نهايةرسميةواحدةتصلA/B/C، تحريرالأجهزةوالـtimers، إغلاقالتقييموحفظcutoff/النتيجة، GETresyncعندحدثمفقود، عدمإعادةprepعلىcompleted؛ لااستدعاءendثانٍمطلوبمنالخصم |
| FV20-FINAL /28.5 | LOCAL/T-B: نهايةالمنافسة منفصلةعنdrain/receipts/finalmarker/finalized، آخِرمقاطع/lease؛ 404إنظهر: URL/وقت/حالةبلاسر، لاdiagnosisمنملاحظةغيرمحفوظة | drainمحدودةوذيلرفعالمخولمحفوظ؛ marker/فهرسنهائيصادق، idempotency/retry وفقالعقود، تشغيلVODللطرفينوللمشاهد؛ لاendيتعطلبالرفع، لاPHP/DBبعيددونتفويض، لاطلبfinalizeمخترع |
| FV20-LEAVE /28.5 | LOCAL/T-B: enumerateleaveBtn/dialog والتنقل وإلغاءpreview؛ قرارالمالكيرفضميزةمغادرةاختياريةثمعودة | إزالةميزةleave-and-return الخاصةأثناءlive، معزرendالقائموتأكيده، تحذيرتنقلبقدرةالمتصفح، تنظيفآمن؛ الانقطاع/إغلاقالتبويبليسendتلقائيًا، استعادةالاتصالومعاينةقبلالنشرمحفوظتان |
| FV20-SMALL /35 | LOCAL/T-B: NaN%واستجابةcompatibility_score؛ reminderحسب§12.7؛ nullإذاعادفقط | قيمةصادقةأوحالةغيرمتاحةدونNaNأونسبةمختلقة؛ التذكيربعقده؛ بقيةO19/UXمحفوظة، لاchildتنفيذآنية |

### 13.3 عقود الحل وحدود التكلفة

- علاجSIG لايعني حذفغيرالإشارات أوتغييرgetAfterعالميًا لكلالمستهلكين بلااختبارات؛ عقدcursor واضح ومتوافق، تقدم علىالمدىالمقروء حتىبعدالتصفية، معتحققالمستلم/الترتيبوالـauth. لاتجاوزبقراءةكلالتاريخفيكلpoll أوزيادةالتردد/الحجمبلاحد. اختباراتموضعيةتثبتحدوداستعلاماتD1 وعددصفوفالدفعات ومؤشرquery/index المناسب؛ لاauditDBعام ولاهجرةاستضافة.
- علاجREPLAY يميزinitial subscription وreconnect؛ لاتجعلمنعالتوستالقديميمحوunread/history أويسقطأحداثًاحدثتخلالالتعافي. نظمالمؤشراتالمختلفةلايخلطصلاحياتالقنوات.
- عقدTIME يربط index timeline بزمنالمشغّلالفعلي بمصدرواحد؛ لايفرضأنcurrentTimeمحليأومطلقفيكلMSE/blob. يسمحبتطبيعآمنعندالتشغيلإنثبتكفايته، وأيضرورةتغييرمنبعالتسجيلتثبتقبلpatch معحفظالوسائطالقائمةوالـready/durationsوالتنزيل30. لاتغييرcodec/containerشامل ولاserverFFmpeg أوإعادةكتابةملفاتقديمـةلمجردالملاحظة.
- الإنهاءمعتمدسابقًا في28.5؛ لايعادسؤالصلاحياته. رفضleave-and-return لايفوضحبسالمستخدم أوendمنbeforeunload. reconnectللإنقطاعلايُلغى.
- التشخيصوالإصلاحمتصلان فيUNITنفسها؛ لاPRتشخيصشكلي، ولااختبارإنتاجثالثقبلالمعالجةالمثبتة. ملكيةتنفيذواحدةثممراجعخارجيواحدكأصل؛ الحاجةلخبيرآخرتحددموضعًالسببمثبت لااستهلاكواسع.

### 13.4 الخروج والقبول المتبقي

بعدكلتعديل LOCAL/T-B موضعية → REMOTEمستقلعلىHEADنفسه → بروتوكول10 → حالةالكودوالنشر في14. الاختباراتالإلزاميةالحاكمةلاتُعطل؛ لاfull suiteإضافيةمتكررةبلاسبب.
بعدحزمالإصلاح، جلسةSواحدةللرحلةالمتأثرة تجمعمصدرينمميزينومشاهدًا، نشرصريح/تبادلوصوتوتسجيل، زمنوقفزوحافة، endواحدةوتحريرأجهزةوتسجيللجميعالأدوار. لاPASSللوسائطمنmock، ولاحاجةلأجهزةقياسصوتخاصةلإثباتوجودصوتالطرفين؛ قياسsyncدقيقيطلبفقطلعيبمحدد.
قائدالتنفيذيحفظPASSالقديمةغيرالمتأثرة، ويربطكلFV20وO19بالتقرير/الاختباروالحالة: CONFIRMED/FIXED/VERIFIED/NOT REPRODUCED/BLOCKED وحدودها. NOT REPRODUCEDلاتمحوإفادةقديمة، وفرضيةمفندةلاتصبححاجبًا.
القبولالمحددلبقية28 قبل30حسب14؛ اختبارالمالكالشاملبعد30يبقىموعدًاواحدًالرحلةالتنزيلوالنسخة. 41يقبلالمتبقيولاتكرارلشاهدصحيححديث.

## 14. اعتماد21أكتوبر — متابعة قبول الوحدة28 / المنافسة2242

**OWNER APPROVED — 2026-10-21.** المصدر تقرير `FV-UNIT28-ACCEPTANCE-REPORT(1).md` ومناقشته مع المالك واعتماده. يكمل هذا القسم §§11–13؛ لا يعيدها ولا يلغي أي DoD. الحالة والترتيب حصريًا في14-UNIFIED-EXECUTION-PATH. هذه **حزمة متابعة واحدة تحت UNIT28 القائمة**، لا UNIT جديدة أو مسار قبول موازٍ. معرفات A28 أدناه معرفات عيوب/أدلة وليست صفوف تنفيذ جديدة.

### 14.1 الواقع المثبت وحدود القبول

- CODE MAIN `d0768783ede68c11aab9cc442c148d99349fead3`؛ PR122 (متابعة28.3.1) MERGED إلى`54a3380a3c2c06319d48b2be2f953134bba2302d`، PR123 (متابعة28.4.1) إلى`a422f776381a91349e8e2b111dbe92734ed3e89a`، PR124 (28.5) إلىMAIN أعلاه. Quality39551641343 وDeploy39551641346 SUCCESS علىنفسMAIN؛ الكود والنشر مثبتان، **UNIT28 NOT ACCEPTED**.
- بحسب تجربة2242: نشر صريح ومعاينة خاصة، P2P بالاتجاهين، مصدران مميزان أحمر/أزرق داخل تسجيلMP4، شعار عربي، LIVE وVOD للمشاهد، تعافي الاتصال، حدث النهاية وتحرير أجهزة في الحالة المجربة، وإشعارات بلاreplay قديم نجحت. تحفظ كأدلة قبول محدودة؛ لا إعادةTURN/Finance/Ads أوcompositor أوكل الرحلة.
- البيئة Chromium/headless مع كاميرا/صوت من ملفات اصطناعية؛ تثبت المسار والمصادر المميزة، لا أجهزة المالك البشرية. وجود النغمتين مصدريًا لا يغني عن دليل صوت الخرج إن احتاج بند قبول الصوت إغلاقًا.
- العيوب الثلاثة: توقف التسجيل نهائيًا بعد فشلheartbeat عابر، عدم انتقال المنافسين إلىVOD في المكان، وقراءة VOD الجارية تتجاوز الإجمالي. نجاحgetStats/اتصالreconnect لا يثبت استئناف التسجيل. بقاء الملف الأول والتسلسل لا يثبت حفظ ذيل ما بعد الانقطاع.
- سبب تعليق انتقالVOD المقترح (استثناءteardown بعد تعيينcompleted) **فرضية تحتاج trace قبلpatch**؛ قد يرتبط بفشل التسجيل أو يكون مستقلًا. تمييز فشلheartbeat عناستحواذ حقيقي يحتاج اختبار المسارات الفعلية، لا قبول وصف التقرير كتشخيص كامل لكل كود.
- في نهاية2242 لم يكنB ينشر بعدreload؛ توقف إرسال خصم نشط عندإنهاء الآخر **حالة لم تختبر**، ولا تغلق منPASS devices فقط. O19-10 بذلكPARTIAL/NOT TESTED لهذه الحالة، لاNOT REPRODUCED بمعنى سلامتها.
- مشاركة الشاشةBLOCKED في بيئة الجلسة؛ ليستعيبًا ولاPASS. التنزيل30 **OUT OF SCOPE / NOT TESTED** وليسNOT REPRODUCED أومرحلة مغلقة. تأخرpreview أكثرمن40s ملاحظة تتبع، ليست عيبًا رابعًا مؤكد السبب.
- WORKLOG/PLAN-STATUS تحملان تقاريرLOCAL قبلالدمج؛ تاريخ محفوظ لا يعلو على أحداثGitHub. يضيف القائد الحالة الفعلية ولا يمحو التاريخ أويسمي الوحدةACCEPTED.

### 14.2 الملكية والتسلسل الداخلي

LOCAL واحد يملك الحزمة، ثم REMOTE مستقل واحد كأصل. **الترتيب الداخلي: A28-LEASE → A28-SURFACE → A28-TIME**؛ تحضير القراءة مستقل، لكن لا وكلاء متداخلون علىالملفات نفسها. الحزمة تغطي المتبقي فقط من عقود28/28.3.1/28.4.1/28.5، دون إعادةالوحدات المدمجة أوفرض PR لكلعيب. PR واحدة متماسكة مع تشخيص/اختبارات كل جزء؛ لوظهر فصل هندسي لازم يعرض السبب للقائد/التخطيط، لا ينشأ مسار إضافي تلقائيًا.
قبل التكليف يقرأ القائدMAIN وPR/WIP النشطة؛ absence of PR لا تثبتغياب عمل محلي. يرفق مقتطف التقرير/الأدلة للمنفذ والمراجع؛ المسارات `/home/z/my-project/...` فيتقريرالمختبر محليةله وليست ملفات مشتركة مفترضة.

### 14.3 مصفوفة التحقق قبل الإصلاح وبعده

| ID / أصل النطاق | LOCAL قبلpatch داخل المهمة نفسها | التنفيذ المقيد وREMOTE بعده |
|---|---|---|
| **A28-LEASE** /28 وعقدresume في15§2 وFV20-FINAL | نفّذ مسارheartbeat الفعلي وأظهر نتيجةnetwork/timeout/5xx مقابلرفضصلاحية/expiry/takeover. تتبعbeatLease/onLeaseLost/abort/طابورالرفع وreacquireLease ومستدعيه؛ عدموجودمستدعٍ وحده لايعني وجوباستدعائه بلاعقد. أثبت سببوقفregister/upload بعدعودةالشبكة | حالاتصريحة: HELD / UNKNOWN-TRANSIENT / EXPIRED / LOST-TAKEN-OVER وفقالعقد. لاادعاءاستحواذ منnetwork error. عندتعذرإثباتالصلاحية لا نشرغيرمخول؛ حفظالمعلق ضمنحدودالتخزينوالزمن القائمة، backoff/retry محدودان، وإعادةتحققخادميةقبلالاستئناف. عودةappend بتسلسلوجيلمخولين، لاoverwrite/حذف. REMOTE يختبرفشلهبضةواحدة، قطع15s، expiry، استحواذحقيقي، ردودقديمة وطلباتقيدالطيران؛ stale-generation يظل مرفوضًا. لا تمديدleaseمنالعميل أوتجاهل403/409/فقدصلاحيةلتمريرالاختبار |
| **A28-SURFACE** /28.5 وFV20-END | trace لتنفيذapplyCompetitionState→terminal teardown→render، والوعود/الاستثناءات والحالةالسابقـة بعدالتعيين. أعدالعطل معمسجل سليم ومعمسجلأُحبط أوفشلdrain؛ لاpatchلموضعمفترض منالوصففقط | قرارcompleted يصللسطحVOD/processing/unavailableالصادق لكلالأدوار دونRefresh، ولا تمنعخطوةتنظيففاشلة أوteardownمكرر اكتمالانتقالالواجهة. تنظيفمصادر/PC/timers آمنidempotent، معحفظذيلالرفعالمخول وعدمخلطUI deadline بإلغاءdrain. REMOTE يختبرالمُنهي والمتلقي، endمكرر وحدثمكرر/مفقود+GETresync، ثمS فيالجزءالمعدل |
| **A28-TIME** /28.4.1 وFV20-TIME | تتبعالمشغل الفعلي الذي تستعملهصفحةالمنافسة وقراءةtimeDisplay بعدseek، سواءSmartVodPlayer أوMSE/blob؛ عينةحقيقيةبطوابعغيرصفرية ومقارنةcurrentTime/getGlobalTime/index. لايكفي نجاحمعادلةأومشغلغيرمستخدم | مصدرواحدلتحويلmedia time إلىtimeline، لاoffsetمرتين، ولاclampلإخفاءالحسابالخاطئ. REMOTE يثبتالوقتقربالمحتوىالمقصود قبل/بعدseekوعندالحدود، totalصحيح، وعدمإفسادseek/rapid/window/double-bufferوالصوت؛ zero-origin/nonzero-origin ومسارMSEالفعلي إنمستخدم. لاإعادةتصميمcodec/container أوكتابةوسائطقديمة |
| **A28-PREVIEW-OBS** /28.3.1 | تتبعإعادةacquire بعدreload إذاعاد تأخر>40s: permissions/device/تهيئة/lease/signaling/network؛ افصلوسائطالاختبارعنحالةمنتج | لايصبحعيبًارابعًا تلقائيًا؛ إنثبتسببضمنالحزمةوبسيطوثقهواعرضحده، وأيscopeجديديرفعللتخطيط. NOT REPRODUCED يوثقمعالحدود، لاpatchاحتياطي ولا إسقاط للملاحظة |

**حدود الاستئناف:** لاوعد بحفظ كلوسائط انقطاعغيرمحدود أوذاكرةغيرمحدودة. يسجلالمنفذ بدقة ماذا جرىللمقاطعالمعلقة/الفاشلة/الفجوات وعندحدودالتخزينالقائمة. هذا لايفوضإسقاططابورعندفشلنبضةعابرة، أوإخفاءالفجوات، أوتغييرقرارresume append. رسالةالمستخدم تعكسالسببالحقيقي ولا تدعيجلسةأخرى دونإثبات.
لاserverFFmpeg، لاحذفقطع، لاoverwrite، لاهجرةD1/PHP/استضافة أوعقددفع/تقييمجديد. أيحاجةتغييرخارجي تثبتوتتبع10 وتفويضه؛ اعتمادالخطة وحده ليستفويضكتابةإنتاج.

### 14.4 أقل تحقق إضافي بعد التنفيذ والنشر

1. LOCAL يقدم before/after واختبارات سلوكية علىالمستهلك الفعلي، ثم REMOTE مستقل علىHEAD النهائي. الاختبارات الحاكمة القائمة تجرى وفقالمشروع؛ لا تكرارfull suite يدوي إضافي حيثCIيؤديها.
2. انتهاءالمراجعة والبوابات ودمجexpected HEAD ثمQuality/Deploy علىactual main وفق10؛ لاCODE DONE منوجودPR، ولاACCEPTED منبواباتخضراء.
3. **جلسةمتصفح/وسائط واحدة محددة بعدالإصلاح** تستخدممصدرينمميزينومشاهدًا للوصول للحالات التالية؛ لا تعاد قائمةمحطاتPASS كاملةً كاختبارات منفصلة:
   - بثوتسجيل → انقطاعمضيفمؤقت → عودة: P2P ليسالدليل الوحيد؛ طلباتregister/upload تستأنف وتظهرمقاطعجديدةready بمصدرين، والملفاتالسابقةلاتتغير، وآخرالذيلالمخول محفوظ.
   - إنهاءبينماالطرفانينشرانفعليًا: endواحدة، تحريرالطرفين وانتقالسطحيهما وواجهةالمشاهد إلىVOD/processingالصادق دونRefresh. فشلتنظيف/مسجلمحبط يختبرT/B ولا يلزمإفسادجلسةS يدويًا لإعادته.
   - زمنVOD صحيح بداية/بعدseekوعندالحدود، لايتجاوزالإجماليبسببdouble-offset؛ صوت/انتقالسليمبقدرالتعديل.
4. **استحواذleaseحقيقي:** تحققT/B تكاملي صالحللخادم/العميل وgeneration fencing، ورفضالكاتب القديم حتىمعطلبقديمقيدالطيران؛ لايحتاجS أوإطلاقجلسةبشريةإضافيةإنأثبتهالتكامل. لااختبارtakeoverإنتاجيعبثي.
5. **مشاركةالشاشة:** يسجلالقائد دليلنجاحسابق علىالمسار نفسه ويفحصهلتمسهالتغييرات. إنكانكافيًامحفوظًا فلايعاد؛ وإنلميوجدأوتأثراختبرهذهالنقطةفقطبمتصفحيدعمcapture وبإجراءمستخدم. لاPASSمنBLOCKEDأوheadless ولاادعاءأنخادمًا معطوبلغيابpicker.
6. كلA28تأخذ VERIFIED / OPEN / BLOCKED ودليلًا واضحًا؛ SOURCE syntheticيذكرصراحةً. لاجهازقياسخاصمطلوبلإثباتوجودالصوت، لكنلاPASSلصوتالخرجمنوجودaudio trackفقط.
7. تحفظنتائجFV20-SIG/TOAST/OFFER/REPLAY/PAIR والأدواتوالشعاروالنافذةغيرالمتأثرة؛ لاتعنيكلفروعالتعافيأوكلdevices. NaN% في35، 30للتنزيل، 32.1للقوائم، H7والمالوالمراحل التاريخيةلاتعاد.
8. إغلاققبول28 بعدالمتبقيالمحدد وحفظدليلscreenالمناسب فقط، ثم30 وفق14. اختبارالمالكالشامل بعد30 محفوظ؛41 يقبلالمتبقي ولايعيدالدليل الحديث السليم.

## 15. اعتماد23أكتوبر — UNIT30.4 / R4-COMP-CONTROLS-EARLY-END-1

**OWNER APPROVED — 2026-10-23.** المالك اعتمد مقترح توحيد أدوات المنافسة وملء الشاشة والألوان وقاعدة الإنهاء قبل خمس دقائق، بما فيه دخول الرصيد النظامي في تقييم الخصم وخفض ظهور التسجيلات القصيرة. موضع الوحدة30.4 قبل بوابة قبول واحدة للوحدات30–30.4، ثم31 وبقية14. هذه مواصفة وليست مصدرNEXT ثانٍ.

### 15.1 الحالة والنطاق

- UNIT28 ACCEPTED/CLOSED بقرار22أكتوبر؛ تحافظ هذه الإضافة على قبولها، وتعالج ملاحظات جديدة ومتطلبات منتج محددة، دون إعادةالاختبارات التاريخية.
- PR129/30 MERGED إلى`886026f9291fecf9c5640e2aadb942e16a24b380`؛ PR130/30.1 إلى`d12b7065de57aef02b3829ef60a10d7bc7d05151`؛ PR131/30.2 إلى`312af270c32fb9a44b471da0593565093ee2e521`؛ PR132/30.3 إلى`85eec139893f3b8f783befb8b119f709f8e40b33`. Quality39995222613 وDeploy39995222476 SUCCESS علىMAIN الأخير. الوحدات30–30.3 CODE MERGED/DEPLOYED؛ **PRODUCTION ACCEPTANCE PENDING**.
- نطاق30.4: أدوات صفحةالمنافسة ومشغلها للأدوار الثلاثة، زرالتنزيل وإرسالالتعليق وإرسالالرسالة فقط، وإنهاءمبكر/رصيدنظامي/جودةالمنافسةالقصيرة وترتيبظهورها. LOCAL واحد ثمREMOTE مستقل كأصل؛ لا تفويض لبناءالرسائل31 أوإعادةتصميمUX35.
- PR110 تظلOPEN/HOLD ولايدمجكودها؛ PR129 بديلها. حصرsuperseded/reused/missing وتوثيقالبديلقبلإغلاقها وفققرارB باقٍ؛ هذهالخطةلاتغلقPRكودأوتحذففرعها تلقائيًا.

### 15.2 أدوات البدء والنشر والتكبير

- الكودالمرجعي `85eec139`: `startBtn/fa-play` يستدعيstartCompetition وينقلaccepted→live؛ `publishBtn/fa-broadcast-tower` يستدعيpublishMedia وينشرمصدرالمستخدم. **وظيفتانمختلفتان** رغمطلبإزالةالسهم؛ يوحدالتفاعل المرئي فيزرالبرج، وينفذالإجراءالمناسب للحالةوالدور بمايحفظبدءالمنافسةالمخولوموافقةنشرالمستخدم نفسه. لا حذفstartAPIأوصلاحياته، ولااستبدالالموافقةبإذنالجهازأوحالةlive.
- للمضيفعندaccepted يجبأنتظلرحلةبدءالمنافسةونشرمصدره قابلةللوصول منزرالبرج بهيئةوعنوانواضحين؛ الخصمينشرمصدره بصلاحياته دونمنحهسلطةstartجديدة. عالجفشلجزءمنالعمليةوالنقرالمتكرروتحديثالحالة بصدق؛ لاقرارمنشوركاذبأوإرسالقبلالموافقة. لا تغييرزرplay/pauseلمشاهدةVOD؛ طلبالحذف يخصسهمبدءالمنافسةفقط.
- للمتنافس `expandBtn/toggleExpandStage` توسعةداخلصفحة، و`fullscreenBtn/toggleFullscreen` ملءشاشةمتصفح؛ يبقيانلأنهماوظيفتانمختلفتان، بأيقوناتtitle/ariaتوضحالفرق والحالةوتتبعمرجعألوانأدواتالاختبارالمعتمد. كلنقطةزائدةلنفسوظيفةfullscreenداخلنفسالسطحتوحد بعدجردالربط.
- مشغلالمشاهدفيMAIN يحويزرينمرتبطينبـembeddedToggleFullscreen؛ يوحدالزرالمتاححسبLIVE/VOD دونتركنسخةمعطلةأوفقدالوصول.
- طلبfullscreen يكونلحاويةتضم الفيديووالأدواتالمناسبة وزرخروجظاهر، لا الفيديووحدهوالأدواتخارجه. ظهور/إخفاءشريطالأدواتإنوجد لايحرممستخدماللمسمنإعادته. زرالخروج accessible، والنقرة/Escape/خروجنظامالمتصفح تحدثالأيقونةوالحالةعبرfullscreenchange؛ عالجنفيالوعدورفضالطلبوبديلwebkit دوناستدعاءاتمتنافسة.
- يغطيذلكالمضيفوالخصموالمشاهدأثناءLIVE وVOD وعندانتقالالحالة. لايتسببالfullscreenأوswapأوexpandفيتغييرمصادرالتسجيلأوالمرسلاتأوالموافقة أوإعادةإنشاءPC/recorder.

### 15.3 الهاتف وألوان الأزرار

- للمشاهد: fullscreen أفقي عنددعمscreenorientation وقبولالمتصفح، بإجراءالمستخدم؛ يستخدمالمساحةالمتاحةويحفظنسبةالفيديو والأدوات/safeareas. عندرفضالorientation أوعدموجودfullscreenAPI يقدمأفضلعرضمتاحداخلصفحة دونادعاءقفلناجح أوخطأيكسرالمشغل. يعيدorientationعندالخروجإندعمالمتصفح.
- للمتنافس: يلائمالعرضاتجاهمصدره/طريقةبثه، بلافرضlandscapeعلىمصدرعمودي أوتمديد/قصغيرمقصود؛ PiPوالتحكميظلانمناسبينللمقاسواللمس. تكبيرالصفحة/الهاتفوالدورانلايخفيانالخروجووظائفالتحكم، ولايغيّرانهويةمصادرالفيديو.
- زرdownload/sendcomment/sendmessage تستخدم **نفس صنف/تدرج الأزرار الأساسية الحالي من البنفسجي إلىالأزرق** مثلsearch/login؛ يستخرجالمنفذالتصميمالمشتركالقائم ولايخترعتدرجًاآخر. حافظعلىhover/focus/disabled/loading/contrast وicon/title/ariaوالنقرمرةواحدة. بقيةأدواتالبثتبقىبألوانمرجعالاختبارالمعتمدة؛ لا طلاءكلالأزرارباللوننفسه.
- إصلاحلونإرسالالرسالةلايفوضcompose/history/auth/M-01..05؛ وظائف31باقية. يسجلمن31/35ماأنجزموضعيًا لتجنبالتكرار؛ بقيةDoDلايسقط.

### 15.4 قاعدة300ثانية والرصيد النظامي للإنهاء المبكر

**قرارمنتججديدمحدد يتقدم علىالقواعدالعامةالمتعارضة فيهذاالنطاق فقط.** أهليةتصويتالمشاهدبعد300ثانيةوقيمته1–5 وتعديلاتهحتىالنهايةوالتعليقاتوH7الرقميةباقية.

1. يقاسالزمنخادميًا من `started_at` الرسميةإلىوقتقبولانتقالالنهايةالذري. **أقلمن300ثانية** إنهاءمبكر؛ عند300أوأكثرالقواعدالعادية. الوقتالمعروضأوساعةالعميللايقررانالعقوبة، والانقطاعلايصفّرالزمنأويوقفهباختراعقاعدةجديدة. لا عقوبةعلىaccepted/pendingغيرالمبدوءة.
2. عندطلبمتنافسلـendمبكر يعرضتحذيرAR/ENصريح: سيخسر، وخصمهسيحصلعلىرصيدنظامييعادلتقييمينبخمسنجوم(10نجوم)، وهوصفر، والمنافسةالقصيرةجودتهاصفر. إنألغىلايرسلend؛ إذاوافقينفذالخادمالقراربالزمنالفعلي. تأخرالنقربعدالحديخضعلمدةالخادم، لا عقوبةعلىطلبوصلبعد300. يجبأنلايستطيعالعميلتجاوزالعقوبةبحذفwarningأوتعديلpayload.
3. النتيجةللخصمفائزبانسحاب/إنهاءمبكر؛ **الرصيد10للخصمو0للمنهي** يدخلانفيالتقييمالعاموفقالمعادلةالمعتمدة(إجماليالنجوم/عددالمنافساتالتيخاضها). الصفرنتيجةنظامية، ليسصوت1–5 لمشاهد. المصدرSYSTEM_EARLY_ENDموثقأوبديلهالتصميميالقائم؛ لاتنشئحسابين/مشاهدتين/صوتينبشريينمزيفين، ولاتزودعدادuniqueviewersأوالمقيمينالحقيقيينباثنين.
4. تحفظهويةالفاعل/السبب/الوقتوالإصداراللازملمنعالتكراروتفسيرالنتيجة. لايجوزتراكم10عندretry/reload أوطلبendمكرر. endمتزامنمنالطرفينيفصلبأولانتقالذريمعتمدواحد؛ الطلبالخاسرلايضيفنجومًاويقرأالنتيجةالقائمة. لايثقwinner/bonusبالعميل.
5. الانقطاعأوالتبويبأوreconnectليسطلبانسحاب. النهايةالتلقائية/الإداريةدونفاعلإنهاءمتنافسمؤكدلاتنسبالعقوبةلطرفافتراضًا. توثقلنتيجةالمباراةالمنتهيةفعليًاقلمن300قاعدةالجودةأدناه ولوكانتأسبابالنهايةمختلفة. لاختراعفائزإنلامنهيبشريواضح.
6. تعرضالنتيجةبسببها، لا«اختارهالجمهور»أواختلاقتقييمينمنالمتنافسينلأنفسهم. نجومالنظامتفصلعنأصواتالجمهورفيالعدوالتاريخ؛ مايعرضفيالبروفايلوالبحثواقتراحالمنافسينيستعملالتقييمالعامالمحدثبمصدره دونتغييرصلتهبالموضوع/اللغة/البلد.
7. لا سياسةماليةأوغرامةجديدة؛ يحافظمسارend/cutoffوالتسويةالقائمةعلىidempotency. حددقبلpatchكلالمستهلكينللـwinner/ratingوأثبتتكاملنتيجةالإنهاءالمبكرمعالعقودالموجودة، دونإعادةبواباتFinance/Ads. أي تعارضمنتجلمتحسمههذهالقواعديرفعمحددًاللمالك/التخطيط.

### 15.5 المنافسات القصيرة في الاكتشاف والبحث

- لكلتسجيلمنافسةمدتهالرسميةالموثوقةأقلمن300ثانية، **مساهمةجودةالمنافسةفيالترتيبصفر**، بمافيهاالنجومالنظامية. لاتُصفّرviews/likes/commentsالحقيقيةأونجومملفاتالمتنافسينأوتحذفالبيانات؛ الصفرعقدqualityللمنافسة.
- الصفرلايكفيلندرةالظهورمعإشاراتالصلةوالحداثة؛ لذلكتكونالمنافساتالقصيرةفي**طبقةأولويةبعدالبدائلالمؤهلةالأطول** فيالتوصياتوالتصفحوالبحثالاكتشافيضمننفسfilter/surface، معترتيبH7المعتمدداعلياكلطبقة. تظهرعندنُفادالبدائلمنالطبقةالأولى، لامنعنهائيولاخلطcategoriesلملءصف.
- تبقىبالرابطوبالبحثالمباشرعنها. يحددالمنفذبوضوحمنعإخفاءالنتيجةالمقصودةبالـid/الرابط/عنوانمطابقللعقدالقائم؛ لا يضعمنافسةغيرمطابقةبدلها. LIVE/Upcomingلمتكتملمدتهالاتعاملتلقائيًاقصيرةلمجردأنعمرهاأقلمن300.
- snapshot/cursor/hasMore/exhaustionيبقىصحيحًا؛ لاRANDOM+OFFSETأوهاردكابأوقطعcontinuationعندبدءالطبقةالثانية، ولاافتراضثباتجلسةقديمبعدتغييرسياسةالترتيبدونعقدتوافق/نسخةواضحة. H7weightsالرقميةلاتعاد؛ هذهطبقةأولويةمعتمدةجديدة.
- المدةغيرالمعروفةأوالبياناتالمتناقضةلايخمنلهاصفرأوعقوبة؛ سجلحالتهاوبديلهاالمتوافق. تطبيققاعدةالعرضمنمدةموثوقةلايتطلبإعادةكتابةدفاترأرصدةتاريخية. لاbulkتغييرنجومأوفائزينقدامىأوحذفseed/منافساتمنهذهالوحدة.
- الأداء: يراجعLOCALمسارالاستعلاموModelوالفهرسقبلالإضافة، وREMOTEيثبتpaginationوالحدودوالتكلفةالموضعية؛ لاجلبكلالمنافساتللعميللفرزها، ولاDBmigrationبعيدةدون10والتفويض.

### 15.6 تحقق قبل التنفيذ وبعده والقبول المجمع

**قبلpatch — LOCAL ضمنالمهمة:** جردstart/publish/expand/fullscreen ومساراتالأدواروأسماءالحاويات؛ إثباتاختفاءالأدواتبالـDOM/متصفح، ومصدرالgradientالقائم. تتبعendالتزامني/مدةالخادم/حسابالنجوموالفائزومستهلكيهاوحراسالأهلية، وجودةالمنافسةوترتيبH7/الطبقات/الجلسات. السببالمفترضيثبتولايمسالمنفذمسارًاسليمًابافتراضالتكرار. لا تحقيقإنتاجيشاملقبلالعمل.

**بعدالتنفيذ — REMOTEمستقل علىexactHEAD:**
- اختباراتسلوكيةلزرالبرجفيaccepted/liveوالأدواروفشلstart/publishوالنقرالمزدوج؛ لاإرسالقبلالموافقةولااختفاءوظيفةstartالمخولة. أدواتتوسعة/ملءشاشةمتميزةومداخلfullscreenبلاازدواجداخلنفسالسطح.
- اختباراتحدود299.999/300/300.001s بحسبدقةالتخزين، ساعةعميلكاذبة، cancel، retry، endمتزامن، فاعلغيرمخول/انقطاع/autoend؛ رصيد10/0وفائزواحدوتجميعprofileمرةواحدة، لاfakeviews/voters، والتقييمالعاديبعدالحدمحفوظ.
- اختبارquality0للقصيرةودونتصفيرالبيانات، طبقتيالأولويةلكلالـsurfacesالمتأثرة، topic/status/languageisolation، بحثمباشر، cursor/exhaustionوالجلسة/refresh وعدمقفزالنتائجأوتكرارها؛ بقاءترتيبH7داخلطبقة.
- اختباراتالمستهلكالفعليونقاطالربط، لاregexيوهمأنالسلوكعمل. تحديثWORKLOG/PLAN-STATUSفيPRبحالةصادقةومتبقيS.

**بوابةقبولإنتاجواحدةبعد30.4:** تضم30/30.1/30.2/30.3/30.4؛ لابوابةخامسةمنفصلة. تشملDoDالتنزيل/الجلسة/HttpOnly/حراسالأمانوالعقودالمتأثرةفقط، والتحققالبصريfullscreen/exit/expand علىسطحوهاتفبالأدواروالـLIVE/VOD المناسبة، ألوانالأزرار، وتحذيرونتيجةإنهاءمبكرموجهةبالحساباتالتجريبية. ماتوفرقبولهسابقًاغيرمتأثرلايعاد؛28تبقىمغلقة، لاSشاملةTURN/مال.
FULLSCREEN/orientationعلىجهازلايدعمهايسجلحدودالدعموبديلًايعمل؛ mockorientationليسقبولهاتف. H7الرقميةلايعاداعتمادها. بعدالقبولالمجمع31→32→32.1→33–42؛ اختبارات31/35اللاحقةتستثنيالألوانالمقبولةفقط وتحفظبقيةنطاقها.
