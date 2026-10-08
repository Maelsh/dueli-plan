## 2026-10-08 — PR106 and owner visual findings (pending production gates)

- **CODE PR#106 R4-EVENTS-NOTIFY-1 MERGED** on `375bd1809482d21ce2abd4aa7e6c013704967e50`; independently approved remediation HEAD `253a1b724d8f36f6f40eaee3eadb4145982abe56`. PR Quality Gate #37794609452 SUCCESS, preview Deploy #37794609471 SUCCESS. Post-merge Quality Gate #37799232295 and production Deploy #37799232315 were IN PROGRESS at last check; do not mark DEPLOYED/DONE before both success. Owner-authorized old-notifications cleanup cutoff `2026-10-08T03:31:39Z` still NOT EXECUTED; SQL reviewed conditionally, production schema/count guard required.
- **OWNER VISUAL NEW FINDINGS** (screenshot competition/2201?lang=ar, authenticated): authenticated top-bar Help icon duplicated with account-menu Help, hurts mobile layout; retain top-bar Help for guests only. Arabic page shows raw English `Reminder On` on a **completed** competition; require ar/en translation via t()/translations and lifecycle-aware hide/disable of reminder on completed state, plus RTL/mobile/a11y regression. Screenshot also shows VOD spinner; investigate availability/state separately under MEDIA, not proof of unavailable recording.
- **NON-NEGOTIABLE AGENT CONTRACT**: before changing UI read CODE `AGENTS.md`, `docs/01-ARCHITECTURE-RULES.md`, `docs/11-DEFINITION-OF-DONE.md`, `docs/13-TEST-STRATEGY.md`, `docs/18-REPOSITORY-CHANGE-POLICY.md`, relevant 00/16, and PLAN 08/10/12; enforce MVC/OOP, no SQL in controllers/pages, ar/en i18n, RTL/LTR, accessibility/aria, mobile and dark mode. Agent chat reports ≤5 short evidence items + STATUS/PR/HEAD/BLOCKERS/NEXT; long evidence in repo only.

## 2026-10-08 — LEADERSHIP SYNC: PR103–105 (verified GitHub)

- **CODE MAIN** `5a74310667bfed286cc1f1ba0dfa450be1bb041b`. PR#103 title escaping **MERGED** `9cbb93c5c05103f30466d10aa5fd59f639bcc3ea`, Quality Gate/Deploy **SUCCESS** (runs 37760838270/37760838240).
- **R4-DB-DIAG-1** report received, local EXPLAIN and query diagnosis only; **DB-01 OPEN**: no actual production before/after D1 rowsRead/rowsWritten/executions, quota recovery alone not resolution.
- **R4-DB-OPT-1 PR#104** **MERGED** `30baed309ee5e6a932c5c5d88d819411c9a63f55`. Owner-authorized production migration `0039_r4_db_opt1_indexes.sql` applied to `dueli-db` by LOCAL; SHA256 `ddf4ac98cc2ebf2bd9ad987e65d1c30239ed1570e6487bb8af39755112f58ca9`; journal 39→40, pending none, indexes 107→113 (+6), reported users 561/competitions 1542/tables 67 unchanged. REMOTE independently reviewed logged evidence; no direct D1 credentials. Quality Gate success but production Deploy **FAILED** run 37771438709: collector omitted six required indexes from snapshot, not a confirmed missing migration.
- **Release collector hotfix PR#105** **MERGED** `5a74310667bfed286cc1f1ba0dfa450be1bb041b`. Unrestricted `sqlite_master` index snapshot; regression tests 5/5 + workflow 9/9; REMOTE APPROVE exact `fae3981d591044a59d7c2450d4c86c10c4e0fa7d`. **Post-merge Quality Gate SUCCESS** run 37774306486; **Deploy SUCCESS** run 37774306356. Release incident closed; DB-01 capacity issue remains OPEN.
- **Recurring failure prevention**: #458 (baseline 0034) and #37771438709 (0039) had same class of incomplete release-index snapshot. Before any manifest/index migration merge, leadership MUST cross-check full required_schema.indexes against the actual collector's scope, read prior release failures and confirm regression using new tables outside required_schema.tables; green preview alone does not prove production readiness.
- **NEXT R4-EVENTS-NOTIFY-1**: LOCAL prompt issued; PR/HEAD not yet received. Preserve owner-approved one-time notification read cleanup cutoff `2026-10-08T03:31:39Z`, **NOT EXECUTED**; leader reviews exact SQL/runbook before write. N-03 disputed targeted check; N-07 targeted. Follow 08/10/12. Other closed phases remain closed.

