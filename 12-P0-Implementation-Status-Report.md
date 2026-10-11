# 12 — تقرير حالة التنفيذ: المرحلة P0 (نواة المستودع والنزاهة)

**من:** Agent 2 — Technical Gate & Implementation Lead
**إلى:** Product Director
**التاريخ:** 2026-09-05
**الحالة:** ✅ **P0 مكتملة — بوابة الخروج محقَّقة — بانتظار إذن الانتقال إلى P1**
**المرجعية:** 10 §9.2 (تعريف P0 وبوابة خروجها) · 10B §2.1 (ENF-A1-02/06/07) · A-1 §3/§6 · أمر PD (8 شروط)

---

## 0 — الخلاصة التنفيذية

| البند | النتيجة |
|---|---|
| المستودع | أُنشئ **من الصفر** (Greenfield · PD-107) في `ERP-Platform/erp/` — 3 التزامات git، 40 ملفاً مُتتبَّعاً، 881 سطر كود منتج، 1,173 سطر اختبار |
| الكتالوج محمَّل بلا انحراف | **44 دوراً · 63 قاعدة (62 نشطة + PR-P-033 مسحوبة) · 27 آلة حالات (+ REVERSAL تقنية) · 22 رمز فشل (20 رسمياً + 2 تقنيان معتمدان في A-1)** — مُثبت على ثلاث طبقات: YAML ⇔ نصوص المرجعية (21 اختبار مطابقة) · YAML ⇔ قاعدة البيانات · الحزام |
| الجمود على مستوى DB (AR-005 · TD-3) | مُثبت: محفزات `ENABLE ALWAYS` على UPDATE/DELETE/TRUNCATE **+** سحب الصلاحيات من دور التطبيق `erp_app` — طبقتان مستقلتان، كل منهما مُختبَرة سلبياً |
| حارس ولاية `TEST` (PD-102 · A-1 §3) | مُثبت: قيد DB (محفز + CHECK) **+** حارس محرك؛ `TEST` مستحيلة في تنصيب `PRODUCTION`، واختُبر ذلك على قاعدة إنتاجية توأم |
| معايير القبول P0 | **AC-56 ✅ · AC-57 ✅** (اختبارات مُسمّاة، على مستوى النواة وعلى مستوى DB) — **2 من 70** |
| الأدلة | **119 اختباراً ناجحاً** على PostgreSQL 17.10 حقيقية (لا mocks) — مخرجات pytest في `erp/docs/evidence/` |
| قرارات وظيفية جديدة | **صفر** — لا قاعدة مخترعة؛ ما ظهر من مسائل مُدرج في §5 كمرشّحات تنتظر قرارك |

---

## 1 — ما بُني (مطابقةً لتعريف P0 في 10 §9.2)

