# Dueli — لوحة التنفيذ والقرارات

> **تحديث معتمد — 2026-10-04:** H7 الرقمية معتمدة في [11-H7-APPROVED-RANKING-POLICY.md](11-H7-APPROVED-RANKING-POLICY.md). D0 مكتملة وثائقياً؛ تنفيذ D1/D2 ينتظر دوره وجاهزية إشاراته. أي نص تاريخي يقول إن الأرقام غير معتمدة أصبح متجاوزاً. الحالة في04 وقرارات المالك في08.

**مزامنة بعد PR #86 — code main4c6ddd98fbab619470c124fe0e5da7ac2e1cb87c؛ 2026-10-05 UTC.** [08-OWNER-DECISIONS.md](08-OWNER-DECISIONS.md) مرجع القرارات، لا المقترحات القديمة. دمج الخطة لا يعني تنفيذ متطلباتها.

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
| R0 قرارات المنتج | OWNER CONFIRMED في08/11، بما فيها H7؛ الإجراءات الخارجية منفصلة ولم يثبت إنجازها |
| R2 وبقية R3/R4 | PLANNED؛ لا نعلن إكمالها من اعتماد السياسة |
| R5 | DEFERRED AFTER WEB LAUNCH |

#75–#80 merged مثبت من GitHub. إنتاج #80 وتطبيق migration0033 ونتيجة Spam/SPF/DKIM/DMARC مصدرها تقرير القائد/المالك؛ هذه المراجعة لم تتصل بقاعدة الإنتاج أو تفحص البريد الحي. لا إعادة تكليف Guest/Auth؛ لا ادعاء اكتمال بقية R2.

## الوحدات

| الوحدة | الحالة / الاعتماد |
|---|---|
| R3-GUEST-1 | DONE — PR#76 مدموج بعد APPROVE مستقل من وكيلين؛ تجربة المالك PASS |
| R2-AUTH-1 | DONE CODE — PR#77 مدموج بعد APPROVE مستقل من وكيلين وreal-D1 integration؛ وصول Spam رُصد وفق تقرير المالك؛ لا Inbox blocker؛ قرار تأجيل deliverability |
| R-RELEASE-1 | DONE AFTER REMEDIATION #83 — SEC-06 coverage، preview bindings، required schema gate، نفس SHA؛ T ومراجعة مستقلة |
| R3-RAILS-1A | CODE MERGED #82 / RELEASE RECOVERED #83 —؛ providers/context/filter على البنية القائمة؛ لا H7 coefficients |
| R3-RAILS-1B | CODE MERGED #82 / RELEASE RECOVERED #83 —؛ كل الصفوف حتى exhaustion؛ T+B؛ يجوز جمع A/B |
| R2-J | CODE DONE / DEPLOYED #85 — H3 والدعوة/القبول والسجل والواجهة؛ post-merge Quality#223+Deploy#452 |
| R3-EXPLORE-CONTEXT-1 | CODE DONE / DEPLOYED #86 — typed View All + subcategory/session context؛ REMOTE APPROVE×2؛ merge 4c6ddd98fbab619470c124fe0e5da7ac2e1cb87c؛ post-merge Quality#225+Deploy#454 |
| R2-L1 | CODE DONE / DEPLOYED #87 + release remediation #88/#89 — H1=300 ثانية، H2؛ تعليقات/حضور/مشاهدة؛ post-merge Quality#231 + Deploy#460 على fbc8607920a658cf58cb52a069b2dea7afae1765 |
| R2-V | CODE DONE / DEPLOYED #90 — تقييم 1..5 بعد 300s، تعديل حتى cutoff، live provisional ثم final exactly-once؛ merge 35ccd4f899e6687e780744505d0e7a6a83c3fef2؛ Quality#233 + Deploy#462 SUCCESS |
| R2-L2 | CODE DONE / DEPLOYED #91 — غرفة/وسائط/إعلان وLike/Dislike وتعليقات video-time؛ migration0035 مطبقة ومثبتة؛ merge fed9b939cd40472a945c9074618b5c7cc9984a27؛ Quality#236 + Deploy#465 SUCCESS |
| R2-A | CODE DONE / DEPLOYED #92 — admin/settings/roles/H9 documents؛ migration0036 مطبقة ومثبتة؛ merge c2c3e4c61338ffba66798ea27a7a94bafed21f9e؛ Quality#239 + Deploy#468 SUCCESS |
| R2-M | CODE DONE / DEPLOYED #93 — personal/admin messaging منفصلان؛ migration0037 مطبقة ومثبتة؛ merge ec27f722e1caea693597c6d341301e21efa2f333؛ Quality#242 + Deploy#471 SUCCESS |
| R2-P | CODE DONE / DEPLOYED #94 — طرق صرف محفوظة + ownership/snapshot/legacy؛ migration0038 مطبقة ومثبتة؛ merge 2497bdae4c25ade69852de73720138f9932bd680؛ Quality#244 + Deploy#473 SUCCESS |
| R2-F | CODE DONE / DEPLOYED #95 — الرحلات الأصلية المتبقية أغلقت بفحص+إصلاح موضعي؛ merge 17d6dd7c06b0fec7bc5b98425c0d2325d7f81a5e؛ Quality#246 + Deploy#475 SUCCESS |
| R3-D0 | DOCS DONE / OWNER APPROVED 2026-10-04 — h7-v1 في11؛ D1/D2 لم تنفذا |
| R3-D1 | PLANNED — أوزان جميع Home rails والأقسام والفروع بعد D0 وجاهزية الإشارات؛ استمرار وحده لا يغلق Home |
| R3-D2 | PLANNED — Profile=SUM نجوم/عدد منافسات، ترتيب المستخدمين ومطابقة التخصص |
| R3-C1/C2 | PLANNED — مساعدة/إتاحة ووثائق من لوحة المدير؛ الحقيقيات بعدالإطلاق حسب H9 |
| R3-C3 | PLANNED DESIGN ONLY — KEEP NOW ثابتة |
| R4 | PLANNED — قبول الرحلات الجديدة، تسليم مسؤول ببيانات غيرمؤقتة، إجراءات فعلية وقرار إطلاق |