# Dueli — لوحة التنفيذ والقرارات

> **الحالة الحالية — 2026-10-08:** R2 ووحدات R3 منفذة ومغلقة وفق04، بما فيها D1/D2 وC1/C2/C3. R4 كشف عيوبًا جديدة محددة؛ خطة الاستعادة في [12-R4-RECOVERY-PLAN.md](12-R4-RECOVERY-PLAN.md). NEXT: **R4-DB-DIAG-1**. PR#103 OPEN؛ لا تعاد الأعمال المغلقة. الفوترة ونقلDB والسياسة الدائمة للإشعارات غير معتمدة؛ تنظيف الإشعارات القديمة مرة واحدة معتمد في08/12 §10، ولم ينفذ من تحديث الخطة.

> **H7 معتمدة وثابتة:** السياسة الرقمية في11، وD0/D1/D2 مغلقة وفق04. لا إعادة تصميم أو اعتماد الأوزان؛ تحسين الاستهلاك يحفظها.

**مزامنة بعد PR#102 — code main `2e3d3681093a591e917dd1c57dc9cc249c307458`؛ 2026-10-08.**08 مرجع القرارات؛12 الاستعادة الحالية. دمج الخطة لا يعني تنفيذها.

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
| incident 0033 | REMEDIATED؛ حمايةrelease مدموجة وفق04/10، لا تخلط مع حادثdaily read quota الجديد |
| Home rails | continuation وH7 منفذتان؛ عيب بطء وبناء جلسات متكرر محتمل يعالج موضعيًا في12، لا إعادةRAILS/D1 |
| R0 قرارات المنتج | OWNER CONFIRMED في08/11، بما فيها H7؛ الإجراءات الخارجية منفصلة ولم يثبت إنجازها |
| R2/R3/R4 | R2 ووحداتR3 مغلقة وفقسجلPRs؛ R4 IN RECOVERY/ACCEPTANCE —12 |
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
| R3-D0 | DOCS DONE / OWNER APPROVED؛ D1/D2 منفذتان ومغلقتان؛ h7-v1 ثابتة |
| R3-D1 | CODE DONE / DEPLOYED #96 + REM1 #97 — h7-v1 لأسطح اكتشاف المنافسات؛ #96 merge 1c84bc4ec416fcc636508a644b418682cffb9e37؛ REM1 أغلق Unicode search وfav namespace وH2 view-writer invariant والتعليق؛ #97 merge f8c7add89409a65ae04546e4cbc8d2c927fc1f54؛ Quality#250 + Deploy#479 SUCCESS |
| R3-D2 | CODE DONE / DEPLOYED #98 — Profile actual-participation SSOT + user/opponent/follow/participation H7 + frozen sessions؛ REMOTE REJECT ثم FIX ثم APPROVE×2؛ merge d5233f44de9b24ecd0d4b327c2b740b40057d7e2؛ Quality#253 + Deploy#482 SUCCESS؛ لا migration |
| R3-C1/C2 | CODE DONE / DEPLOYED #99/#101 وفق التحديثات أدناه |
| R3-C3 | CODE/DOCS DONE / DEPLOYED #102؛ design only؛ لا runtime deletion |
| R4 | IN RECOVERY / NOT ACCEPTED؛ عيوب جديدة محددة وخطة12؛ PR103 OPEN |

**NEXT: R4-DB-DIAG-1** وفق12؛ متابعةPR103 القائمة مستقلًا؛ R0 بالتوازي. H7/D1/D2/C1/C2/C3 مغلقة.

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