| مكوّن P0 (10 §9.2) | التنفيذ | الموقع |
|---|---|---|
| إنشاء المستودع وهيكل المشروع | git على `main` · طبقات `kernel → catalog → platform → ledger → core` مع **قاعدة اعتماديات مُنفَّذة كاختبار AST** (T-8) | `erp/`, `tests/p0/test_dependency_rule.py` |
| Postgres + Alembic | PostgreSQL 17.10 · Alembic 1.19 · هجرة واحدة `0001_p0_foundation` (schemas `platform` · `ledger`) · **لا downgrade** للدفاتر (AR-005) | `erp/db/migrations/` |
| نواة Decimal/التقريب (ROU-01/04/05) | `Decimal` حصراً (حظر `float` في النواة كاختبار) · ROU-02 كمية بدقة 6 · ROU-03 الباقي لأكبر سطر · ROU-04 تحويل الإجمالي وأكبر باقٍ (اختبار خصائص 25 بذرة) · ROU-05 سطر موازنة واحد ≤ (وحدة صغرى × عدد الأسطر) وإلا `FAIL-BAL-01` · ROU-06 الدور `ACC.MISC.ROUNDING` حصراً | `erp/src/erp/kernel/money.py` |
| محمِّلات الكتالوج + اختبار المطابقة | الكتالوجات **بيانات** (YAML) لا كود · محمِّل مع تحقق بنائي (العدّ · AC-57 · ROU-06 · VER-03 · اتساق آلات الحالات · الأنواع المحظورة) · محمِّل إلى DB **مجمِّد المحتوى بالبصمة** (VER-03: نفس `(rule_id, version)` بمحتوى مختلف ⇒ رفض) | `erp/catalog/*.yaml`, `erp/src/erp/catalog/loader.py`, `erp/src/erp/platform/catalog_loader.py`, `tests/conformance/` |
| صلاحيات INSERT-only ومحفزات الجمود (AR-005) | آلية عامة `platform.make_append_only()` تسجّل الجدول في `platform.append_only_table` وتسلّحه: محفز `ER005` على UPDATE/DELETE/TRUNCATE بوضع `ENABLE ALWAYS` (يعمل حتى تحت `session_replication_role=replica`) + `REVOKE` من `erp_app` و`PUBLIC` · مطبّقة على `ledger.journal` · `ledger.journal_line` · `platform.audit_event` · `platform.installation` | الهجرة 0001 |
| نواة التدقيق | `platform.audit_event` بحقول C-19 (الفاعل · الدور · الهدف · الفعل · قبل/بعد · السبب · لقطة السياسة) · **سلسلة بصمات sha256** مع دالة تحقق `verify_audit_chain()` · INSERT-only | الهجرة 0001 |
| حارس ولاية `TEST` (A-1 §3) | `platform.installation` (صف وحيد يُعلَن مرة واحدة: `PRODUCTION`/`TEST` — جامد) · `platform.tax_jurisdiction` مع `params JSONB` **بلا قيم افتراضية** (PD-102) · محفز `ER102` يمنع `is_test` خارج تنصيب `TEST` · CHECK يمنع تنكّر الكود `TEST` كغير اختباري · حارس متماثل يمنع إعلان `PRODUCTION` مع وجود `TEST` · حارس محرك `guards.py` (`ProductionGuardViolation`) · `TEST` **تُزرع من مجموعة الاختبار حصراً** | الهجرة 0001 · `erp/src/erp/platform/guards.py` |
| CI مع قاعدة الاعتماديات | `scripts/ci.sh` (نفس الأمر محلياً وفي الأنبوب) + `.github/workflows/ci.yml` بخدمة Postgres 17 | `erp/scripts/`, `erp/.github/` |

### 1.1 هيكل قاعدة البيانات بعد P0 (15 جدولاً · 22 محفزاً · 10 دوال)

| المخطط | الجداول | الغرض |
|---|---|---|
| `platform` | `installation` · `tax_jurisdiction` · `failure_code` · `sm_definition` · `sm_state` · `sm_transition` · `forbidden_document_type` · `append_only_table` · `audit_event` · `alembic_version` | تنصيب · ولايات · سجلات الكتالوج · آلية الجمود · التدقيق |
| `ledger` | `account_role` · `posting_rule` · `posting_rule_line` · `journal` · `journal_line` | سجل الأدوار · القواعد المُصدَّرة · **هيكل القيد** (يُستكمل في P2 بالحسابات والمستندات والأبعاد) |

**قيود منفَّذة داخل DB (غير قابلة للتجاوز من التطبيق):**

| القيد | الآلية | SQLSTATE |
|---|---|---|
| AR-005 / PS-02 / VER-04 | محفز + سحب صلاحيات | `ER005` |
| ROU-01 · ROU-05 · AC-56 (مدين = دائن · سطر موازنة واحد ≤ العتبة · لا مبلغ أدق من الوحدة الصغرى · لا قيد بسطر واحد) | **محفز قيدي مؤجَّل `DEFERRABLE INITIALLY DEFERRED`** — يُفحص عند COMMIT فيُرفض القيد كله | `ER001` |
| AC-57 (قاعدة `Confirmed` لا تحمل سطوراً) | محفز على `posting_rule_line` | `ER057` |
| 08 §5/21 · 05 §0.3 (مستند التزام لا يملك حالة `Posted`) | محفز على `sm_state` + CHECK (`COMMITMENT ⇒ reaches_posted = false`) | `ER021` |
| A-1 Q-A2-02/03/04 · GAP-01 · PD-103 (لا نوع محظور في أي سجل) | جدول `forbidden_document_type` + محفز على `sm_definition` و`posting_rule` | `ERA01` |
| PD-102 / A-1 §3 (حارس `TEST`) | محفزان + CHECK | `ER102` |
| ROU-06 | CHECK: سطر على `ACC.MISC.ROUNDING` ⟺ `is_rounding_line` · لا `ACC.MISC.ROUNDING` في قوالب القواعد | `23514` |
| VER-01 · RES-03 | FK `(rule_id, rule_version)` إلزامي على كل قيد · `account_role` + `resolution_level 1…9` إلزاميان على كل سطر | `23503` |

