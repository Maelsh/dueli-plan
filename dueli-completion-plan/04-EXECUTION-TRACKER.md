# Dueli — لوحة التنفيذ والقرارات

**مزامنة بعد PR #80 — code main: b23cfe2a9202136f47da08d55fecee74e259f979.** [08-OWNER-DECISIONS.md](08-OWNER-DECISIONS.md) مرجع القرارات، لا المقترحات القديمة. دمج الخطة لا يعني تنفيذ متطلباتها.

## الحالة المرجعية

| المجال | الحالة والدليل |
|---|---|
| خطة 16 والبنية/البث/المال/الإعلانات | CLOSED؛ لا إعادة تحقق |
| R1 كلها | DONE بتأكيد المالك |
| R3-B7 | DONE CODE — PR#75 مدموجة؛ HEAD c8f8e86f592ddf3a593b52fd5c88156c9ad3a6a7؛ merge d19204738407657c97f6ba6ede9c601a3cbdb644 |
| Guest «مقترح لك» | DONE — R3-GUEST-1 عبر PR#76؛ HEAD a39966a92a129591d672c690668d83067fb078da؛ merge 79edbf2ffd3ee0755a9b35c6fd20d5e62acd7ff5؛ تجربة المالك PASS |
| بريد استعادة/تغيير المرور | DONE CODE — R2-AUTH-1 عبر PR#77؛ HEAD 98e3ba012e61feede45e5c8005ac46ff8332a0f4؛ merge 1376c045adaf901ad9b266741789665f0137f3f8؛ وصول بريد إلى Spam مثبت بتقرير المالك؛ لا ضمان Inbox، تحقيق deliverability مؤجل |
| #78 هوية الدومين | DONE — merge f3942c3bbe450bf3c727a235fe37a46bdf9be9b1؛ لا تغيير transport/DNS |
| #79 استعادة النشر | DONE — merge af96b8f06fd6920e435384af444c857bf8492dc9؛ remediation محددة لاحقة في RELEASE، لا إلغاء الدمج |
| #80 UX البريد + rails forensic | DONE — merge b23cfe2a9202136f47da08d55fecee74e259f979؛ production deployed وفق القائد، UX لا deliverability fix |
| incident 0033 | REMEDIATED OPERATIONALLY حسب القائد: manual remote apply، الجدولان موجودان؛ منع التكرار PLANNED في RELEASE |
| Home rails | Guest continuation موجودة؛ logged Suggested/category/subcategory دفعة15 بلا continuation. Suggested Guest/User يتجاهلان status؛ recorded eligibility ناقصة. 05 §8 و09 |
| R0 قرارات المنتج | OWNER CONFIRMED في 08، عدا أرقام H7؛ الإجراءات الخارجية منفصلة ولم يثبت إنجازها |
| R2 وبقية R3/R4 | PLANNED؛ لا نعلن إكمالها من اعتماد السياسة |
| R5 | DEFERRED AFTER WEB LAUNCH |

#75–#80 merged مثبت من GitHub. إنتاج #80 وتطبيق migration0033 ونتيجة Spam/SPF/DKIM/DMARC مصدرها تقرير القائد/المالك؛ هذه المراجعة لم تتصل بقاعدة الإنتاج أو تفحص البريد الحي. لا إعادة تكليف Guest/Auth؛ لا ادعاء اكتمال بقية R2.

## الوحدات

| الوحدة | الحالة / الاعتماد |
|---|---|
| R3-GUEST-1 | DONE — PR#76 مدموج بعد APPROVE مستقل من وكيلين؛ تجربة المالك PASS |
| R2-AUTH-1 | DONE CODE — PR#77 مدموج بعد APPROVE مستقل من وكيلين وreal-D1 integration؛ وصول Spam رُصد وفق تقرير المالك؛ لا Inbox blocker؛ قرار تأجيل deliverability |
| R-RELEASE-1 | MERGED #81 / POST-MERGE BLOCKED — SEC-06 coverage، preview bindings، required schema gate، نفس SHA؛ T ومراجعة مستقلة |
| R3-RAILS-1A | MERGED #82 / POST-MERGE BLOCKED —؛ providers/context/filter على البنية القائمة؛ لا H7 coefficients |
| R3-RAILS-1B | MERGED #82 / POST-MERGE BLOCKED —؛ كل الصفوف حتى exhaustion؛ T+B؛ يجوز جمع A/B |
| R2-J | PLANNED — H3 محسومة، لا طلب موازٍ وقبول واحد يغلق المعلق الآخر |
| R2-L1 | PLANNED — H1=300 ثانية، H2 معتمدة؛ تعليقات وحضور وكاتب مشاهدة |
| R2-V | PLANNED — بعد L1؛ تعديل 1..5 لكل طرف، حصيلة live ظاهرة ثم حسم نهائي |
| R2-L2 | PLANNED — غرفة/وسائط/إعلان و Like/Dislike وتعليقات video-time |
| R2-A | PLANNED — admin المؤقت وإعداداته وصلاحياته ونظام وثائق/بيانات؛ الحساب لم ينشأ بهذا التحديث |
| R2-M | PLANNED — personal ثم admin مستقل وظيفياً وبياناتياً، هويةرسمية وتبويب وإشعار منفصلان |
| R2-P | PLANNED — طرق صرف محفوظة؛ البنك الحقيقي إجراء خارجي |
| R2-F | CONDITIONAL — وظائف أصلية ناقصة خارج R1، لا بوابة خدمات قديمة |
| R3-D0 | DESIGN OPEN / START WITH RELEASE — أوزان كل صف وقسم وفرع، عرض مبكر للمالك؛ النطاق معتمد والأرقام مفتوحة |
| R3-D1 | PLANNED — أوزان جميع Home rails والأقسام والفروع بعد D0 وجاهزية الإشارات؛ استمرار وحده لا يغلق Home |
| R3-D2 | PLANNED — Profile=SUM نجوم/عدد منافسات، ترتيب المستخدمين ومطابقة التخصص |
| R3-C1/C2 | PLANNED — مساعدة/إتاحة ووثائق من لوحة المدير؛ الحقيقيات بعدالإطلاق حسب H9 |
| R3-C3 | PLANNED DESIGN ONLY — KEEP NOW ثابتة |
| R4 | PLANNED — قبول الرحلات الجديدة، تسليم مسؤول ببيانات غيرمؤقتة، إجراءات فعلية وقرار إطلاق |

