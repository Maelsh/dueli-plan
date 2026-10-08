# Dueli — R4 Recovery / D1 Consumption / Leadership Handoff

**مراجعة 2026-10-08؛ مقترح تنفيذي للمراجعة قبل الدمج.** هذا الملف يضيف إصلاحات لعيوب استخدام وتشغيل جديدة محددة. لا يعيد فتح Backend/Core/Live/TURN/Finance/Ads/R1 أو الوحدات الصحيحة المغلقة. 08 مرجع قرار المالك، 11 مرجع H7 الثابتة، 04 الحالة، 10 بروتوكول الدمج والإصدار. لا تفويض فوترة أو نقل قاعدة أو كتابة إنتاجية من اعتماد هذا الملف.

## 1. الحالة ومصدر الدليل

- code main المثبت من GitHub: `2e3d3681093a591e917dd1c57dc9cc249c307458`، PR#102 merged. R2 ووحدات R3 مغلقة برمجيًا وفق سجل04؛ C3 وثيقة تصميم فقط ولا تفوض حذف synthetic.
- PR#103 OPEN وقت القراءة؛ HEAD `d020d8c4febdf778fabfe592dd11f40ed48add4a`، BASE هو main أعلاه؛ إصلاح title escaping موجود فلا يعاد تكليف تنفيذه. لا DEPLOYED قبل بروتوكول10.
- تقريران بصريان خارجيان، ملخصهما موجه القائد الذي نقله المالك في2026-10-08: NOT READY مع عيوب محددة. هذه المراجعة لم تدخل الإنتاج ولم تتصل بCloudflare. التقارير الأصلية غير متاحة في هذه المراجعة؛ لا نخترع تصنيف BOTH/ONE لكل بند. القائد يربط كل بند بالشاهد الأصلي المتاح دون إعادة الاختبار لمجرد تصنيفه.
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

## 3. الوحدات والنطاق ومعيار القبول

| الوحدة | الهدف وDoD | الوسيلة / الاعتماد |
|---|---|---|
|R4-DB-DIAG-1 — NEXT|ربط الاستعلامات الأعلى بالكود الكامل؛ قراءة مخطط الفهارس عند توفر تفويض القراءة؛ EXPLAIN محلي على مخطط مماثل؛ تحديد إعادة البناء/loadProfiles/context/polling ومسار attribution؛ تسليمbaseline وخطة تحسين صغيرة بلا كودإنتاجي|T+تحليل؛ Analytics منقولة تستخدم مع حدودها؛ لا Astra|
|R4-DB-OPT-1|فهرس/إعادةصياغة/تقليل التكرار وفق القياس؛ مقارنة before/after على أحجام محددة؛ invariants التقييم/المشاركة/H7/الحجب/snapshot/filters/exhaustion محفوظة؛ binds<=100 شامل scalars والقوائم المكررة؛ قياس rowsWritten أيضًا|بعدDIAG؛ T+B موضعيان؛ migration جديدة تحتاج مسارrelease وتفويضproduction منفصل|
|R4-EVENTS-NOTIFY-1|حفظ receiver في csp-delegate مع allowlist/CSP؛ نقر/keyboard؛ فتح الإشعار يحدثread والعداد بعقد ownership؛ join link يوصل إلى الطلب القابل للقرار؛ replay لا يكررtoast؛ تاريخ الحالة واضح|T+B؛ لا eval أو إعادةأذونات؛ سياسة unreadالمفتوحة أدناه تعرض عند الحاجة|
|R4-MESSAGES-1|إظهار حاوية mobile الأم/عودةالقائمة؛ بدءمحادثةمنmessages؛ profile deep-link يرجع الموجود/الاسم؛ إرسال/معاينات/عدادات بلاreload؛ الحجب والملكية محفوظان|T+B ar/en mobile/desktop؛ لا إعادةبناءرسائلالإدارة|
|R4-PROFILE-SAVE-1|PUTsettings200 بلاpersist فيdisplay_name/bio: تتبعpayload/controller/model/GET؛ حفظثمrefresh مثبت؛ validation/ownership|T+B محدد؛ لا إعادةAuth/settingsكاملة|
|R4-HOME-UX-1|رسمrails المستقلة عندجاهزيتها معloading/retryواضحين؛ المتأخرلا يحجبالسريع؛ تحميلعندالرؤية/تنسيقفتحالجلسات وفققياس؛ لا stalepaint/requeststorm|ينسق معDB-OPT علىHomePage؛ لا تكليفين متعارضين|
|R4-UX-STATE-1|قائمةالعيوبالمثبتة أدناه:ترجمة/NaN/mojibake/reminder422/help/adminvisibility/عدادات/popovers/تأخير؛ يجمعالمترابطويفصلPRعنداختلافالمسارات|T+B موضعيان؛ لااستكشافشامل|
|R4-MEDIA-ADMIN-ACCEPT-1|VODprocessingلعينةموجودة:تمييزdemoقديمعنعيب؛ رحلةردالإدارةبحسابصالحومصرح؛ PASS/FAIL/BLOCKEDبدليل|T/Bأولًا؛ S/Hفقطللوسائطالحقيقيةأوالوصول|
|R4-ACCEPT-REM-1|قبولالرحلاتالتيثبتفشلهاوالمواضعالمعدلةواستقرارDBضمنميزانية؛ تقريرجاهزيةلايمحوعوائقR0|بعدالخدمةوالإصلاحات؛ لا إعادةالبواباتالتاريخية|

