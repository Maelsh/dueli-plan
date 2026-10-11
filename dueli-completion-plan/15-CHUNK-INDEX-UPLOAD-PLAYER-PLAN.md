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

NEXT يقرأمن14: INDEX ثمSAFE ثمPLAYER ثمDOWNLOAD ثمكلالباقي. OWNER APPROVED لخطة/كود/اختبار هذهالمعالجات؛ تطبيقremoteDB/PHP/إعداداستضافة يحتاجartifactراجع وتفويضالنطاق وفق10/02، لا تغير credentials أوتحذفقطعًا. لاإعادةطلبقراراتالبنية/H7. نسخةupload.php المعطاةكافيةلتحليلها؛ اطلبنسخ الملفاتالأخرىمنزوعةالأسرارعندلزومinventoryفقط.

مرجعFFmpeg الرسمي: https://ffmpegwasm.netlify.app/docs/getting-started/installation/ ؛ مرجعD1pricing: https://developers.cloudflare.com/d1/platform/pricing/ . يستوثقالمنفذمنversions الفعليةوعقدworkerقبلالتنفيذ.