**NEXT الحالي: R-RELEASE-1-REM1 وفق10.** #81/#82 merged؛ توقف feature merges حتى حسم deploy/main Quality. ما يلي وصف ترتيب ما بعد#80 قبل هذه الواقعة: السبب: نقص تغطية SEC-06 مثبت وعزل preview/schema readiness غير مضمونين؛ تمنع تكرار حادث0033 قبل المزيد من الإصدارات. بعدها R3-RAILS-1A/1B → J → L1 → V → L2 → A → M → P → F → D1/D2 وبقية01. D0 يبدأ مع RELEASE ويعرض أوزان كل قسم وفرع مبكراً. continuation يمكن تجهيزه قبل الأرقام؛ إكمال Home يتطلب أوزان D1 المعتمدة.

## القرارات المثبتة

| القرار | الحالة |
|---|---|
| H1:5 دقائق=300 ثانية مشاهدة حية لنفس المنافسة | OWNER CONFIRMED |
| H2:مشاهدةواحدة/هوية/منافسة/يوم وحضورمستقل | OWNER CONFIRMED |
| H3:دعوةمعلقة تمنعطلباً موازياً وخصمواحد يغلقالبقية | CONFIRMED AS REPORTED BY LEAD/OWNER |
| H4:1..5 لكل طرف، قابلللتعديل حتىالنهاية بصوتفعالواحد | OWNER CONFIRMED |
| H5:نتيجةحيةمؤقتةظاهرة، ثم نهائيةعندالإغلاق | OWNER CONFIRMED |
| Profile=SUM النجومعبرالمنافسات÷عددالمنافسات، لاعددالمصوتين | OWNER CONFIRMED |
| Rank المنافسة=أثرجمعنجومطرفيها+المشاهدات+Like/Dislike، الوزنضمن H7 | OWNER CONFIRMED INPUTS؛ coefficients OPEN |
| استبدالالقلب بـ Like/Dislike | OWNER CONFIRMED |
| H6:رسائلإدارةمستقلة، هويةإداريةرسمية، تبويبخاصوإشعارخارجي | OWNER CONFIRMED؛ مقترحدعمشخصيرُفض |
| H7:الفريقيصممالأوزانمنكلالإشاراتثم يعرضها | DESIGN AUTHORIZED؛ أرقامغيرمعتمدة |
| H8:admin/admin مؤقت، إعدادات username/password/email؛ التغييرقبلالإطلاقالعام وفقردالقائد | OWNER CONFIRMED؛ تنفيذحسابغيرمثبت |
| H9:نظامالوثائقوالبياناتمنواجهةالمدير؛ الحقيقياتبعدالإطلاق | OWNER CONFIRMED؛ لاادعاءبنك/KYC منجز |
| التعليقاتمفتوحة؛ video_offset وتشغيلمتزامن وقائمةأخيرةزمنية | OWNER CONFIRMED |
| الإجراءاتالفعليةللبنك/المزوّد/الكيان والإطلاق | EXTERNAL/LATER — لا تفترضإنجازها |

## سجل التنفيذ