هذه الوحدات ليست عددPRs مفروضًا. PR103مسارموجودمستقل؛ REMOTEرسمي ثمprotocol10، لا APPROVEشخصيبديل. DIAGيمكنبالتوازي معه؛ الواجهاتمحليًايمكنالتقدم فيها أثناءانتظارanalytics، لكن اختبارإنتاجيعلىDBمستنفدةلايفيد.

## 4. سجل العيوب الذي يغطيه الإصلاح

| ID | الأولوية | الشاهد/السبب المتاح | الوحدة |
|---|---|---|---|
|DB-01|BLOCKER|المالك نقلخطأdaily read quota؛ لا migration/bind-limit|DIAG/OPT|
|N-01|BLOCKER|dropdownنقرTypeError؛ resolveFnيرجعfunctionبلاreceiver وrunHandlerيناديهابلاreceiverمؤيدبالكود|EVENTS-NOTIFY|
|M-01|BLOCKER|mobileحاويةhidden md:flexلا تظهرعندفتحconversationوفقالتقرير|MESSAGES|
|P-01|HIGH|settings200والاسم/bioلايحفظانحسبالتقرير؛ السبب يحتاجتتبع|PROFILE-SAVE|
|N-02|HIGH|فتحViewبلاmarkread؛ اليدويوMarkAllيعملان|EVENTS-NOTIFY|
|N-03|HIGH|joinnotificationيذهبcompetitionبلاdecision بينماmy-requestsفيهالإجراء|EVENTS-NOTIFY|
|M-02|HIGH|profile→messagesاسم#id/محادثةموجودةلا تسترجع|MESSAGES|
|H-01|HIGH|Homeتأخر15–30ثانيةوفقالمتصفح؛ Promise.allمؤيدبالكود|HOME-UX/OPT|
|S-01|HIGH|titleغيرمهرب؛ PR103OPENيعالجالمسارالمركزي|PR103القائمة|
|N-04|MEDIUM|SSEtoastsقديمة/closedunread/قبولبعنوانطلبجديد/عربيعلىEN|EVENTS-NOTIFY/UX-STATE|
|I-01|MEDIUM|InvitePanelmojibake/NaN%، مفاتيحنصوصمفقودة|UX-STATE|
|U-01|MEDIUM|RemindMe422بلاموعدوبلاتفسير/تأخرقبول10–12ثانية/تعليقاتعدادبلاrefresh|UX-STATE|
|U-02|MEDIUM|AdminPanelلغيرadminثم403 وhelpرابطobjectObject|UX-STATE|
|U-03|MEDIUM|بطءinviteبحث/popoversمكررة/تأخرانتقالبعدcreate|UX-STATE|
|M-03|GAP|Composeغيرموجود/معايناترسائلوقراءةعدادمتأخرة|MESSAGES|
|VOD-01|NEEDS TARGETED VERIFICATION|processingلعينات؛ بياناتdemoقديمةأوعطللميحسم|MEDIA-ADMIN-ACCEPT|
|ADM-01|BLOCKED ACCESS|لاadminصالحللتجربة؛ لاPASSولاFAIL؛ admin/adminلايعمللايعنيإنشاءهإنتاجيًا|MEDIA-ADMIN-ACCEPT|
|VIS-01|TARGETED|responsive/a11y/darkmodeحسبالتقارير؛ يلزمشاهدوموضعلكلبند|الرحلةالمتأثرةثمACCEPT|