## تحديث 2026-10-06 — R3-D1 / REM1

- R3-D1 #96: APPROVE مستقل؛ merge `1c84bc4ec416fcc636508a644b418682cffb9e37`؛ H7-v1 مطبقة على أسطح اكتشاف المنافسات، الجلسات frozen/exhaustion بلا سقف، لا migration.
- R3-D1-REM1 #97: الأربع ملاحظات المعروفة CLOSED بتحقق مستقل: Unicode word boundaries ar/en، حجز `fav:`، توحيد counted-view writer وفق H2، وتصحيح تعليق H7SignalsModel. merge `f8c7add89409a65ae04546e4cbc8d2c927fc1f54`؛ Quality #250 SUCCESS؛ Deploy #479 SUCCESS؛ لا migration.
- ملاحظة REMOTE غير مانعة: tokenless guest requests قد تنشئ هويات ضيف جديدة وفق semantics الهوية القائمة؛ ليست regression في #97 ولا يعاد فتح REM1 بسببها، وتراجع فقط إذا دخلت نطاق وحدة لاحقة.
- NEXT التاريخي عند تسجيل هذا التحديث: **R3-D2** وفق03/05/08/11؛ لا إعادة تصميم H7.


## تحديث 2026-10-06 — R3-D2

- PR #98: BASE `f8c7add89409a65ae04546e4cbc8d2c927fc1f54`؛ approved final HEAD `a7f926b8b8f6ef6146376c75a572daa985e172f7` بعد REMOTE REJECT وإصلاح ثلاثة blockers: actual participation=`started_at IS NOT NULL`، language-layer gating للخصم، وcandidate-missing Profile=0.5 عند availability session-wide.
- إعادة REMOTE من الوكيلين: APPROVE / MERGE-SAFE YES؛ لا blockers ولا migration.
- merge `d5233f44de9b24ecd0d4b327c2b740b40057d7e2`؛ main Quality #253 SUCCESS؛ production Deploy #482 SUCCESS على نفس SHA.
- R3-D2 CODE DONE / DEPLOYED. H7 D0/D1/D2 مغلقة. NEXT: **R3-C1**؛ C2/C3 بعدها وفق03، وR0 يبقى بالتوازي.


## تحديث 2026-10-07 — INCIDENT D1-100 / PR #100

- بعد نشر #98 ظهر في الإنتاج POST /api/home-rails/sessions = 500 لبعض الصفوف الكبيرة؛ #99/C1 كان مفتوحاً وغير مدموج، فأوقف الدمج ولم يُنسب الحادث إليه.
- التحقيق الخارجي أثبت السبب: Cloudflare D1 يسمح بحد أقصى 100 bound parameters لكل statement؛ بعض SQL الديناميكية كانت توسع قوائم IDs فوق الحد. ظهر الخلل مع حجم بيانات الإنتاج، بينما node:sqlite المحلي لم يكن يحاكي الحد.
- PR #100 أغلق الفئة المعروفة: NOT EXISTS anti-joins للمدخلات غير المحدودة، وchunking آمن للhydration/loads مع حفظ الترتيب، وحارس اختبار دائم: >100 يفشل و<=100 يمر.
- REMOTE مستقلان: APPROVE / MERGE-SAFE YES على HEAD b1b1a0235a4fc59e7c36a4fe2565b5320e3f920d بعد تدقيق dynamic-bind sites؛ لا production-reachable valid-data query معروف يتجاوز 100 binds.
- merge 3fac1e360d144dc46acb99d50c658afb0ff65e3d؛ main Quality #258 SUCCESS؛ Deploy #487 SUCCESS؛ لا migration/schema/config write.
- قاعدة دائمة: احسب إجمالي binds في statement (كل القوائم المكررة + scalar binds)، لا batch size فقط. المدخل الصالح غير المحدود لا يوسع مباشرة إلى placeholders؛ استخدم anti-join أو chunking يحفظ semantics والترتيب.
- #99/R3-C1 بقي OPEN/HOLD بلا تغيير أثناء الحادث؛ بعد #100 يحدث على main الجديد ويحتاج delta/integration verification فقط ما لم تغير التعارضات سلوكه، لا إعادة المراجعة الكاملة.
- الحالة: D1-100 CODE DONE / DEPLOYED. NEXT: تحديث #99 على main ثم delta verification وفق10.