**NEXT: R3-D1** بعد إغلاق R2-F ونشرها؛ R0 بالتوازي، D0 DOCS DONE / OWNER APPROVED.

## القرارات المثبتة

| القرار | الحالة |
|---|---|
| H1:5 دقائق=300 ثانية مشاهدة حية لنفس المنافسة | OWNER CONFIRMED |
| H2:مشاهدةواحدة/هوية/منافسة/يوم وحضورمستقل | OWNER CONFIRMED |
| H3:دعوةمعلقة تمنعطلباً موازياً وخصمواحد يغلقالبقية | CONFIRMED AS REPORTED BY LEAD/OWNER |
| H4:1..5 لكل طرف، قابلللتعديل حتىالنهاية بصوتفعالواحد | OWNER CONFIRMED |
| H5:نتيجةحيةمؤقتةظاهرة، ثم نهائيةعندالإغلاق | OWNER CONFIRMED |
| Profile=SUM النجومعبرالمنافسات÷عددالمنافسات، لاعددالمصوتين | OWNER CONFIRMED |
| Rank المنافسة=أثرجمعنجومطرفيها+المشاهدات+Like/Dislike، الوزنضمن H7 | OWNER CONFIRMED INPUTS + COEFFICIENTS في11 |
| استبدالالقلب بـ Like/Dislike | OWNER CONFIRMED |
| H6:رسائلإدارةمستقلة، هويةإداريةرسمية، تبويبخاصوإشعارخارجي | OWNER CONFIRMED؛ مقترحدعمشخصيرُفض |
| H7:الفريقيصممالأوزانمنكلالإشاراتثم يعرضها | OWNER APPROVED — h7-v1 في11 |
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

## سجل حادث #81/#82 التاريخي — عولج لاحقاً في#83

| الوحدة | الدمج | main Quality | النشر / الإغلاق |
|---|---|---|---|
| R-RELEASE-1 | MERGED #81 / daa449b85d22704326a31d0d644ee45542dbc3b5 | PASS run37084529534 | POST-MERGE BLOCKED: deploy fail، لا DONE تشغيلي |
| R3-RAILS-1A/1B | MERGED #82 / cb80789b20c3f766b3deec8b16d7ed8393aa57ed | FAIL run37125477474، assertion ساعة واحد؛ PR head05b8c80 PASS | POST-MERGE BLOCKED؛ continuation code merged، لا إغلاق weighted Home |
| R-RELEASE-1-REM1 | DONE #83 — السطر التالي تاريخي | workflow/clock remediation محددة | وفق 10؛ D0 تصميم مستقل مستمر |

Cloudflare check id111209903606 سجل deployment ناجحًا لنفس cb80789 قبل اكتمال Quality الفاشلة؛ لا production verification هنا. تفسير الصورة والأدلة في10. لا إعادة TURN gate أو إعادة تنفيذRAILS. سجّل run/event/SHA لكل نجاح، وتميّز حالة MERGED عن DEPLOYED.