يضيفالقائدروابطالشواهدالأصليةويصنفCONFIRMED_BY_ONE/BOTH/TARGETEDعندتوفرها؛ لا يطلبإعادةالرؤيةلامجردعدالشهود. لا حذفdemoأوالتاريخلحلUX. حالاتقديمالنصيمكنfallbackدونخلطالعربيةبالترجمةالدلاليةالجديدة.

## 5. تحقيق وتحسين D1 دون تغيير المنتج

1. توقفالتشخيصالمحادثيالمتكررمعمساعدCloudflare؛ الجدولأولويةكافية. استرجعrawanalyticsفقطإنكانتمتاحةبسهولة، ولا توقفالفحصالمحليعلىتناقضexecutionالذيلايغيرترتيبالمستهلكين.
2. اقرأالفهارسالفعالةبإذنقراءةمحددإذاكانمتاحًا؛ حافظعلىمخططlocal/previewمطابق. EXPLAINQUERYPLANللنصالكاملبلاbenchmarkمستنفدعلىproduction. لا تفترضcreatedindexفيrepo=productionموجوددونreadinessدليل.
3. قارنindexمرشحcreator/opponentمرتبطactualparticipationوملخصحالةالبدءبالخطةوالحجم، ولا تضفثلاثفهارسعمياء. تحققبأنCOUNT/SUMتجمعالصفوفالصحيحة.
4. شاركسياقالمستخدموالإشاراتالخاملةضمنعمليةبناءمنسقةأوcacheمحكومإذاقياسالتكراربرره؛ لاKVإلزاميولاcacheشخصيمشتركيكشفبيانات. مفتاحيشملidentity/context/policyوالصلاحياتوexpiry؛ إعادةزيارةصريحةتظلجلسةجديدة.
5. قستكلفةإنشاءsnapshotكاملةواستمرارهاكلّعلىحدة؛ المؤهلونليسوا15فقط. لا سقف15/100 ولاRANDOM+OFFSETولاخلطcontextلحلاستهلاك.
6. aggregatesمسبقةحللاحقفقطإنأثبتالقياسحاجتها؛ تحتاجupdate/invalidationعندتعديلالتقييم/القطع/المشاركة، لا تغييرSUMstars÷participationsأوH7.
7. ميزانيةمتوقعة=استدعاءاتالواجهات×قراءاتالطلب+polling/background/QA. متوسطmsالمنخفضلايثبتأنقراءاتD1رخيصة. freequotaقراركفايةبعدالتحسينبهامشموثق؛ لا نعدبأنفهرسينسيجعلانالحصةكافية.
8. لا حملإنتاجيجديدمتكررلإثباتالاستقرار؛ تحققصغيربعداستعادةالخدمةضمنميزانيةمصرحهابينLOCAL/REMOTEوالقائد.

## 6. القرارات المفتوحة وحدود التفويض

- **DB-HOSTING OPEN:** إبقاءD1Free/WorkersPaid/نقلإلىاستضافةالمالكلميعتمد. توصيةالتخطيط: تحسينالاستعلاماتأولًا، ومعحاجةاستعادةالخدمةعرضPaidعلىالمالك؛ لا ترقيةأوفوترةأونقلأوSQLwriteهنا. MySQL/MariaDBعلىiFastNetقابلانللدراسةلاحقًا؛ يلزمباقة/TLS/موارد/backup/latencyواختبارترحيلمحدد. SQLiteAPIيعنيbackendإضافيلا نقلملفمباشرإلىWorker.
- **NOTIFICATION-CLOSED POLICY PROPOSED, NOT OWNER APPROVED:** حفظالتاريخ، وسمالحالةالمغلقةوإخفاءالإجراء؛ القراءةلا تعنيالإغلاقوالإغلاقلا يعنيالقراءة؛ unreadللقراءةوالطلباتالقابلةللإجراءمستقلة. رابطdeep-linkإلىواجهةالقراركافٍبدلإضافةأزرارداخلdropdown. القائديراجع08/العقدالحالي، ويعرضفقطالاختلافالذييحتاجقرارًا؛ لايفرضهذهالمقترحاتكقرارمثبت.
- **ADMIN ACCESS OPEN:** حسابصالحبتفويضمنالمالكخاصًا. لاadmin/adminإنتاجيمنهذهالخطة، ولا اختراعتفويضإنشائه.
- **PRODUCTION MIGRATION:** الإذنالسابقبقراءةالفهارسوEXPLAINلمساعدCloudflareلاينتقلإلىأيLOCALكوصولعام؛ القائديحددنطاقالأوامروالهويةإذااحتاجها. الكتابةعنطريقmigration/runbookقابلللمراجعةوتفويضصريح.
- قراراتH1–H9المثبتةوh7-v1لايعادطرحها؛ KEEP NOWلايتغير؛ grace-periodSECغيرالمانعةلاتتحولدَينًاجديدًا.