## تحديث 2026-10-07 — R3-C1

- PR #99: C1 help/accessibility؛ approved pre-integration C1 HEAD `77dca79c1e9fb34cbe910568ade9dc98764afff5`، ثم حُجز الدمج أثناء حادث #100 دون نسبة الحادث إليه.
- بعد إغلاق #100 وتحقق الإنتاج، دُمج main في #99 فقط؛ final candidate HEAD `91eb729cb9314b65511082efd609c908a75c0791`. REMOTE delta APPROVE / MERGE-SAFE YES: لا source/function overlap مع #100، وC1 وD1 guards محفوظة، ولا migration.
- merge `d7021aee56c8fec2f63c0a8865b6b83ac4474db0`؛ main Quality #260 SUCCESS؛ Deploy #489 SUCCESS على merge SHA.
- R3-C1 CODE DONE / DEPLOYED. لا إعادة C1 أو #100.
- NEXT التاريخي عند تسجيل هذا التحديث: R3-C2 وفق03/05/08 H9؛ افحص ما أنجزه R2-A في managed documents ثم نفّذ الناقص فقط، ولا تعاود بناء الموجود.


## تحديث 2026-10-07 — R3-C2

- PR #101 أكمل C2 فوق managed_documents الموجود من R2-A دون نظام موازٍ أو migration. final HEAD `6c3e3dbeee76890da576114933b031b8519d2bd8`؛ REMOTE ×2: APPROVE / MERGE-SAFE YES.
- merge `88461f6afd3546650b7be1e3801d0d5f5dfc0770`؛ main Quality #262 SUCCESS؛ Deploy #491 SUCCESS. R3-C2 CODE DONE / DEPLOYED.
- Deferred non-blocking إلى R4/عند الحاجة: مراجعة مركزية لتهريب `<title>` عبر generateHTML/callers مع تجنب double escaping؛ `/docs` pagination فقط عند نمو catalog فعلياً. لا يُسجّل تحويل SEC grace-period إلى blocking كدين مطلوب؛ بعض الحراس لتقنيات غير مستخدمة وقد تكون non-blocking عمداً.
- NEXT التاريخي عند تسجيل هذا التحديث: R3-C3 حسب 03/05/08: synthetic retirement future design/documentation only؛ لا deletion/migration/production write.


## تحديث 2026-10-07 — R3-C3

- PR #102 وثّق تصميم Synthetic Retirement المستقبلي فقط؛ لا runtime deletion أو migration أو production write. final HEAD `cdbecebeba23acf840dac20c8342b2be41c4a1ab`؛ REMOTE ×2 APPROVE / MERGE-SAFE YES.
- merge `2e3d3681093a591e917dd1c57dc9cc249c307458`؛ main Quality #264 SUCCESS؛ Deploy #493 SUCCESS. R3-C3 CODE/DOCS DONE / DEPLOYED.
- التصميم المستقبلي fail-closed، dry-run إلزامي، وتصريح المالك مطلوب عند التنفيذ؛ هذا الإغلاق لا يفوض أي حذف مستقبلي.
- R3 C1/C2/C3 CLOSED. NEXT: R4 وفق 01/03/04/05/08/10؛ لا إعادة فتح الأعمال المغلقة دون blocker جديد محدد.

## الحالة النشطة — 2026-10-08 / R4 recovery