| الوحدة | base SHA | PR/HEAD | REMOTE ودليله | merge SHA | المتبقي |
|---|---|---|---|---|---|
| R3-B7 | يرجعلسجل#75 | #75 / c8f8e86f592ddf3a593b52fd5c88156c9ad3a6a7 | قرارالمراجع يرجع لسجل القائد؛ لااختبارجديد هنا | d19204738407657c97f6ba6ede9c601a3cbdb644 | Guest منجزة#76؛ تمديد Home في RAILS، لا يعاد Explore |
| R3-GUEST-1 | d19204738407657c97f6ba6ede9c601a3cbdb644 | #76 / a39966a92a129591d672c690668d83067fb078da | وكيلان مستقلان: APPROVE؛ T+B ar/en، continuation حتى النفاد، reuse #75، لا blockers | 79edbf2ffd3ee0755a9b35c6fd20d5e62acd7ff5 | تجربة المالك PASS |
| R2-AUTH-1 | 79edbf2ffd3ee0755a9b35c6fd20d5e62acd7ff5 | #77 / 98e3ba012e61feede45e5c8005ac46ff8332a0f4 | وكيلان مستقلان: APPROVE؛ real-D1 integration مثبت، TTL/NULL clearing/one-time PASS، لا blockers | 1376c045adaf901ad9b266741789665f0137f3f8 | وصول Spam بحسب تقرير المالك؛ لا تحقيق Inbox الآن أو منع J |
| EMAIL-DOMAIN | 1376c045adaf901ad9b266741789665f0137f3f8 | [#78](https://github.com/Maelsh/dueli-opus/pull/78) / 47203de37c470088cb559049cb4ffefe6ed4ac87 | APPROVE مستقل وفق تقرير القائد؛ هذه المراجعة للملفات فقط | f3942c3bbe450bf3c727a235fe37a46bdf9be9b1 | لا تغيير مزود/DNS |
| DEPLOY-RECOVERY | f3942c3bbe450bf3c727a235fe37a46bdf9be9b1 | [#79](https://github.com/Maelsh/dueli-opus/pull/79) / f928f2ab4e2ffde5f364570cd06f195d658bf900 | APPROVE مستقل وفق تقرير القائد؛ هذه المراجعة للملفات فقط | af96b8f06fd6920e435384af444c857bf8492dc9 | تحسينات الإصدار المحددة في R-RELEASE-1 |
| EMAIL-UX / HOME-FORENSIC | af96b8f06fd6920e435384af444c857bf8492dc9 | [#80](https://github.com/Maelsh/dueli-opus/pull/80) / b0cb64296c83a3da98fe5f72cd303c179c8b544f | APPROVE مستقل وفق تقرير القائد؛ هذه المراجعة للملفات فقط | b23cfe2a9202136f47da08d55fecee74e259f979 | استمرار Home في RAILS؛ UX لا deliverability fix |

القائد يثبت main قبل التكليف ويحدث هذه اللوحة بعد كل LOCAL/REMOTE/دمج. حالات OPEN/IN PROGRESS/REMOTE/REJECT/DONE/ALREADY DONE/BLOCKED DEVICE/H/DEFERRED بدليلها؛ وجودمكونخلفي لايغلقرحلة.
T/B أولاً؛ S للصورةوالصوتوالجهازالحقيقي فقط؛ H للإجراءالبشري. لا Astra للرانك/النجوم/الصلاحيات/التمرير، ولابوابات مغلقةتعاد.

ملاحظة النطاق: #77 تخص استعادة المنسي وتطبيع البريد والعقد العام؛ لا تعني إنشاء رحلة تغيير كلمة المرور داخل الحساب إن كانت مفقودة. أي ناقص واجهة مثبت يبقى ضمن R2-F، ولا إعادة Auth gate.

قرار المالك الأخير: كل قسم وفرع يخضع للأوزان؛ frozen session لا تعني نتائج ثابتة في كل زيارة. RANDOM-only ليس قبولاً نهائياً؛ نتيجة continuation لا تغلق weighted Home المطلوبة في D1. انظر08.

## مزامنة #81/#82 — 2026-10-03

| الوحدة | الدمج | main Quality | النشر / الإغلاق |
|---|---|---|---|
| R-RELEASE-1 | MERGED #81 / daa449b85d22704326a31d0d644ee45542dbc3b5 | PASS run37084529534 | POST-MERGE BLOCKED: deploy fail، لا DONE تشغيلي |
| R3-RAILS-1A/1B | MERGED #82 / cb80789b20c3f766b3deec8b16d7ed8393aa57ed | FAIL run37125477474، assertion ساعة واحد؛ PR head05b8c80 PASS | POST-MERGE BLOCKED؛ continuation code merged، لا إغلاق weighted Home |
| R-RELEASE-1-REM1 | NEXT / PLANNED | workflow/clock remediation محددة | وفق10؛ D0 تصميم مستقل مستمر |

Cloudflare check id111209903606 سجل deployment ناجحًا لنفس cb80789 قبل اكتمال Quality الفاشلة؛ لا production verification هنا. تفسير الصورة والأدلة في10. لا إعادة TURN gate أو إعادة تنفيذRAILS. سجّل run/event/SHA لكل نجاح، وتميّز حالة MERGED عن DEPLOYED.

السجل لكل دمج تالٍ: UNIT/PR/BASE/approved HEAD/tested candidate+event/REMOTE/merge SHA/main Quality run/deploy environment+SHA/status/blocker/NEXT.
