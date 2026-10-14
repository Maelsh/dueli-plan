# Dueli — فهرس المقاطع وأمان الرفع والمشغل والتنزيل

**OWNER APPROVED — 2026-10-11.** المالك وافق على التقسيم والترتيب والمعالجات وطلب تثبيتها ودمج الخطة، وسلم نص upload.php الحالي. ترتيب وحالة وNEXT حصريًا في[14](14-UNIFIED-EXECUTION-PATH.md). هذا ملف عقود وDoD، وليس مسارًا ثانيًا. 08 للقرارات و10 للإصدار؛ لا إعادة H7 أو مراحل مغلقة.

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