### 1.2 ما لم يُبنَ عمداً (التزاماً بالأوامر)

| البند | السبب | الإثبات |
|---|---|---|
| Correction Document | ممنوع حتى A-2 — لا placeholder ولا تنفيذ جزئي | `ENF-A1-07` (5 اختبارات: كود · كتالوج · DB) + محفز `ERA01` |
| Opening Balance | GAP-01 — القدرة معتمدة (PD-106) والقواعد تنتظر A-2؛ **لم يُخترع دور 45** | نفسه؛ `len(roles) == 44` وثابت |
| Fixed Assets · إشعار المورد · Consignment-In | خارج النطاق — لا بنية تحضيرية | نفسه |
| أي شاشة / API | ليست في P0 (FastAPI من P5) | — |
| أي سلوك وظيفي غير محسوم | مثال: نمط كسر التعادل في التقريب (§5.1) مُعامَل كمعامل تقني معلَن، لا كقرار | `money.py` ROUNDING_MODE موثَّق بـ TD-11 |

---

## 2 — أدلة التحقق (مخرجات حقيقية)

**البيئة:** Python 3.13.14 · pytest 9.0.3 · psycopg 3.3.5 · SQLAlchemy 2.0.52 · Alembic 1.19.2 · PostgreSQL 17.10 (عنقود محلي `127.0.0.1:5432`). كل اختبار DB يُنشئ القاعدة من الصفر عبر Alembic ثم يحمّل الكتالوج — **لا mocks ولا SQLite**.

```
$ ./scripts/ci.sh
tests/conformance ........................ 21 passed in 0.21s
tests/p0 ................................ 87 passed in 0.94s
tests/belt .............................. 11 passed in 0.39s
tests -m "not db" ....................... 73 passed, 46 deselected in 0.46s
```
```
$ python3 -m pytest tests -q
119 passed in 1.46s
```

### 2.1 توزيع الاختبارات (119)

| الملف | العدد | ما يُثبته |
|---|---|---|
| `tests/conformance/test_catalogue_vs_authority.py` | 21 | مطابقة الكتالوج لنصوص 03/04/05/06/07/08/11 بالتعبير النمطي: 44 دوراً · 63 قاعدة · 22 رمزاً · 27 قسماً في 05 · **AC = 70** · POL = 22 · **حزام الثوابت = 84** (صفوف الجداول) + الثوابت النثرية |
| `tests/p0/test_kernel_money.py` | 41 | ROU-01…06 · حظر float · خصائص ROU-04 (25 بذرة) · مجموعة رموز الفشل |
| `tests/p0/test_dependency_rule.py` | 3 | قاعدة الطبقات T-8 · لا `erp/domain`/`erp/industry` في P0 · لا `float` في النواة |
| `tests/p0/test_db_foundation.py` | 30 | الجمود (المالك والتطبيق) · الصلاحيات · المحفز المؤجَّل · ROU-05/06 · VER-01/03 · AC-57 · المنع 21 · الأنواع المحظورة (5) · سلسلة التدقيق · حارس `TEST` (إيجابي وسلبي وقاعدة بلا إعلان) |
| `tests/p0/test_ac_p0.py` | 8 | **AC-56** (نواة ×3 · DB ×2) · **AC-57** (كتالوج · DB ×2) |
| `tests/p0/test_structural_absence.py` | 5 | **ENF-A1-07**: لا وحدة/صنف/دالة/جدول/عمود/صف سجل لأي قدرة مستبعَدة؛ الأسماء تظهر فقط في مواضع التحريم المُدرجة |
| `tests/belt/test_belt_p0.py` | 11 | شريحة P0 من الحزام (تعمل بعد كل سيناريو): ROU-01/05/06 · PS-02 · VER-01/03 · RES-03 · AC-57 · المنع 21 · لا انحراف كتالوج⇔DB · ENF-A1-02 · ENF-A1-07 · سلامة سلسلة التدقيق |