السجل لكل دمج تالٍ: UNIT/PR/BASE/approved HEAD/tested candidate+event/REMOTE/merge SHA/main Quality run/deploy environment+SHA/status/blocker/NEXT.

## الحالة الحالية بعد #85 — مصدرGitHub والمالك

| الوحدة | mergeSHA | actual main Quality | actual production Deploy | الحالة |
|---|---|---|---|---|
| REM1/#83 | 861e8d7f212711a5eeaefa2c999d9c495ce9be47 | [#219 SUCCESS](https://github.com/Maelsh/dueli-opus/actions/runs/37135947624) | [#448 SUCCESS](https://github.com/Maelsh/dueli-opus/actions/runs/37135947630) | CODE DONE / DEPLOYED |
| MAINT/#84 | 4c0286209a321180689a29d31cc052cea7f448ae | [#221 SUCCESS](https://github.com/Maelsh/dueli-opus/actions/runs/37152320610) | [#450 SUCCESS](https://github.com/Maelsh/dueli-opus/actions/runs/37152320600) | CODE DONE / DEPLOYED |
| R2-J/#85 | 020eacc38e5d81676ed35e159e5662f9fc8aae94 | [#223 SUCCESS](https://github.com/Maelsh/dueli-opus/actions/runs/37158786428) | [#452 SUCCESS](https://github.com/Maelsh/dueli-opus/actions/runs/37158786451) | CODE DONE / DEPLOYED |
| R3-EXPLORE-CONTEXT-1/#86 | 4c6ddd98fbab619470c124fe0e5da7ac2e1cb87c | [#225 SUCCESS](https://github.com/Maelsh/dueli-opus/actions/runs/37266797252) | [#454 SUCCESS](https://github.com/Maelsh/dueli-opus/actions/runs/37266797256) | CODE DONE / DEPLOYED |
| R2-L1/#87 + release remediation #88/#89 | fbc8607920a658cf58cb52a069b2dea7afae1765 | #231 SUCCESS | #460 SUCCESS | CODE DONE / DEPLOYED |
| R2-V/#90 | 35ccd4f899e6687e780744505d0e7a6a83c3fef2 | #233 SUCCESS | #462 SUCCESS | CODE DONE / DEPLOYED |
| R2-L2/#91 | fed9b939cd40472a945c9074618b5c7cc9984a27 | #236 SUCCESS | #465 SUCCESS | CODE DONE / DEPLOYED |

#85 BASE: 4c0286209a321180689a29d31cc052cea7f448ae؛ APPROVED HEAD: e80e52bb8af67b2c546860e3b2dea2ae4493663f. REMOTE APPROVE و1156/1156 مصدرهما تقرير القائد؛ metadata وmain runs قرئت مباشرة من GitHub، وخطوة Deploy production فعلية SUCCESS وليست skipped. لا يدعي هذا السجل قبولاً بشرياً جديداً لرحلة J أو PROD VERIFIED لكل الأدوار.

#84 نقل checkout/setup-node إلى v7 وubuntu إلى 24.04؛ صيانة مغلقة. #83 أصلح workflow وانتظار Quality واختبار الساعة وبوابة جاهزية المخطط. صلاحيات Pages Edit + D1 Read للحساب المحدد مصدرها قرار وتقرير المالك؛ لم تفحص قيم الأسرار أو صلاحيات الحساب هنا.

ملاحظة topology: لا نعطل مسار Cloudflare افتراضياً؛ تحديد البيئة بالدليل وتفويض المالك يسبقان أي تغيير في dashboard. نجاح Actions لا يثبت تعطيل كل المسارات الموازية. القائد يرفق دليل topology الموجود في handoff إن كان قد حسمه.

R2-L1 أغلقت بعد #87 ثم release remediation #88/#89. R2-V أغلقت ونُشرت عبر #90؛ merge 35ccd4f899e6687e780744505d0e7a6a83c3fef2؛ Quality #233 SUCCESS وDeploy #462 SUCCESS. NEXT هو R2-L2.

## H7 — قرار المالك النهائي 2026-10-04

R3-D0: DOCS DONE / OWNER APPROVED — h7-v1 في11. D1/D2 لم تنفذا؛ تنفيذ الأوزان بعد جاهزية إشارات L1/V/L2 وفق ترتيب03. المفضلات الاختيارية من الإعدادات ضمن D1، ومؤشر المتنافس وعرضه ضمن D2 دون تبديل صيغة08. لا LOCAL/REMOTE جديدة أطلقت ضمن تحديث الخطة؛ NEXT لم يتغير.