- مرجعCODE المثبت: `2e3d3681093a591e917dd1c57dc9cc249c307458`. PR#103 OPEN؛ HEAD `d020d8c4febdf778fabfe592dd11f40ed48add4a`. لا merge أو deploy لها وقت القراءة؛ لا إصلاح مكرر.
- نتائج المتصفح: NOT READY وفق ملخص القائد؛ عيوب12 لا تعيد المراحل المغلقة. الإدارة BLOCKED ACCESS؛ VOD يحتاج فحص عينة، لا FAIL شامل.
- استهلاكD1 منقول من مساعدCloudflare/جدول المالك: 1+2 يمثلان48.5%، أعلى عشرة73.4%. الأرقام الساعية/executions متناقضة في تقرير لاحق؛ لا تستخدم لتحديد الزوار أو سببfull scan دون دليل. القراءة المباشرة للمخطط غير متاحة هنا.
- **NEXT: R4-DB-DIAG-1 — PLANNED**؛ ثمOPT وفق الدليل. وحداتR4 الأخرى PLANNED في12، لا نفترض تنفيذها.
- DB-HOSTING/NOTIFICATION-CLOSED POLICY/ADMIN ACCESS: OPEN؛ لا تغيّرقرارات08/11 ولا تمنح production write.
- انتهى حوار مساعدCloudflare؛ يكمل LOCAL الفحص المحدد، لا جولات إحصاء واسعة أو تعطيل العمل لتصحيح عدد الزوار.
- القائد يحفظ أي حالة LOCAL/REMOTE أحدث وPLAN/CODE SHA قبل handoff. تقدير5–9أيام مشروط، لا موعدإطلاق مضمونًا.


## متابعة تقرير PDF الأصلي وقرار المالك — 2026-10-08

PLANNED/OPEN: تفاصيلPDF علىSHA2e3d368 أضيفت إلى12 §10 ضمن وحدات الاستعادة القائمة: M-04/M-05، N-05/N-06/N-07، VOD-02، VIS-02/VIS-03، U-04/U-05، S-02، وcreate feedback/degraded UX/discoverability. لاCODE DONE من تحديث الوثائق.

N-03 = DISPUTED / TARGETED CHECK: PDF يثبتone-click للقرار بينما الملخص ينفيه؛ القائد يحسم علىHEAD الحالي بعينة محددة للدور والحالة داخلEVENTS-NOTIFY.
تنظيفnotification read قبل2026-10-08T03:31:39Z = OWNER APPROVED / NOT EXECUTED؛ التفويض المحدود في08 و12 §10.2، ولا تنظيف رسائل أو حذف بيانات.
DB-01 = OPEN رغم عودة الخدمة بتقرير المالك؛ تشخيص وخفض الاستهلاك وقبول ميزانية مقاسة ما زالت مطلوبة.
NEXT المرجعي R4-DB-DIAG-1 ثمOPT؛ إن بدأ القائد بالفعل لا يعاد التكليف ولا يلغى عمل نشط. يحدث حالةLOCAL/REMOTE/PR من الواقع الحالي قبل أيprompt جديد.


## متابعة R4-DB-DIAG-1 — تقرير LOCAL 2026-10-08

LOCAL READ-ONLY REPORT RECEIVED / LEAD REVIEW PENDING؛ بلا PR/كود/إنتاج. EXPLAIN محلي يثبت مسارات scan لratings competitor وcompetitions creator/opponent وusers active وreverse blocks وفرز SSE؛ T0/بحث كامل وpolling مصادر تضخيم. HEAD المحلي d020d8c والشجرة متسخة بملفات غير ذات صلة؛ نتائج DAU تقديرية وليست قياس rowsRead/rowsWritten. **DB-01 OPEN؛ NEXT: مراجعة التشخيص وتحديد OPT-1، لا إعادة DIAG**. التفاصيل والقيود بجوار الوحدة في12 §10.5.

**OWNER PROCESS DECISION:** سجل الملاحظات بجوار وحداتها في ملفات الخطة لا في المحادثة؛ كل موجه للوكلاء يطلب تقريرًا مختصرًا جدًا مع إحالة الأدلة التفصيلية لملفات المستودع. راجع 10 §12 و12 §10.6. PR#103 ما زالت OPEN ولم تُدمج، وS-02 يحتاج حسمًا؛ تنظيف الإشعارات القديمة معتمد ولم ينفذ.