### 2.2 اختبارات الإنفاذ المطلوبة في P0 (10B §2.1)

| المعرِّف | الاختبار | النتيجة |
|---|---|---|
| **ENF-A1-02** | `test_test_jurisdiction_impossible_in_production_installation` (حارس المحرك + محفز DB + CHECK + جمود `installation` + رفض الإشارة إلى `TEST`) · `test_no_jurisdiction_before_installation_mode_declared` · حزام `test_belt_enf_a1_02_…` | ✅ |
| **ENF-A1-06** | `test_app_role_has_no_update_delete_privilege_on_posted_tables` · `test_app_role_update_attempt_is_a_privilege_error` · `test_posted_journal_cannot_be_updated_deleted_or_truncated_even_by_owner` · حزام `test_belt_ps02_ar005_…` | ✅ |
| **ENF-A1-07** | 5 اختبارات `test_structural_absence.py` + `test_a1_forbidden_types_cannot_enter_registries[×5]` + حزام | ✅ |

**سجل الأدلة الكامل:** `erp/docs/evidence/p0-pytest-20260905.txt` (المخرجات) · `erp/docs/evidence/p0-test-inventory.txt` (أسماء الـ119 اختباراً).

### 2.3 بوابة خروج P0 (10 §9.2) — التحقق بنداً بنداً

| شرط البوابة | الدليل | الحالة |
|---|---|---|
| الكتالوج محمَّل 44/63/27 (+20 رمز فشل) بلا انحراف | `test_registry_counts_match_catalogue` + `test_belt_catalogue_db_no_drift` (20 رسمياً + 2 تقنيان = 22) | ✅ |
| الجمود مُثبت على مستوى DB | ENF-A1-06 أعلاه | ✅ |
| حارس `TEST` مُثبت | ENF-A1-02 أعلاه | ✅ |
| AC-56 · AC-57 | `test_ac_p0.py` (8) | ✅ |

---

## 3 — تعديلات T-01 المنفَّذة في هذه المرحلة (تحريرية · لا وظيفية)

| المستند | التعديل | السبب |
|---|---|---|
| 10A §G · 10B §2 | عائلة MEX = **MEX-01…02** (لا MEX-03) | التدقيق الآلي على 07 §… أظهر معرِّفين فقط |
| 10B §2 | ملاحظة تدقيق: الـ84 = صفوف جداول الثوابت في 06/07 بالضبط؛ 10 ثوابت نثرية + RES-01…05 تُنفَّذ ضمن الحزام **دون تغيير الرقم 84** | نتيجة الاختبار `test_numbered_constraints_belt_is_84` |
| 10 / 10A / 10B | تسجيل A-1 في سلسلة الأسبقية وتحديث كل المواضع المتأثرة (تم قبل بدء الكود) | أمر PD |

---

## 4 — مطابقة شروط PD الثمانية

| # | الشرط | الالتزام |
|---|---|---|
| 1 | الإغلاق = 70 AC + حزام 84 — لا 98 | اختبار مطابقة يفشل إن انحرف العدّ عن 70 أو 84 |
| 2 | Correction Document ممنوع حتى A-2 ولا يُستعاض عنه | محفز `ERA01` + ENF-A1-07 |
| 3 | Fixed Assets وإشعار المورد: لا بناء ولا بنية تحضيرية | نفسه |
| 4 | `TEST` محظورة إنتاجياً بحارس صريح | ENF-A1-02 (DB + محرك) |
| 5 | قياس أداء قفل (كيان × صنف) في P5 | مُجدوَل — PERF-A1-01 في 10B §2.1 |
| 6 | أي فجوة جديدة تُرفع ولا تُسدّ باجتهاد | §5 أدناه |
| 7 | P0 من الصفر بلا مستودع سابق | 3 التزامات فقط، كلها بتاريخ اليوم |
| 8 | لا كود لسلوك وظيفي غير محسوم | §1.2 |