## 7. القبول والكلفة وتسليم القيادة

T: receiver/persistence/queryplan/numericinvariants/ownership. B: Playwrightأومتصفحمعتادmobile/desktopar/enRTL/LTRللنقر/الرسائل/الفلاتر/العدادات/التمرير. S/Astraأوالمالك: الصوتوالصورةوالجهازالحقيقيوالحكمالبصريالحصريعندتعذرT/B؛ لافرضAstraللرانكأوالفهارسأوالرسائل. H: حسابالإدارةوالبنكوالفوترةوالإطلاق.

إغلاقR4الويب:لاblocker/Highمعلومفيالرحلاتالأساسية؛ snapshot/H7/صيغالتقييممحفوظة؛ الخدمةضمنميزانيةمقاسةوالأخطاءواضحة؛ قبولالرحلاتالفاشلة؛ الوصولالإداريالمصرحومعلوماتالإطلاقغيرمؤقتة. R0حالةخارجيةصريحةلاPASSمصطنع؛ البنك/المزوّد/الوثائق/قرارالإطلاقبيدالمالك.

تقديرتخطيطيمن8أكتوبرمعإبقاءD1:متفائل3–5أيام،أرجح5–9،ومععطلmediaأوبناءsnapshotبنيوي10–14؛ ليسموعدإطلاقمضمونًاولايتضمنترحيلDBأوالخارجيات. يحدثبعدDIAGولا يستخدمعددPRsوحدهكقياسقبول.

نقل القيادة يمكن الآن دون انتظارإغلاقجميعالعيوب:يحفظالقائد04وحالةPR103وتكليفREMOTEالنشطوالأدلةوالتفويضات؛ يعطيCODE/PLANSHAالنهائيينومرجع12وNEXT. لا يبدأPRإصلاحمكررلـ103ولا يعيدH7/R2/R3. كلPRكودWORKLOG+PLANSTATUS→REMOTEexactHEAD→expected_head_sha→QualityactualmergeSHA→DeployنفسSHAوفق10.

## 8. بطاقة LOCAL للخطوة الأولى

```text
DUELI — LOCAL — R4-DB-DIAG-1 — READ ONLY / NO CODE CHANGES
CODE: https://github.com/Maelsh/dueli-opus
PLAN: https://github.com/Maelsh/dueli-plan/tree/main/dueli-completion-plan
PLAN COMMIT: <merged plan SHA>; BASE: <current code main confirmed by lead>
اقرأ12 §§1–5 و04 و08 و10 و11؛ القائد يرفقمقتطفالنطاقوالجدولعندتعذرالوصول.
استعلاماcreator/opponentcounts يمثلان48.5%منقراءاتالجدولالمنقول.
اربطالنصالكاملبـH7SignalsModel.loadProfilesوloadViewerContext
وبـUserSignalsModel؛ تحققمنindicesوالـEXPLAINعلىlocal/preview.
تتبععددsessionbuildsوتكرارprofile/contextبينHome rails؛
قستكلفةبناءالمؤهلينكاملةواستمرارالدفعاتكلّعلىحدة.
لا تعتبرالنصالمبتور50paramsعقدًاولاfullscanمثبتًا.
سلمBASE/مساراتSQL/الفهارس/الخطة/baselineواقتراحأصغرOPT
يحفظH7والتقييمactualparticipationوالحجبوالسياقوexhaustion.
لا كودأوPRشكليولاproductionload/remoteexport/write/index/migration
ولاbillingأوترحيلأوحذفsynthetic. غيابremoteaccessليسإذنطلبsecrets.
استخدمالأدلةالمنقولةوالمحلية؛ اذكرماينقصفقطلتحسينمحدد.
```