---

## 5 — مرشّحات Blockers / Functional Gaps الجديدة (تنتظر قرارك — لم يُبنَ عليها شيء)

> **لا شيء مما يلي يمنع بدء P1.** مُدرجة لأن الأمر (6) يقضي برفعها لا سدّها.

| المعرِّف | النوع | الوصف | ما فعلته الآن | المطلوب منك |
|---|---|---|---|---|
| **GAP-C-01** | **مرشّح FUNCTIONAL GAP** | **نمط كسر التعادل في التقريب غير محدَّد في المرجعية.** 06 ROU-01…06 تحدد *أين* يُقرَّب و*من يتحمل الفرق*، لكن لا تحدد نمط التقريب عند التعادل بالضبط (0.005 ⇒ 0.01 أم 0.00؟ HALF_UP / HALF_EVEN / …). يؤثر في كل سطر ممتد وكل تحويل عملة وكل توزيع قيمة | النواة تعمل بـ **`ROUND_HALF_UP`** كمعامل تقني واحد معلَن (TD-11) قابل للتغيير في سطر واحد — لا قرار وظيفي اتُّخذ | تأكيد HALF_UP أو تحديد نمط آخر (يفضَّل قبل P2 حيث يبدأ توليد القيود من القواعد) |
| **GAP-C-02** | **مرشّح FUNCTIONAL GAP** (ينتظر A-2 أصلاً) | **GAP-01 Opening Balance** — لا تغيير: القدرة معتمدة، القواعد غير مكتوبة | محظورة بنيوياً (`ERA01`) حتى A-2 | يُغلق في A-2 (مع Correction Document) |
| **NOTE-01** | ملاحظة نمذجة (لا قرار) | `CASH_SESSION` و`COST_OBJECT` يصلان إلى الترحيل دون حالة اسمها `Posted` (07: الجلسة تُرحَّل عند `Closed`؛ Cost Object يُرحَّل عبر معالم في 5 حالات). نُمذجت في الكتالوج بحقل `posting_states` بدل حالة `Posted` — **مطابق للنص، لا تغيير فيه** | موثَّق في `state_machines.yaml` | اطّلاع فقط |
| **NOTE-02** | ملاحظة عدّ (لا قرار) | 84 = صفوف جداول الثوابت بالضبط؛ 10 ثوابت نثرية + RES-01…05 تُنفَّذ ضمن الحزام نفسه دون تغيير الرقم الرسمي | 10B §2 مُحدَّث | اطّلاع فقط |
| **NOTE-03** | ملاحظة تقنية | رموز الفشل في DB موسومة `origin = AUTHORITY (20) / TECHNICAL (2)` كي يبقى الرقم الرسمي 20 قابلاً للتدقيق مع وجود FAIL-RULE-01/02 المعتمدين في A-1 | منفَّذ | اطّلاع فقط |

**لا BLOCKER — FOUNDATION CONFLICT** ظهر في P0.

---

## 6 — الخطوة التالية المقترحة

**P1 — البيانات الأساسية للمنصة** (10 §9.2): org · identity (السباعية · SoD · تفويض) · party · item/UoM/كمية مزدوجة/دفعات/تسلسلي/رموز أسباب · dimensions · currency/FX (`minor_unit` ينتقل إلى جدول `currency` ويُربط `journal` به) · policy engine (22 POL) · periods · numbering (NUM-01…07) · بوابة الخروج: مستند اختباري يمر بحراس الصلاحية/SoD/الفترة · **AC-35 · AC-37 · AC-38 · AC-67**.

**أطلب:** (أ) إذن الانتقال إلى P1، (ب) قرارك في **GAP-C-01** (نمط كسر التعادل) — يمكن أن يصل خلال P1 دون تعطيل، لكنه مطلوب قبل إغلاق P2.

---

*Agent 2 — Technical Gate & Implementation Lead · لا قرار وظيفي جديد · لا قاعدة مخترعة · لا شاشات · الكود في `ERP-Platform/erp/` @ `d7a8d94`*
