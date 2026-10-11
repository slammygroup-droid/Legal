# Technical Design v0.1 — ERP Platform (Greenfield)

**المُعدّ:** Agent 2 — Technical Gate & Implementation Lead
**النوع:** تصميم تقني — مخرج المرحلة 1 من البريف (`09` §8)
**الحالة:** ⛔ **بانتظار الاعتماد — لا كود قبل الاعتماد**
**التاريخ:** 2026-09-05
**المرجع الملزم:** `03` (Foundation) ► `08` (Baseline PD) ► `06`·`07` (دلتا v1.1) ► `04`·`05` (كتالوجات v1.0) · `01` مرجعي
**الوثائق المرافقة:** `10A-Capability-Register-v0.1.md` (قائمة القدرات) · `10B-Verification-Matrix-v0.1.md` (مصفوفة التحقق)

> **ما تفعله هذه الوثيقة:** تحوّل السلطة الوظيفية إلى معمارية ونموذج بيانات ومحركات وترتيب بناء.
> **ما لا تفعله:** لا تعيد تعريف أي قرار وظيفي · لا تخترع قاعدة · لا تبسّط قيداً لأنه مكلف · لا شاشات.
> كل عنصر تقني هنا يحمل مرجعه الوظيفي. ما لا مرجع له مصنَّف صراحةً كـ **قرار تقني** أو **سؤال مرفوع**.

---

## 0 — حالة البوابة

| البند | الحالة |
|---|---|
| قراءة الوثائق الثماني كاملة | ✅ (القسم 1) |
| قائمة القدرات المشتقة من `03` + الكتالوجين | ✅ `10A` |
| تصميم الطبقات الأساسية (§3.1 بند 3 في البريف) | ✅ الأقسام 3–6 |
| ترتيب البناء ومراحله مقابل معايير القبول | ✅ القسم 9 + `10B` |
| أسئلة/فجوات مرفوعة | ⚠ القسم 12 — **12 بنداً**، منها بند واحد يحجب مرحلة كاملة (GAP-01) |
| كود مكتوب | **صفر** — بانتظار الاعتماد |

---

## 1 — تأكيد القراءة والمرجعية

### 1.1 ما قُرئ

| الملف | الأسطر | الدور في هذا التصميم |
|---|---|---|
| `09-Agent-2-Handoff-Brief.md` | 198 | التعليمات والحدود |
| `08-Functional-Baseline-v1.1-PD-Approved.md` | 168 | قرارات PD-101…107 · الممنوعات الـ34 · المؤجَّل · GAP-01 |
| `03-ERP-Functional-Foundation-v0.1.md` | 817 | P1–P7 · C-01…C-24 · BR-001…907 · POL (22) · AC-01…42 · M-01…15 |
| `04-Posting-Rule-Catalogue-v1.md` | 877 | 43 دوراً · 57 معرِّف قاعدة · حل الحساب · FX · حالات الفشل |
| `06-Posting-Rule-Catalogue-v1.1-Revision.md` | 576 | C-01…C-12 · +6 قواعد −1 مسحوبة · RRI/OWN/BIL/RES-06/RSP/PPV/COS/DIS/SRC/ROU/PM · F-01…21 · AC-43…58 |
| `05-Document-State-Machine-Catalogue-v1.md` | 718 | آلات حالات 26 مستنداً · مصفوفة الموانع · أسباب الإلغاء · الصلاحيات المرجعية |
| `07-Document-State-Machine-Catalogue-v1.1-Revision.md` | 434 | الثلاثية · تعريف Posted · Completed/Closed · نموذج العكس · الترقيم · الأب/الابن · المركبة · SF-01…12 · AC-59…70 |
| `01-Motakamel-Decision-Register.md` | 472 | مرجعي — PD-001…005 · AR-001…006 · مواصفة كائن السياسة |

### 1.2 أرقام السلطة كما تحققتُ منها آلياً (grep على الملفات المنفصلة)

| العنصر | النص يقول | ما عددتُه | التعامل |
|---|---|---|---|
| أدوار الحسابات | 44 | 43 في `04` + `ACC.REV.DEFERRED` في `06` = **44** ✅ | تُحمَّل كسجل مغلق |
| قواعد الترحيل | 63 | 57 معرِّفاً في `04` + 6 جديدة في `06` = **63 معرِّفاً** (منها `PR-P-033` مسحوبة ⇒ 62 نافذة) ✅ | تُحمَّل 63 سجلاً؛ المسحوبة بحالة `WITHDRAWN` (الإصدار يقتضي حفظ التاريخ — VER-03) |
| حالات الفشل | 17 | **19 معرِّفاً** فريداً عبر `04`/`06` | أنفّذ بالمعرِّفات لا بالعدد — انظر Q-A2-09 |
| معايير القبول المرقّمة | 98 | **70** (AC-01…70) — الـ28 «المضافة» غير مرقّمة في أي وثيقة | Q-A2-01 — أُغطّي الـ70 صراحةً، وأطلب تعريف الـ28 |
| السياسات | 22 | **22** ✅ | كائن سياسة كامل المواصفة (`03` §7.1) |
| المستندات | 26 | 26 مدخلاً في كتالوج `05` (+ Reservation كسجل لا مستند) | أُنمذجها كـ27 نوعاً تقنياً (CN وDN نوعان بآلة واحدة) — Q-A2-08 |
| مستويات حل الحساب | 9 | 9 (`06` §5.2) ✅ | — |

### 1.3 ما طُبِّق من ترتيب الأسبقية أثناء القراءة (لا قرارات — تطبيق آلي للترتيب)

| الموضع | التعارض الظاهري | الحسم بالأسبقية |
|---|---|---|
| POL-MFG-001 الافتراضي | `03`: L1 في الموجة 1 · `01`: L2 | **L1** — Foundation أعلى |
| Stock Adjustment: حالة `Approved` | `07` §1.3 لا تذكرها في ملخص الثلاثية · `05` و`08` §5.3/27 تنصّان عليها | **موجودة** — `08` أعلى من `07`، و`07` §1.3 يُقرأ كملخص لا كحصر (تأكيد مطلوب — Q-A2-10) |
| Delivery: `Ready to Pick` | `07` §1.3 لا تذكرها · `05` تفصّلها | تبقى كما في `05` (نفس الأساس) |
| PR-P-033 | `04` تعرّفها · `06` تسحبها | **مسحوبة** — الدلتا أعلى |
| Q-01 / BLK-05 / `02` | `01` و`03` تذكران مستودعاً | **لاغٍ** — PD-107 |

### 1.4 قرارات PD المطبَّقة بنيوياً في هذا التصميم

| القرار | أثره التقني الملزم هنا |
|---|---|
| **PD-101** | محرك التكلفة يمنع الرصيد السالب على أصناف WMA بنيوياً؛ محرك السياسات يرفض تفعيل POL-INV-001 على نطاق يشمل صنف WMA (تعارض سياسة)؛ لا مسار كود يحوّل طريقة التقييم آلياً؛ PR-I-060/061 مقصورتان على FIFO |
| **PD-102** | Tax Engine بمعاملات ولاية **بلا قيم افتراضية** (`TAX_POINT_ADVANCE`، مستوى تقريب الضريبة، المعدلات)؛ أي ساق ضريبية بلا تهيئة ⇒ `FAIL-CFG-03`؛ الاختبارات تستخدم تهيئة موسومة `TEST` صراحةً لا افتراضاً |
| **PD-103** | لا كيان ولا مستند ولا قاعدة لمخزون المورد (Consignment-In). دفتر المخزون يحمل خاصية «ملكية» احتياطاً (BR-112 مملوك العميل) بلا مستند يستخدمها في الموجة 1 |
| **PD-104** | Approval Engine كبيانات: مسارات + شروط مسمّاة + عتبات تُقرأ من Policy Configuration؛ لا رقم مغروس |
| **PD-106 / GAP-01** | مستند الرصيد الافتتاحي **محجوز كخانة** (نوع مستند + مصدر طبقة `OPENING_BALANCE` معرَّفان بالاسم فقط، بلا آلة حالات ولا قاعدة). خطوة «الأرصدة الافتتاحية» في معالج التهيئة **محجوبة** بانتظار الملحق. لا مسار استيراد يكتب في الطبقات أو القيود خارج محرك الترحيل |
| **PD-107** | Greenfield: لا طبقة توافق، لا هجرة، لا فحص مستودع |

---

## 2 — المبادئ التقنية الحاكمة (مشتقة من P1–P7 والثوابت)

| # | المبدأ الوظيفي | نتيجته التقنية غير القابلة للتفاوض |
|---|---|---|
| T-1 | **P1 الحدث الذري** · AC-01 · AC-61 · CX-04 | كل انتقال إلى `Posted` = **معاملة قاعدة بيانات واحدة** تشمل: الكمية + الطبقة/التكلفة + القيد + البنود المفتوحة + الحالة + التدقيق + الحدث الصادر (Outbox). لا معالجة لاحقة غير متزامنة لأي أثر مالي أو كمّي. **هذا يفرض قاعدة بيانات علائقية واحدة ذات ACID، ويستبعد Microservices للنواة** |
| T-2 | **AR-005 · BR-003 · PS-02 · AC-64 · AC-58** | الجمود يُفرض على مستوى قاعدة البيانات لا الكود فقط: جداول القيود والحركات والطبقات والتدقيق **INSERT-only** (بلا صلاحيات UPDATE/DELETE لدور التطبيق)؛ والمستند بعد `Posted` محمي بمحفّز يرفض التعديل عدا الأعمدة المشتقة |
| T-3 | **VER-01…04 · REV-02** | كل سطر قيد يخزّن `rule_id` + `rule_version` + دور الحساب + الحساب المحلول + مستوى الحل. القواعد وآلات الحالات **بيانات مُصدَّرة** تُحمَّل من كتالوج مُدار بالإصدار، لا `if/else` في الكود |
| T-4 | **F-11 · RES-06 · BR-010** | لا يوجد في التصميم أي «حساب افتراضي» أو «حساب معلّق»؛ سلسلة الحل تنتهي بـ **فشل مهيكل** يوقف المعاملة |
| T-5 | **ROU-01 · F-20** | حساب عشري دقيق (Decimal) في كل مكان؛ **ممنوع Float**؛ الموازنة تُتحقق منها قاعدة البيانات نفسها (قيد مؤجَّل على مجموع القيد) |
| T-6 | **GS-01/02 · AC-59/60** | الحالتان الفرعيتان **تُشتقّان** بدالة واحدة داخل نفس معاملة الترحيل؛ لا واجهة برمجية لتعيينهما |
| T-7 | **P5 · PD-004 · §7.2** | لا مفتاح في الكود يغيّر سلوكاً محاسبياً. المرونة الوحيدة: كائنات السياسة الـ22 + معاملات الولاية الضريبية. تغيير قاعدة ترحيل = نشر إصدار كتالوج جديد بتاريخ سريان |
| T-8 | **P6 · §5.4/29** | حدود الوحدات تُفرض آلياً (اختبار اعتماديات في CI): `core` لا يستورد من `domain`، و`domain` لا يستورد من `industry` |
| T-9 | **P4 · BR-906 · AC-36** | كل سطر قيد يحمل مراجع مباشرة: المستند ← الحدث/الانتقال ← الفاعل ← لقطة السياسات. الوصول في ≤3 خطوات هو **عقد بيانات** لا ميزة تقرير |
| T-10 | **NUM-04 · CX-04** | الرقم يُسحب داخل معاملة الترحيل من عدّاد جدولي مقفول؛ فشل المعاملة يُرجع العدّاد ⇒ الفجوات نادرة، وكل فجوة مُفسَّرة في سجل الفجوات |

---

## 3 — المعمارية العامة

### 3.1 النمط: Modular Monolith سداسي (Hexagonal) فوق قاعدة بيانات واحدة

```
┌──────────────────────────── Interfaces (رقيقة) ────────────────────────────┐
│  HTTP API (OpenAPI)  ·  CLI/Setup  ·  Import/Export  ·  Webhooks (outbox)  │
└───────────────┬─────────────────────────────────────────────────────────────┘
                │ Application Services (أوامر/استعلامات · معاملة واحدة لكل أمر)
┌───────────────▼────────────────── CORE (C-01…C-24) ─────────────────────────┐
│ platform.*   : org · identity · party · item · dimension · currency · tax   │
│                document(framework+numbering) · workflow · policy · period    │
│                audit · events(outbox) · attachments · integration · setup    │
│ ledger.*     : gl(roles · resolution · rules · journal · reversal ·          │
│                milestone) · inventory(movements · buckets · pools · layers · │
│                costing · reservation/ATP · revaluation) · costobject         │
│ subledger.*  : openitems(AR/AP · allocation · aging) · advances · treasury   │
│ semantic     : metric registry · drill-down contract (Wave 1: الحد الأدنى)   │
└───────────────┬─────────────────────────────────────────────────────────────┘
                │ يستدعي Core فقط (لا العكس)
┌───────────────▼──────────── DOMAIN ENGINES (Wave 1) ────────────────────────┐
│ procurement · sales · inventory_ops                                          │
│ (fixed_assets: انظر Q-A2-02 · pos: الموجة 1.5 · manufacturing: الموجة 2)    │
└───────────────┬─────────────────────────────────────────────────────────────┘
                │ تهيئة + مصطلحات + قوالب فقط — بلا منطق محاسبي/مخزني
┌───────────────▼──────────── INDUSTRY PACKS (خارج خطة البناء هذه) ───────────┐
└─────────────────────────────────────────────────────────────────────────────┘
                     ▼ PostgreSQL (مصدر الحقيقة الوحيد · ACID)
```

**لماذا Monolith معياري لا Microservices:** الثابت T-1 يتطلب أن تقع حركة الكمية والطبقة والقيد والحالة في معاملة واحدة. توزيعها على خدمات يستلزم Sagas/تعويضات = «نصف أثر» مؤقت، وهو بعينه ما يمنعه P1. الحدود المعيارية الصارمة (T-8) تحفظ إمكانية الفصل مستقبلاً إن احتاج نطاق غير مالي (مثل التكامل أو الإشعارات).

### 3.2 قاعدة الاعتماديات بين الوحدات

| من | يجوز أن يستدعي | لا يجوز |
|---|---|---|
| `platform.*` | `platform.*` الأدنى (org ← identity ← …) | `ledger`, `subledger`, `domain` |
| `ledger.gl` | `platform.*` | `ledger.inventory` مباشرة (التكامل عبر محرك الترحيل الذي ينسّق الاثنين) |
| `ledger.inventory` | `platform.*` · واجهة `gl.posting` | `domain` |
| `subledger.*` | `platform.*` · `ledger.gl` | `domain` |
| `domain.*` | `core` عبر خدمات التطبيق والمستندات | وحدة domain أخرى مباشرة (عبر مستندات/أحداث فقط) |
| `industry.*` | تهيئة وقوالب فقط | أي كود يُغيّر أثراً مالياً أو مخزنياً |

**اختبار الحذف (P6/`01` §6.2)** يُنفَّذ آلياً: حذف مجلد `industry/*` يجب أن يترك مجموعة اختبارات Core وDomain خضراء.

### 3.3 الحزمة التقنية المقترحة (قرار تقني — يحتاج تأكيداً، انظر §11)

| الطبقة | الاختيار | المبرر المرتبط بالسلطة الوظيفية | البديل المكافئ |
|---|---|---|---|
| قاعدة البيانات | **PostgreSQL 17** | ACID · قيود مؤجَّلة لتحقق `مدين = دائن` · محفزات الجمود · صلاحيات INSERT-only · JSONB للتدقيق ولقطات السياسات · أقفال صفوف صريحة للمتوسط المرجح والترقيم · DDL معاملاتي للهجرات | — (لا بديل مكافئ في المتطلبات) |
| لغة النواة | **Python 3.13** (نمط Domain-first، بلا اعتماد إطار في النواة) | نوع `decimal.Decimal` أصلي بدقة مضبوطة (ROU-01…06) · `pytest` لـ70+ معيار قبول آلي · سرعة بناء عالية | **TypeScript/Node 20** (متاح أيضاً) — نفس التصميم يصلح بلا تغيير |
| الوصول للبيانات | SQLAlchemy Core + Alembic | SQL صريح (لا سحر ORM يخفي UPDATE) · هجرات مُصدَّرة | Drizzle/Kysely للبديل |
| واجهة HTTP | FastAPI (رقيقة، تُضاف بعد استقرار المحركات) | OpenAPI تلقائي للتكامل · لا منطق فيها | Fastify |
| الاختبار | pytest + Postgres حقيقي (لا SQLite) | المحفزات والقيود جزء من الضمانات ⇒ يجب اختبارها على المحرك الحقيقي | vitest |
| التنفيذ | حاوية واحدة + Postgres | بساطة التشغيل للشريك | — |

> ملاحظة بيئة: في مساحة العمل الحالية تتوفر Python 3.13 وNode 20 وpip وapt (PostgreSQL 17 قابل للتثبيت). Java المتاح 11 (قديم) و.NET غير متاح.

### 3.4 دقة الأرقام (قرار تقني ملزم)

| القيمة | النوع | القاعدة |
|---|---|---|
| الكميات (أساسية وثانوية) | `NUMERIC(24,6)` | ROU-02: التقريب لا يمس الكمية |
| تكلفة الوحدة / سعر الوحدة | `NUMERIC(24,10)` | ROU طبقة 1: سعر الوحدة يحتفظ بدقته الأعلى ولا يُقرَّب لإجبار إجمالي |
| المبالغ (معاملة/وظيفية) | `NUMERIC(24,6)` مخزَّنة · **مقرَّبة لدقة العملة** عند مستوى السطر الممتد | ROU طبقة 1 + FX-06 |
| أسعار الصرف | `NUMERIC(24,12)` | — |
| الوقت | `timestamptz` (UTC) + منطقة زمنية محلية مسجَّلة | `05` §0.6 |
| تاريخ المستند / التاريخ المحاسبي | حقلان مستقلان | `05` §10.4 · AC-05 |

---

## 4 — نموذج المعاملة الذرية (Posting Pipeline)

كل أمر تطبيق (`Transition(document, to_state, actor, reason)`) يمر بالخط التالي **داخل معاملة واحدة**:

```
 0  فتح المعاملة · قفل رأس المستند (FOR UPDATE) · تحقق الإصدار التفاؤلي · مفتاح Idempotency
 1  حراس الانتقال (State Machine Engine): الصلاحية <DOC>.<TRANSITION> · SoD · الفترة · الشروط المسمّاة
 2  تركيب الحدث (Event Composition): أي قواعد تنطبق على هذا الانتقال، وبأي شروط (RSP-03 قبل التخصيص)
 3  اختيار القواعد (RSP-01/02): الأخص يفوز · التساوي ⇒ FAIL-RULE-02 (مقترح) · لا قاعدة ⇒ FAIL-RULE-01 (مقترح)
 4  أقفال التكلفة: cost_pool لكل (كيان × صنف) بترتيب معرّفات ثابت (منع Deadlock) · أرصدة الحالات
 5  حساب الآثار الكمّية والتكلفة (Inventory Ledger): طبقات · متوسط · سلاسل مصدر التكلفة · موانع السالب (PD-101)
 6  بناء سطور القيد من قوالب القاعدة: مصادر المبالغ المسمّاة · الأبعاد الموروثة (04 §3.1) · FX (FX-01…06) · الضريبة (Tax Engine)
 7  حل الحساب لكل دور (9 مستويات) · تثبيت (دور · حساب · مستوى) في السطر · فشل ⇒ FAIL-CFG-02 مع سلسلة البحث
 8  التقريب (ROU-04 أكبر باقٍ · ROU-05 سطر موازنة ≤ عتبة وإلا FAIL-BAL-01) · تحقق مدين = دائن بالوظيفية
 9  الثوابت العابرة: RRI-01 (قاعدة إيراد واحدة بالضبط لكل سطر تسليم) · FAIL-OWN-01 · FAIL-REV-01/02/03 · DIS-03 …
10  الكتابة: journal + journal_line · inventory_movement + layer_* · open_item/allocation · milestone · document_link
11  سحب رقم المستند (NUM-04) من العدّاد المقفول · تحديث العدّادات الثلاثية على سطور الأصل (Ordered/Executed/Invoiced)
12  تغيير الحالة العامة · اشتقاق الحالتين الفرعيتين للمستند ولآبائه (داخل المعاملة)
13  التدقيق: state_transition_log + audit_event (قبل/بعد · لقطة السياسات · إصدارات القواعد · معرّفات القيود والحركات)
14  Outbox: حدث «Posted» للمشتركين (يُنشر بعد الالتزام فقط)
15  COMMIT — أي استثناء في 1…14 ⇒ ROLLBACK كامل، ولا يبقى أثر ولا رقم (PS-04 · AC-61 · CX-04)
```

| الجانب | القرار التقني |
|---|---|
| مستوى العزل | `READ COMMITTED` + أقفال صفوف صريحة (رأس المستند · cost_pool · stock_balance · open_item · numbering_counter). المتوسط المرجح **يُسلسَل لكل (كيان × صنف)** ضماناً للحتمية |
| ترتيب الأقفال | مستند ← أصناف (مرتبة بالمعرّف) ← بنود مفتوحة (مرتبة) ← عدّاد الترقيم (آخر شيء لتقصير زمن القفل) |
| Idempotency | مفتاح طلب لكل انتقال؛ التكرار يعيد النتيجة الأولى ولا يرحّل مرتين |
| الفشل | كائن `PostingFailure{code, details}` مهيكل: سلسلة الحل عند `FAIL-CFG-02`، الأبناء المانعون والمسار البديل عند منع العكس (REV-10 · AC-70)، اقتراحات المخزن البديل/التحويل/أمر الشراء عند `FAIL-COST-01` (AC-09) — كلها **حسابات قراءة** لا آثار |
| المعاملات المركبة | `business_transaction_id` مشترك (CX-06)؛ البيع الفوري يُنشئ SO ثم Delivery ثم Invoice (ثم Receipt إن وُجد قبض) **مروراً بكل حالة وسيطة فعلياً** (CX-02)، وكلها مستندات حقيقية بأرقام (CX-03)، في معاملة واحدة |
| العمليات الدورية (PR-X-010 وعكسها الآلي · انتهاء الحجز إن فُعِّل SD-01) | مهام مجدولة تستدعي **نفس الخط** أعلاه — لا كتابة مباشرة |

---

## 5 — نموذج البيانات المنطقي

> مستوى منطقي (كيانات وسمات مفتاحية وقيود). DDL وهجرات Alembic في مرحلة التنفيذ.
> **Append-only** = لا UPDATE/DELETE لدور التطبيق على مستوى قاعدة البيانات.

### 5.1 `platform.org` — C-01

| الكيان | السمات المفتاحية | ملاحظات/المرجع |
|---|---|---|
| `legal_entity` | code · name · functional_currency · fiscal_calendar | نطاق التقييم (BR-208) |
| `branch` | entity · code | بُعد تحليلي إلزامي (04 §3.1) |
| `site` | branch · code | «موقع» في الهيكل |
| `location` | entity · site? · code · **kind** ∈ {WAREHOUSE, TRANSIT_INTERNAL, TRANSIT_INBOUND, COST_OBJECT, CUSTOMER_SITE, SUBCONTRACTOR, WORK_CENTER*, STAGE*} · is_physical · **ownership** ∈ {ENTITY_OWNED, CUSTOMER_OWNED} | M-01 مواقع منطقية · BR-111/112. (*) قيم محجوزة للموجة 2 بلا سلوك |

### 5.2 `platform.identity` — C-02

| الكيان | السمات المفتاحية | المرجع |
|---|---|---|
| `user` · `role` | — | — |
| `permission_code` | مثل `GR.POST` · `POST.OVERRIDE_ACCOUNT` · `COST.VIEW` | 05 §0.5 · RES-04 |
| `role_grant` | role · permission · **scope**(entity · branch · warehouse · dimension filter · document states) | BR-901 السباعية |
| `field_permission` | role · entity_type · field · allow_view · **sensitivity_class** (COST…) | BR-902 · AC-35 — تُطبَّق في طبقة الإسقاط الموحدة (عرض/طباعة/تصدير/تكامل) |
| `sod_rule` | code · predicate_name (creator≠approver · approver≠reconciler · counter≠approver · supplier_creator≠bill_approver · cashier≠diff_approver) | BR-903 · 05 §9 |
| `delegation` | from · to · scope · valid_from/to · reason | BR-907 |

### 5.3 `platform.party` — C-03 · `platform.item` — C-04

| الكيان | السمات المفتاحية | المرجع |
|---|---|---|
| `party` · `party_role` | role ∈ {CUSTOMER, SUPPLIER, EMPLOYEE, AGENCY} · credit_limit (عميل) · terms | C-03 · POL-SAL-001 |
| `item` | code · **kind** ∈ {RAW, SEMI_FINISHED, FINISHED, SERVICE, RESOURCE} · is_stock · base_uom · **secondary_uom + dual_mode** · lot_tracked · serial_tracked · shelf_life · item_group | M-06 (لا مصدر توريد مغروس) · M-07 · M-12 |
| `uom` · `uom_conversion` | item? · from · to · factor · **version · locked_after_first_movement** | BR-109 |
| `item_group` (شجري) | — | مستوى حل 4 |
| `lot` · `serial` | item · code · expiry / status | INV-08/09 · FEFO |
| `reason_code` | code · family ∈ {ISSUE, ADJUSTMENT, TRANSIT_LOSS, INBOUND_LOSS, SCRAP} · **capitalization_branch** ∈ {WITHIN_STANDARD, ABOVE_STANDARD, N/A} · **generates role** `ACC.EXP.REASON.<code>` | BR-106 · M-11 · 04 §1.6 |
| `reason_category` | التصنيفات الـ12 للإلغاء/العكس + نص حر | 05 §8 |

### 5.4 `platform.dimension` — C-05 · `platform.currency` — C-06 · `platform.tax` — C-07

| الكيان | السمات المفتاحية | المرجع |
|---|---|---|
| `dimension_type` | code ∈ {ENTITY, BRANCH, LOCATION, COST_CENTER, PROJECT, COST_OBJECT, PARTY, SALES_REP, CHANNEL, SHIFT, CASHIER, POS_TERMINAL, PRODUCTION_ORDER*} · **mandatory_matrix** حسب نوع سطر القيد | AR-006 · 04 §3.1 · M-09 |
| `dimension_value` | type · code · valid_from/to | — |
| `dimension_set` | مجموعة مُطبَّعة يُشار إليها من كل سطر قيد وحركة + لقطة JSONB | «الأبعاد لا تُشتق بعد الترحيل» |
| `currency` | code · **minor_unit** | ROU طبقة 1 |
| `exchange_rate_type` · `exchange_rate` | type · from/to · effective_date · rate | POL-FIN-002 · FX-04 |
| `tax_jurisdiction` | code · **params JSONB بلا قيم افتراضية**: `TAX_POINT_ADVANCE` ∈ {ON_RECEIPT, ON_INVOICE} · `TAX_ROUNDING_LEVEL` ∈ {LINE, TOTAL} · `TAX_ON_INVOICE_BEFORE_CONTROL` … | PD-102 · 06 §10.2 · `FAIL-CFG-03` |
| `tax_type` · `tax_rate` · `tax_exemption` · `tax_class` (صنف/طرف) | direction ∈ {INPUT, OUTPUT} · basis · effective_from/to | C-07 |
| `tax_line` | document_line · basis · rate_ref · amount · **tax_point_event** | ساق ضريبية قابلة للتدقيق |

### 5.5 `platform.document` — C-08 · C-22 (إطار المستند)

| الكيان | السمات المفتاحية | المرجع |
|---|---|---|
| `document_type` | code · **category** ∈ {COMMITMENT, EVENT, RANGE} · supports_completed · supports_closed · numbering_scope · sm_version | CC-01 · SF-04 |
| `document` | type · entity · branch · **number (NULL حتى الترحيل) · draft_ref** · **global_state · execution_substate · settlement_substate** · document_date · **accounting_date** · party · currency · fx_rate/type · **subtype** (مستوى حل 6) · **business_transaction_id** · origin_document · **reversal_of** · correction_of (محجوز) · version · created_by | GS-04 · NUM-04 · CX-06 · REV-01 |
| `document_line` | line_no · item/service · **qty_ordered · qty_executed · qty_invoiced** (عدّادات مستقلة تُحدَّث بأحداث الأبناء، لا تُشتق) · uom · secondary_qty · unit_price · discount · line_amount · dimension_set · reason_code · **ownership_transfer_point** ∈ {AT_SHIPMENT, AT_RECEIPT} (يُثبَّت عند أول حدث) · **invoice_basis** ∈ {SERVICE_PERFORMED, GOODS_UNDELIVERED, NON_INVENTORY_OTHER, GOODS_DELIVERED_NO_DOC} · **bill_basis** ∈ {MATCHED_RECEIPT, IN_TRANSIT_OWNED, SERVICE, ADVANCE_REQUEST, MISSING_RECEIPT} · **line_kind** ∈ {ITEM, SERVICE, LANDED_COST(Q-A2-05)} · quality_status ∈ {HOLD, ACCEPTED, REJECTED} · origin_line · **account_override**(account · reason · actor) (مستوى 1) | BR-804 · OWN-01…04 · PR-S-033 · 06 §4.2 · RES-04 |
| `document_link` | parent(doc/line) · child(doc/line) · **link_type** ∈ {CONVERTED_FROM, FULFILLS, INVOICES, RETURNS, APPLIES, ALLOCATES, REVERSES, MILESTONE_OF} | BR-805 · مصفوفة الأب/الابن `07` §8 |
| `business_transaction` | kind ∈ {INSTANT_SALE, KITTING, COST_OBJECT_EVENT} | CX-06 |
| `state_transition_log` | document · from · to · actor · role · reason_category · reason_text · at_utc · at_local · policy_snapshot · rule_versions[] · journal_ids[] · movement_ids[] · session/device/branch | 05 §0.6 · T-04 |
| `numbering_counter` | doc_type × entity × branch × period · last_number | NUM-01 |
| `numbering_gap_log` | scope · missing_number · explanation · txn_ref · actor · at | NUM-05…07 · AC-67 |
| `attachment` | target(type,id) · file meta · hash | C-22 |
| `sm_definition` · `sm_state` · `sm_transition` | doc_type · version · from · to · permission_code · **guard_names[] · effect_names[]** · actor_kind ∈ {USER, SYSTEM} · requires_reason · requires_category | آلات الحالات كبيانات تعكس `05`+`07` واحداً لواحد |

### 5.6 `platform.workflow` — C-09 (PD-104) · `platform.policy` — C-17 · `platform.period` — C-21

| الكيان | السمات المفتاحية | المرجع |
|---|---|---|
| `approval_route` | doc_type · scope · **condition_predicate** · **threshold_policy_ref** · steps[] | PD-104 · SD-02 |
| `approval_step` | route · seq · approver_role · escalation_after · allow_delegation | C-09 |
| `approval_instance` · `approval_action` | document · step · actor · decision · reason · at | تدقيق سلسلة الاعتماد كاملة (05 §1.1) |
| `policy_definition` | code · owner_role · scope_levels[] · value_type · **default_value (NULL = لا افتراضي ⇒ منع)** · **impact_statement** · required_permission · **conflicts_with[]** · reversible | 03 §7.1 · 01 §9.1 |
| `policy_value` | definition · scope · value · effective_from/to · set_by · **reason** · **impact_ack_at** | AC-38 · لا أثر رجعي |
| `policy_snapshot` | at · values hash/JSONB | يُشار إليه من كل ترحيل وتدقيق |
| `fiscal_year` · `fiscal_period` | entity · start/end · **state** ∈ {OPEN, SOFT_CLOSED, HARD_CLOSED} · reopen log | POL-FIN-001 · BR-004 · AC-05 |
| `closing_run` | entity · period · **blockers JSONB · warnings JSONB · acknowledgments** | PR-X-020 · BIL-03 · MEX-02 · AC-41 |

### 5.7 `ledger.gl` — C-10

| الكيان | السمات المفتاحية | Append-only | المرجع |
|---|---|---|---|
| `account` | entity · code · name · type · **is_postable** · parent | لا | OD-01 (يُستورد عند التهيئة) · RES-05 |
| `account_role` | code (44 + عائلة `ACC.EXP.REASON.<code>` المولَّدة) · nature · mandatory_rule · family_pattern | لا (سجل مغلق يُحمَّل من الكتالوج) | 04 §1 · 06 §1 |
| `account_role_mapping` | role · **level 2…9** · scope_type/scope_id · account · effective_from/to · set_by · reason | لا (مؤرَّخ) | 06 §5.2 · RES-02 (لا يمس قيوداً مُرحَّلة) |
| `posting_rule` | **rule_id · version · effective_from/to · status** ∈ {ACTIVE, WITHDRAWN} · event_code · document_type · required_global_state · precondition_names[] · **selection_keys**(reason_code? · subtype? · item? · item_group? · txn_type?) · **line_templates[]**{role · side · amount_source · dimension_source · currency_mode · condition} · inventory_effect_names[] · cost_effect_name · tax_leg_spec · reversible · reversal_blocker_names[] · milestone_kind? · **source_ref** (مثل `04 §PR-P-020` + `06 §3.3`) | لا (مؤرَّخ بالإصدار) | VER-01…03 · AC-57 |
| `event_composition` | transition/event_code → قائمة استدعاءات قواعد بشروط مسمّاة وقيود عدّ (مثل `DEL.POST` ⇒ `PR-S-020` دائماً + **واحدة بالضبط** من {`PR-S-021`,`PR-S-022`,`PR-S-030`}) | لا | RRI-01 · «قيد مصاحب إلزامي» |
| `journal` | entity · accounting_date · document · transition_log · business_transaction · **rule_id · rule_version** · **kind** ∈ {ORIGINAL, REVERSAL, MILESTONE, AUTO_REVERSAL} · reverses_journal · milestone · posted_by · policy_snapshot · total_dr/cr (وظيفية) | **نعم** | BR-007 · REV · PM |
| `journal_line` | journal · line_no · **account_role · account · resolution_level · resolved_scope** · side · amount_txn · currency · fx_rate · fx_rate_type · **amount_functional** · dimension_set · source_document_line · open_item? · is_rounding_line | **نعم** | RES-03 · FX-01 · ROU-05 |
| `gl_balance` | account × period × (أبعاد مختارة) | مشتق | أداء التقارير فقط |

**قيد قاعدة بيانات:** محفّز مؤجَّل (DEFERRABLE INITIALLY DEFERRED) يرفض الالتزام إن كان Σ مدين ≠ Σ دائن بالوظيفية لأي `journal` (ROU-01).

### 5.8 `ledger.inventory` — C-11 · C-13

| الكيان | السمات المفتاحية | Append-only | المرجع |
|---|---|---|---|
| `stock_bucket` (تعداد) | ON_HAND · HOLD · DAMAGED · RETURNED_PENDING · IN_TRANSIT_INTERNAL · IN_TRANSIT_INBOUND · COST_OBJECT_WIP — و**مشتقات غير مخزَّنة**: RESERVED (من الحجوزات) · ON_ORDER (من سطور PO المؤكدة) | — | BR-101 · 04 |
| `inventory_movement` | entity · item · location_from/to · bucket_from/to · lot · serial · qty_base · qty_secondary · unit_cost · value_functional · costing_method · document_line · journal · rule_id/version · business_transaction · **kind** ∈ {RECEIPT, ISSUE, TRANSFER_OUT, TRANSFER_IN, ADJUST_IN, ADJUST_OUT, KIT_IN, KIT_OUT, RETURN_IN, RETURN_OUT, CONSUME_TO_CO, OUTPUT_FROM_CO, SCRAP, QUALITY_RELEASE, OWNERSHIP_ARRIVAL, REVERSAL} | **نعم** | BR-001 (كمية + قيمة + قيد في نفس المعاملة) |
| `stock_balance` | entity · item · location · bucket · lot → qty_base · qty_secondary | مادي مُصان معاملاتياً (الحركات هي المصدر) | AC-07 (حساب واحد لكل القنوات) |
| `cost_pool` | **(entity × item)** · qty · value · avg_unit_cost · method ∈ {WMA, FIFO} · lock | لا (يُقفل صفياً) | **BR-208 · 04 §3.3: لا مخزن في المفتاح** · PD-101 |
| `valuation_layer` | entity · item · **source_kind** ∈ {PURCHASE_RECEIPT, IN_TRANSIT_OWNED, TRANSFER_IN, STOCK_COUNT_SURPLUS, SALES_RETURN, KIT_ASSEMBLY, COST_OBJECT_OUTPUT, PROVISIONAL_NEGATIVE, OPENING_BALANCE(محجوز — GAP-01)} · source_line · **created_at = تاريخ الترحيل** · original_qty · original_unit_cost · original_value · fx_fixed · lot? · **kit_composition JSONB** · estimated_landed_part | **نعم** | M-03 · AC-42 · COS-03 · DIS-01 |
| `layer_adjustment` | layer · delta_value · **kind** ∈ {LANDED_ACTUAL, PPV_CAPITALIZED, REVALUATION, PROVISIONAL_CLOSE} · journal · milestone | **نعم** | **الآلية التقنية** لـ PPV-02/PPV-06/CF-01/PM: «تضيف قيمة إلى الطبقة القائمة» بسجل جديد؛ القيمة الجارية = الأصلية + Σ التعديلات، ولا UPDATE على الطبقة |
| `layer_consumption` | layer (FIFO) أو pool (WMA) · movement · qty · unit_cost_at_consumption · value · direction ∈ {CONSUME, RETURN_TO_SOURCE} | **نعم** | AC-17 · REV-05 · SRC-01 (الإرجاع تناسبياً على الطبقات المستهلَكة) |
| `provisional_cost_commitment` | entity · item · qty_negative · provisional_unit_cost · status · closed_by | لا | PR-I-060/061 — **FIFO فقط** (PD-101) · AC-10 |
| `reservation` | **source_kind** ∈ {SALES_ORDER, COST_OBJECT, TRANSFER, SERVICE_ORDER} · source_line · item · location scope · qty · consumed_qty · **state** ∈ {ACTIVE, PARTIALLY_CONSUMED, FULLY_CONSUMED, RELEASED, EXPIRED, OVERRIDDEN} · expires_at (NULL ما لم تُضبط SD-01) · override log | لا | M-04/05 · 05 §2.3 · AC-40 |

**قيد قاعدة بيانات:** محفّز على `stock_balance` يرفض رصيداً سالباً لأي صنف طريقته WMA (PD-101) — بغض النظر عن أي سياسة.

### 5.9 `ledger.costobject` — C-12 (جاهزية L3، بلا محرك تصنيع)

| الكيان | السمات المفتاحية | المرجع |
|---|---|---|
| `cost_object` | entity · kind · expected_output_item · state · **logical_location** (يُنشأ تلقائياً) · **dimension_value** (يُنشأ تلقائياً) · opened/closed | M-01 · M-09 · PR-C-010 |
| `cost_object_entry` | kind ∈ {MATERIAL, RESOURCE_LABOR, RESOURCE_OH, SCRAP_NORMAL, SCRAP_ABNORMAL, OUTPUT, VARIANCE_CLOSE} · qty · rate · value · journal · movement | PR-C-020…060 |
| `resource_rate` | resource · rate · effective (غير مضبوط في الموجة 1 — OD-08) | PR-C-030 |

### 5.10 `subledger.*` — C-14 · C-15 · C-16

| الكيان | السمات المفتاحية | المرجع |
|---|---|---|
| `open_item` | entity · party · kind ∈ {AR, AP} · document · currency · amount_txn/functional · **fx_rate_fixed** · due_date · remaining · status | C-15 · FX-03 |
| `allocation` | open_item · settlement_document (Receipt/Payment/CN/Advance application) · amount · **fx_diff_functional** · journal · undone_by (سجل جديد لا حذف) | BR-703 · PR-T-010 · AC-32 |
| `treasury_account` | entity · kind ∈ {CASH, BANK} · currency · **custodian_user** · limit policy ref | BR-701 · POL-CSH-001 |
| `payment_instrument` (على القبض/الصرف) | kind ∈ {CASH, CHEQUE, TRANSFER, CARD, WALLET} · cheque_ref | BR-701 |
| `cheque` | direction · number · bank · due · **state** (دورتا الشيك الوارد والصادر) · party · amount | BR-702 · 05 §4.3/4.4 |
| `cash_session` | terminal · cashier · opened_at · float · expected · counted · **diff** · approver | BR-501/502 · PR-T-050 |
| `bank_statement(_line)` · `reconciliation_match` | مطابقة فقط — **لا قيود** | BR-705 · PR-T-040 |
| `advance` | document · party · direction · **commitment_link(s)** (SO/PO line) أو on_account · fx_fixed · remaining · state ∈ {POSTED, PARTIALLY_APPLIED, FULLY_APPLIED, REFUNDED, FORFEITED, REALLOCATED, REVERSED} · **origin** ∈ {ADVANCE_DOC, RECEIPT_UNALLOCATED} | BR-601…608 · PR-A-* · PR-T-010 (غير المخصص ⇒ رصيد على الحساب) |
| `advance_application` | advance · invoice/bill · amount · fx_diff · journal (Milestone) | PR-S-031 · PR-A-020 |
| `advance_disposition` | advance · decision ∈ {REFUND, FORFEIT, REALLOCATE} · reason · actor | BR-606 · PC-02 · AC-28 |

### 5.11 `platform.audit` — C-19 · `platform.events` — C-18 · `semantic` — C-20 · `integration/setup` — C-23/C-24

| الكيان | السمات المفتاحية | المرجع |
|---|---|---|
| `audit_event` | at_utc · at_local · actor · role_used · session/device/branch · target(type,id) · action · **field_changes JSONB (قبل/بعد)** · reason · policy_snapshot · related_ids · prev_hash · hash (سلسلة تجزئة — إضافة تقنية لكشف العبث) | BR-904 · **INSERT-only** |
| `outbox_event` · `subscription` · `delivery_log` | يُكتب في نفس المعاملة، يُنشر بعد الالتزام | C-18 · لا أثر مالي عبر الأحداث |
| `metric_definition` | code · تعريف بدلالة **أدوار الحسابات** (مثل `REVENUE_RECOGNIZED` = رصيد `ACC.REV.SALES`؛ `DEFERRED_REVENUE` = `ACC.REV.DEFERRED`) · drill_path | RRI-05 · PS-03 · AC-36/62 — الكتالوج الكامل للمقاييس يحتاج مدخلاً وظيفياً (Q-A2-11) |
| `api_key` · `webhook_endpoint` · `import_job` | — | C-23 |
| `setup_checklist` | entity · step · status — تشمل `ROLE_MAPPING_READY` (FAIL-CFG-01) و**`OPENING_BALANCES: BLOCKED_GAP_01`** | C-24 · PD-106 |

---

## 6 — المحركات

### 6.1 سجل أدوار الحسابات (Account Role Registry)
- **مصدر:** 44 دوراً ثابتاً (`04` §1 + `06` §1) + عائلة `ACC.EXP.REASON.<code>` تُولَّد تلقائياً عند إنشاء رمز سبب.
- **لا دليل حسابات ثابت.** الدليل يُستورد عند التهيئة (OD-01)، والربط يتم بالأدوار.
- **فحص الجاهزية (FAIL-CFG-01):** قبل تفعيل أي عملية، تقرير يعرض الأدوار الإلزامية لعملياتها غير المربوطة على أي مستوى؛ التشغيل ممنوع حتى الإكمال.
- **RES-05:** ربط دور بحساب `is_postable = false` يُرفض عند الحفظ.

### 6.2 محرك حل الحساب (Account Resolution Engine)
- **المدخل:** (دور، سياق السطر: reason_code · item · item_group · location · document_subtype · transaction_type · branch · entity · تجاوز السطر إن وُجد).
- **الخوارزمية:** المرور 1→9 بالترتيب الملزم في `06` §5.2، والتوقف عند أول تطابق. المستوى 1 ليس ربطاً بل تجاوزاً على سطر المستند يتطلب `POST.OVERRIDE_ACCOUNT` + سبب + تسجيل (RES-04)، وغير متاح لأي دور تشغيلي.
- **المخرج:** (حساب، مستوى، نطاق) تُثبَّت في سطر القيد (RES-02/03). تغيير الربط لاحقاً لا يمس أي قيد.
- **الفشل:** إخفاق المستوى 9 ⇒ `FAIL-CFG-02` مع **سلسلة البحث كاملة** في كائن الفشل. **لا يوجد فرع بديل في الكود** (F-11 · RES-06 · AC-51).

### 6.3 محرك قواعد الترحيل (Posting Rule Engine)
- **القواعد بيانات لا كود:** 63 سجلاً بإصدار وتاريخ سريان، تُحمَّل من ملف كتالوج مُصدَّر داخل المستودع يعكس `04`+`06` واحداً لواحد مع `source_ref`. **اختبار مطابقة** يتحقق أن مجموعة المعرِّفات المحمَّلة = مجموعة معرِّفات الوثائق.
- **فصل صارم بين آليتين (F-12):**
  - *اختيار القاعدة* (RSP-01…03): الشروط الإلزامية أولاً، ثم التخصيص بالمميّزات الستة (`06` §5.3)، الأخص يفوز، التساوي ⇒ خطأ تهيئة يوقف.
  - *حل الحساب* (§6.2) داخل القاعدة المختارة.
- **مصادر المبالغ مغلقة ومسمّاة** (لا لغة تعبيرات حرة): `PO_PRICE_X_QTY` · `RECEIPT_FIXED_VALUE` · `LAYER_CONSUMPTION_COST` · `SO_LINE_NET_PRORATA` · `INVOICE_NET/TAX/GROSS` · `ADVANCE_APPLY_MIN` · `DEFERRED_PRORATA` · `PPV_CAPITALIZED_PART/CONSUMED_PART` · `KIT_COMPONENTS_SUM` · `DISASSEMBLY_ALLOCATION` · `COS_RESOLVED_COST` · `SRC_RESOLVED_COST` · `RESOURCE_QTY_X_RATE` · `FX_DIFF` … كل مصدر دالة مُختبَرة وحدياً. إضافة مصدر جديد = تغيير كود مُراجَع، لا تهيئة.
- **قوالب السطور:** دور + جهة + مصدر مبلغ + مصدر أبعاد (سطر/رأس) + شرط مسمّى. قاعدة حالتها المطلوبة `Confirmed` قوالبها **فارغة** بنائياً (AC-57).
- **تركيب الحدث (Event Composition):** لكل انتقال منتِج للأثر قائمة استدعاءات بشروط وقيود عدّ — تنفيذ RRI-01 و«القيد المصاحب الإلزامي» (PR-S-030 ⇐ عكس PR-S-021) و(PR-P-030 ⇐ PR-P-031/032) بشكل معلن وقابل للاختبار.
- **الإصدار:** VER-01…04. تعديل قاعدة = إصدار جديد بتاريخ سريان؛ الاختيار يأخذ الإصدار الساري بتاريخ **الترحيل المحاسبي**.

### 6.4 نواة التقريب والعملة (Rounding & FX Kernel)
- FX-01…06: كل سطر يحمل مبلغ المعاملة والعملة والسعر ونوعه والمبلغ الوظيفي؛ السعر يُلتقط عند الترحيل ما لم يكن مثبتاً من أصل (FX-02/03)؛ لا إعادة تقييم للمخزون بعد الرسملة (FX-05/BR-209).
- ROU طبقة 1: حساب بدقة كاملة ثم تقريب **المبلغ الممتد للسطر** لدقة عملة المستند.
- ROU-04: تحويل **إجمالي المستند** ثم توزيعه على الأسطر بـ**أكبر باقٍ** بحيث Σ الأسطر = الإجمالي المحوَّل بالضبط.
- ROU-05: فرق متبقٍ ≤ (وحدة صغرى × عدد الأسطر) ⇒ سطر موازنة واحد إلى `ACC.MISC.ROUNDING`؛ أكبر ⇒ `FAIL-BAL-01`.
- ROU-03: توزيع قيمة على كمية (أعباء · تفكيك · PPV) يُسند الباقي إلى **أكبر سطر قيمةً**.
- ROU طبقة 2 (الضريبة) وطبقة 3 (تقريب المستند) **معطّلتان** حتى قرار الولاية/PD (OD-02 · OD-12) — الآلية موجودة، والمعامل بلا افتراض.

### 6.5 محرك آلات الحالات (State Machine Engine)
- **الحالة = ثلاثية** `(Global, Execution, Settlement)` (GS-04). العام ينتقل بفاعل وصلاحية؛ الفرعيان **يُشتقّان** بدالة `derive_substates(document)` تُستدعى داخل معاملة كل ترحيل مؤثر على المستند أو أبنائه (GS-01). لا واجهة لتعيينهما، ومحفّز قاعدة بيانات يرفض تعديلهما من خارج الدالة.
- **التعريفات بيانات:** `sm_definition` لكل نوع مستند بإصدار، تعكس `05` بعد تصحيح `07` (الحالات الفرعية القديمة مثل `Partially Delivered`/`Matched`/`Settled`/`Allocated` تُنمذَج **فرعية** — CC-02).
- **الحراس (guards) مسمّاة وقابلة للاختبار:** `has_permission` · `sod_ok` · `period_open` · `qty_within_remaining` · `not_creator` · `no_posted_children` · `advance_none_pending` · `original_layer_traceable` · `all_components_available` · `valuation_source_documented` …
- **التمييز الحاكم:** مستندات الالتزام (PR · RFQ · PO · Quote · SO) **لا تحتوي حالة `Posted` في تعريفها أصلاً** — ضمان بنائي لا شرطي (05 §0.3 · §5.3/21).
- **Completed مقابل Closed** (SF-03/04): `Completed` انتقال آلي عند `Fully Executed + Fully Settled` لمستندات الالتزام والمدى فقط؛ `Closed` بفاعل + سبب إلزامي + تحرير التزامات (On Order/Reserved) دون مساس بأي ابن مالي (CC-05).
- **الترقيم:** يُسحب عند أول ترحيل (NUM-04)؛ المسودات ترقيم مؤقت؛ `Discarded` لا يستهلك رقماً؛ الملغى/المعكوس يحتفظ برقمه.

### 6.6 محرك العكس والمعالم (Reversal & Posting Milestone)
- **العكس** مستند حقيقي من نوع `REVERSAL` يشير للأصل (REV-01)؛ يقرأ `rule_version` من سطور قيد الأصل ويولّد قيداً معاكساً به (REV-02)؛ يعيد الكميات بقيم الأصل عبر `layer_consumption(RETURN_TO_SOURCE)` (REV-05)؛ كامل لا جزئي — **واجهة العكس تقبل معرّف المستند فقط، لا سطوراً ولا مبالغ** (REV-03)؛ الأصل ⇒ `Reversed` نهائية (REV-04).
- **ترتيب leaf-first** (REV-06/PC-04): يُبنى رسم الأبناء من `document_link` + `posting_milestone`؛ أي ابن مُرحَّل غير معكوس ⇒ منع مع **سلسلة الأبناء المانعة والمسار البديل** (REV-08/10 · AC-65/70)؛ ابن غير قابل للعكس ⇒ الأصل لا يُعكس أبداً (REV-09)؛ المانع المطلق (استهلاك مادي) ⇒ لا مسار عكس (PC-03).
- **الفترة المقفلة:** العكس في الفترة المفتوحة التالية بتاريخ محاسبي مختلف، وكلاهما مسجَّل (REV-07 · AC-05).
- **Posting Milestone** (PM-01…04): سجل `posting_milestone` + قيد من نوع `MILESTONE` بإصدار القاعدة **الحالي** وقت المعلَم؛ لا يمس الأصل ولا حالته العامة؛ قابل للعكس مستقلاً؛ عكس الأصل يستلزم عكس معالمه أولاً. الأنواع: `LANDED_ACTUAL` (PR-P-051) · `PROVISIONAL_CLOSE` (PR-I-061) · `PPV` (PR-P-031/032) · `ADVANCE_APPLY` (PR-S-031/PR-A-020) · `CHEQUE_CLEAR/BOUNCE` (PR-T-012/013) · `ALLOCATION`.
- **شجرة SF-07** تُقدَّم في كائن الفشل كمسار بديل (Cancel · Reversal · CN/DN · Milestone · Correction). **Correction Document بلا قاعدة ولا آلة حالات في السلطة ⇒ خانة محجوزة لا تُبنى** (Q-A2-03).

### 6.7 دفتر المخزون والتكلفة (Inventory Ledger & Costing)
- **الحركة = كمية + قيمة + قيد في معاملة واحدة** (BR-001). لا حركة بلا قيمة إلا لموقع `CUSTOMER_OWNED` (BR-112 — لا مستند يستخدمه في الموجة 1).
- **حالات المخزون** كدلاء مخزَّنة + مشتقات: `Available = On Hand − Reserved − Hold − Damaged` و`ATP = Available + On Order المؤكد ضمن الأفق` **بدالة واحدة** تستخدمها كل القنوات (BR-101 · AC-07).
- **طريقة التقييم لكل (كيان × صنف)** من POL-VAL-001: 
  - **WMA (الافتراضي):** `cost_pool` واحد لكل (كيان × صنف) — **لا مخزن في المفتاح** (BR-208 · §3.3/13). الاستهلاك بمتوسط اللحظة تحت قفل الصف. الاستلامات تُسجَّل كطبقات مصدر (للتتبع وسلاسل COS/SRC) لكن الطبقات **تندمج** قيمياً في المجمّع (DIS §8.1).
  - **FIFO (اختياري):** استهلاك طبقات بترتيب الإنشاء؛ الطبقات تحتفظ باستقلالها.
  - **LIFO غير موجود في الكود.**
- **الرصيد السالب:** WMA ⇒ ممنوع بنيوياً (PD-101) ⇒ `FAIL-COST-01` مع اقتراحات (AC-09). FIFO + POL-INV-001 مفعّلة + صلاحية ⇒ PR-I-060 بتكلفة مؤقتة = آخر تكلفة معروفة، والتزام مفتوح يُغلق بـ PR-I-061 كمعلَم؛ لا تكلفة سابقة ⇒ منع. لا ترحيل بتكلفة صفر في أي مسار (FAIL-COST-01…04).
- **سلاسل مصدر التكلفة** كمُحلِّل واحد بمخرجات مطبوعة ومستوى مسجَّل في التدقيق:
  - **COS** (زيادة الجرد، 5 مستويات، آخرها `FAIL-COST-02`) · **SRC** (مرتجع البيع، 4 مستويات، المستوى 3 يحتاج اعتماد مراقب مالي + تقرير استثناءات، آخرها `FAIL-COST-04`) · **DIS-02** (التفكيك غير المتتبَّع، `ref` بنفس COS، `FAIL-COST-03`).
  - **لا حقل تكلفة قابل للإدخال** في مخططات: زيادة الجرد · مرتجع المبيعات · التفكيك (AC-53/55 · SRC-03 · COS-01).
- **Kitting:** قيمة المركب = Σ تكلفة المكونات المستهلَكة بالضبط (لا مدخل «تكلفة مستهدفة» أصلاً)؛ تركيبة التكلفة تُحفظ على الطبقة (DIS-01)؛ التفكيك بمسارين (أ) متتبَّع (ب) توزيع DIS-02، وΣ الموزَّع = قيمة طبقة المركب بالضبط والباقي إلى أكبر سطر (DIS-03/04) ⇒ صفر أثر على الدخل (AC-54).
- **PPV** (F-13/14): السياسة تقرر الحد والإجازة؛ الوجهة تُحسب من `Qr/Qt` وقت الترحيل (PPV-01) — رسملة بسجل `layer_adjustment` على الطبقة القائمة (PPV-02) · خارج التسامح لا يُرسمل (PPV-04) · سالب ⇒ `ACC.COGS.ADJ` + وسم (PPV-05) · قيد تسوية جديد دائماً (PPV-06).
- **الأعباء:** تقديرية عند الاستلام تُضاف لقيمة الطبقة (PR-P-050)؛ الفعلية معلَم PR-P-051 بتوزيع رجعي: المتبقي ⇒ `layer_adjustment(LANDED_ACTUAL)` والمباع ⇒ `ACC.COGS.ADJ` في الفترة المفتوحة، مع تقرير توزيع (AC-14).
- **إعادة التقييم:** سبب + مصدر تقييم + معتمِد؛ قيمة فقط بلا كمية (`layer_adjustment(REVALUATION)`).
- **إعادة التقييم الرجعية** آلية واحدة تخدم الأعباء وفروق الإنتاج (M-10).
- **ثابت التسوية (AC-02):** Σ قيمة دلاء المخزون في الدفتر = Σ أرصدة أدوار `ACC.INV.*` المقابلة؛ يُختبر بعد كل سيناريو ويُعرض كتقرير.

### 6.8 الحجز والتوفر (Reservation & ATP)
- سجل مرتبط بمصدر متعدد (SO · Cost Object · Transfer · Service Order) (M-04)؛ بلا أثر مالي؛ `Overridden` بصلاحية عليا وسبب وتدقيق حساس؛ `Expired` معرَّفة والمهلة **غير مضبوطة** حتى SD-01 (لا انتهاء آلي ما دامت السياسة فارغة).
- أولوية التنافس (SF-02) مؤجَّلة للموجة 2 — لا خوارزمية أولوية في الموجة 1 سوى التسلسل الطبيعي للحجز.

### 6.9 محرك الضرائب (Tax Engine — PD-102)
- **بنية قابلة لاستقبال السياسة:** ولاية + أنواع + معدلات مؤرَّخة + إعفاءات + تصنيفات صنف/طرف + **معاملات نقطة الاستحقاق** لكل حدث.
- **لا افتراضات:** كل معامل ولاية `NULL` حتى تُضبط بصلاحية مالية عليا وبلا أثر رجعي. أي قاعدة تحمل ساقاً ضريبية (PR-S-030/031/032/040/041/042 · PR-P-030/034/035/051/070 · PR-A-010/011/012) تفشل بـ `FAIL-CFG-03` إن كان المعامل المطلوب غير مضبوط.
- **الواجهة:** `compute_tax(lines, jurisdiction, event) → tax_lines` — قابلة لاستبدال محتواها بالسياسة القانونية لاحقاً دون مساس بمحرك الترحيل.
- **الاختبارات الآلية** تستخدم ولاية موسومة `TEST` بمعاملات صريحة — ليست افتراضاً ولا تُشحن مع النظام (تأكيد مطلوب — §11).

### 6.10 محرك الاعتماد (Approval Engine — PD-104)
- مسارات كبيانات: نوع مستند + شرط مسمّى (مثل `amount_exceeds(threshold_policy)` · `discount_exceeds` · `credit_exceeded` · `variance_out_of_tolerance`) + خطوات بأدوار + تصعيد + تفويض (BR-907).
- **العتبات تُقرأ من كائنات السياسة** (POL-PUR-002 · POL-CSH-001 · POL-INV-004 · POL-SAL-002 …) — لا رقم في الكود.
- **مسار يشير إلى عتبة غير مضبوطة (SD-02):** المقترح التقني = منع الإرسال بـ `FAIL-CFG-04` (تأكيد مطلوب — Q-A2-06). البديل (تجاوز الاعتماد) قرار وظيفي ليس لي.
- SoD يُقيَّم كحارس في كل انتقال اعتماد/ترحيل (BR-903 · AC-37)، والمحاولة المخالفة تُسجَّل (`FAIL-SOD-01`).

### 6.11 محرك السياسات (Policy Engine — C-17)
- 22 تعريفاً بكامل مواصفة `03` §7.1؛ قيم مؤرَّخة بنطاقات؛ **بيان الأثر يُعرض ويُقرّ قبل التفعيل**؛ سجل تغيير بسبب إلزامي؛ لا أثر رجعي (لقطة السياسات تُثبَّت في كل ترحيل — AC-38).
- **قواعد التعارض المشفَّرة كبيانات:** `POL-INV-001 = مسموح` ∧ الصنف WMA ⇒ رفض (PD-101).
- **ما ليس سياسة (§7.2)** غير قابل للتمثيل: لا تعريف سياسة لتعطيل التكلفة أو تعديل المُرحَّل أو تغيير قاعدة ترحيل — الكتالوج مغلق (T-7).

### 6.12 التدقيق وفصل المهام وأمن الحقول
- `audit_event` بمستوى الحقل، INSERT-only، سلسلة تجزئة اختيارية.
- كل انتقال يسجّل بنود `05` §0.6 كاملة.
- **صلاحية الحقل** تُنفَّذ في **مكوّن إسقاط واحد** يمر عبره العرض والطباعة والتصدير والتكامل (BR-902 · AC-35) — لا تُنفَّذ في الشاشات.

### 6.13 الترقيم (NUM-01…07)
- عدّاد جدولي لكل (نوع × كيان × فرع × فترة) يُقفل ويُزاد داخل معاملة الترحيل ⇒ الفشل يُرجعه (فجوات نادرة جداً).
- تقرير الفجوات (NUM-06) + سجل التفسير؛ فجوة بلا تفسير = استثناء تدقيق (NUM-07 · AC-67).
- مقايضة معلنة: قفل صفّي قصير لكل نطاق ترقيم مقابل شبه انعدام الفجوات. قابل للاستبدال بتسلسل غير معاملاتي + سجل فجوات دون تغيير مخطط.

### 6.14 الفترات وبوابة الإقفال
- حالات الفترة: Open / Soft / Hard (POL-FIN-001)؛ الترحيل على مقفلة ⇒ `FAIL-PER-01` مع **خيار** الفترة المفتوحة التالية بتاريخ محاسبي مختلف — المستخدم يختار، والنظام يسجّل التاريخين (AC-05).
- **بوابة الإقفال (PR-X-020):** يمنع: فروق جرد بانتظار اعتماد · مستندات معلقة في الاعتماد. يحذّر: GRNI معمَّر · DNI · تكاليف مؤقتة · دفعات معمَّرة · كائنات تكلفة مفتوحة (AC-41). **فواتير غير مُرحَّلة/`Match Exception` بند إلزامي يتطلب إقراراً موثقاً** (BIL-03 · MEX-02).
- PR-X-010: إعادة تقييم الأرصدة المفتوحة (لا المخزون) وعكسها الآلي في أول يوم من الفترة التالية عبر نفس خط الترحيل.

### 6.15 البنود المفتوحة والدفعات المقدمة
- الفوترة/الفواتير/الدفعات تُنشئ بنوداً مفتوحة بسعر مثبت؛ التخصيص محدد أو آلي (FIFO) مع تجاوز مسجَّل؛ غير المخصص ⇒ رصيد على الحساب في تقرير مستقل (BR-703 · AC-32)؛ فرق العملة عند التخصيص محقق بسعر الأصل (FX-03 · AC-29).
- **الدفعة المقدمة** كائن أولى الدرجة بدورة `05` §3.1 وقيود BR-601…608: لا إيراد أبداً؛ مربوطة بالتزام؛ تُسوّى آلياً عند الفوترة (معلَم PR-S-031 بأقل القيمتين وبسعر الاستلام المثبت)؛ **إلغاء الالتزام لا يمسها** (PC-02 · AC-66)؛ الزائد رصيد على الحساب (PR-A-030)؛ المرآة للموردين (PR-A-020).
- ارتداد الشيك يعيد فتح البند الأصلي (سجل `allocation` عكسي) ولا يُنشئ ديناً جديداً، والرسوم قيد منفصل (BR-702 · AC-31).

### 6.16 كائن التكلفة (C-12 — جاهزية L3)
- دورة `05` §6.1 وقواعد PR-C-010…060 كأحداث Core بلا واجهة تصنيع ولا BOM/Routing/جدولة.
- الموقع المنطقي والبُعد يُنشآن مع الكائن؛ الاستهلاك لا يغادر أصول الكيان (BR-111)؛ الهالك يتفرع بالمعياري (M-11 · POL-MFG-001)؛ المخرج طبقة مصدرها `COST_OBJECT_OUTPUT` (M-03 · AC-42)؛ الإغلاق بفرق إلى `ACC.CTRL.COSTOBJ_VAR`؛ الإقفال لا يفشل ولا يجبر الإغلاق (AC-41).
- **اختبار الجاهزية 6.1 / AC-39** مُنفَّذ كاختبار آلي بأحداث Core وحدها — شرط إغلاق الموجة 1.

### 6.17 الأحداث (Outbox) · 6.18 الطبقة الدلالية (الحد الأدنى)
- Outbox معاملاتي؛ المشتركون داخليون وWebhooks؛ **لا أثر مالي أو كمّي عبر الأحداث**.
- سجل مقاييس بدلالة الأدوار + عقد Drill-down (≤3 خطوات: سطر تقرير ← قيد ← مستند/حدث ← فاعل/سياسة).

---

## 7 — الحدود

### 7.1 داخل خطة البناء (الموجة 1)
Core بقدراته الـ24 (بالحد الأدنى المعلن لـ C-20/C-23) · Inventory & Costing · Procurement · Sales (بالدفعات المقدمة والإيراد المؤجَّل) · Treasury · كائن التكلفة كجاهزية · مستندات الكتالوج الـ26 · القواعد الـ62 النافذة · واجهة HTTP رقيقة للتكامل والاختبار.

### 7.2 خارج خطة البناء — وكيف يُحفظ لها مكان بلا بناء
| البند | السبب | ما يُحجز في التصميم |
|---|---|---|
| Manufacturing (BOM · Routing · مراكز العمل · جدولة) | الموجة 2 · §5.4/30 | قيم تعداد محجوزة (`WORK_CENTER`, `STAGE`, `PRODUCTION_ORDER`) بلا سلوك |
| POS كمحرك (ورديات كقناة · بلا اتصال) | الموجة 1.5 · SD-05 | مستند `Cash Session` يُبنى في Core كما في الكتالوج؛ سلوك القناة لاحقاً |
| Consignment-In | PD-103 | لا شيء |
| Opening Balance Document | **GAP-01** | نوع مستند + مصدر طبقة محجوزان بالاسم؛ خطوة تهيئة محجوبة |
| Fixed Assets (Wave 1 مخفف في `03` §2.2) | **لا قاعدة ترحيل ولا آلة حالات في `04`–`07`** | **Q-A2-02** — لا يُبنى بلا ملحق |
| Correction Document · إشعار مورد دائن/مدين | مذكوران في شجرة SF-07 بلا قاعدة | **Q-A2-03/04** — خانة محجوزة |
| Intercompany · Projects · Service · CRM · HR · Trade Finance | مؤجَّلة (`03` §10) | لا شيء |
| الشاشات | خارج النطاق · §3.2/ممنوع البدء بها | لا شيء في هذه الخطة |

### 7.3 ما لا يعبر حدود Core أبداً
أسماء مراحل صناعة · نسب دفعة مقدمة إلزامية (الآلية Core والإلزام حزمة) · قياس معاينة · أي منطق محاسبي في Domain أو Industry.

---

## 8 — ضمانات الممنوعات الـ34 (`08` §5) — الآلية التقنية لكل منع

| # | المنع | الآلية |
|---|---|---|
| 1 | Tax Point/Rate | معاملات ولاية NULL بلا افتراض · `FAIL-CFG-03` · اختبارات بولاية `TEST` صريحة |
| 2 | `Posted` = إيراد | المقاييس من الأدوار لا الحالات · عرض الفاتورة يُلزم إظهار بُعد التنفيذ (INV-S3) · AC-62 |
| 3 | `REV.SALES` بلا دليل سيطرة | شرط PR-S-030 على مستوى السطر (تسليم مُرحَّل مرتبط / `SERVICE_PERFORMED` / بيع فوري ذرّي) · RRI-02 اختبار |
| 4 | خلط ADVANCE/DEFERRED | قوالب القواعد ثابتة · فحص بنائي يمنع أي قاعدة دفعة من الإشارة إلى `REV.DEFERRED` والعكس (`FAIL-REV-02`) |
| 5 | حساب متنوعة/معلّق | لا فرع بديل في محرك الحل · سجل أدوار مغلق · AC-51 |
| 6 | Manual Posting | لا مسار إدراج في `journal` إلا دالة الترحيل (SECURITY DEFINER)؛ دور التطبيق بلا INSERT مباشر |
| 7 | تعديل `Posted` | محفّز يرفض UPDATE/DELETE على المستندات بعد `Posted` (عدا الأعمدة المشتقة عبر دالتها) · جداول القيود/الحركات INSERT-only |
| 8 | كسر مدين=دائن | قيد مؤجَّل على مستوى القيد + ROU-05 |
| 9 | سالب WMA / تحويل لـFIFO | محفّز رصيد + تعارض سياسة + لا كود تحويل |
| 10 | إدخال تكلفة يدوياً | لا حقل تكلفة في مخططات المستندات الثلاثة · المحلِّل هو المصدر الوحيد |
| 11 | ترحيل بتكلفة صفر | قيد `CHECK (value > 0 عند qty > 0)` على الطبقات المملوكة · `FAIL-COST-*` |
| 12 | رسملة PPV كاملة على جزئي | PPV-01 دالة واحدة · AC-52 |
| 13 | متوسط على مستوى المخزن | مفتاح `cost_pool` = (كيان × صنف) |
| 14 | أثر للتفكيك على الدخل | DIS-03 تحقق Σ قبل الكتابة · AC-54 |
| 15 | فاتورة مورد تحرك كمية | قواعد الفواتير بلا `inventory_effects` — اختبار بنائي AC-50 |
| 16 | GRNI مرتين | قيد تفرّد على سجل الملكية العابرة المفتوح لكل سطر + شرط PR-P-020 · `FAIL-OWN-01` |
| 17 | إعادة التقييم لإصلاح الأخطاء | مستند يتطلب مصدر تقييم + صلاحية عليا + تقرير مراجعة دوري (ضابط إجرائي — لا يمكن إثباته آلياً بالكامل، ويُعلن ذلك) |
| 18 | Kitting بفرق | القيمة تُحسب حصراً Σ المكونات — لا مدخل لتكلفة مركب |
| 19–20 | الحالة الفرعية تُنتج/تُعيَّن | دالة اشتقاق للقراءة فقط · لا API · محفّز |
| 21 | مستند التزام يصل `Posted` | الحالة غير موجودة في تعريف آلته · AC-57 |
| 22 | الأب يُسقط التزام ابن | حراس PC-01…05 على Cancel/Close/Reverse عبر `document_link` |
| 23 | إغلاق الدفعة آلياً | آثار `SO.CANCEL` لا تتضمن الدفعة · AC-66 |
| 24 | عكس جزئي | واجهة العكس تقبل معرّف المستند فقط |
| 25 | إصدار حالي عند العكس | يُقرأ من سطور الأصل |
| 26 | مستندات خفية | كل مستند مركّب له رقم وحالة وتدقيق · AC-68 |
| 27 | تحريك جرد قبل Approved+Posted | الحركات فقط في أثر `ADJ.POST` المشروط بـ `Approved` |
| 28 | أرصدة افتتاحية وهمية | خطوة التهيئة محجوبة · لا استيراد يكتب في الطبقات/القيود خارج المحرك |
| 29–30 | منطق نشاط/تصنيع في Core | قاعدة اعتماديات في CI + اختبار الحذف |
| 31 | مفاتيح عامة | كتالوج سياسات مغلق · قوالب القواعد غير قابلة للتعديل وقت التشغيل |
| 32–33 | إعادة تعريف/اختراع | كل قاعدة وحالة تحمل `source_ref` · اختبار مطابقة الكتالوج · الفجوات مرفوعة (§12) |
| 34 | افتراض كود سابق | Greenfield |

---

## 9 — ترتيب البناء ومراحله

### 9.1 مبرر الترتيب
1. **النزاهة قبل الوظيفة:** الجمود والذرية والتوازن والحل تُبنى وتُختبر قبل أي مستند تجاري — لأنها الشروط التي تحكم كل ما بعدها.
2. **الأستاذ قبل المخزون قبل المستندات التجارية:** محرك الترحيل يحتاجه كل مستند؛ ودفتر المخزون تحتاجه المشتريات والمبيعات؛ والمشتريات قبل المبيعات لأن طبقات التكلفة تأتي من الشراء.
3. **الاعتراف بالإيراد بعد استقرار التسليم والتكلفة:** RRI-01 يربط التسليم بقاعدة إيراد ذرياً.
4. **الخزينة والدفعات بعد الذمم:** التخصيص يحتاج بنوداً مفتوحة من الفواتير.
5. **كائن التكلفة أخيراً كاختبار جاهزية** لا كميزة.
6. **لا واجهات** في هذه الخطة (§3.2/3). الواجهة البرمجية الرقيقة تُضاف من المرحلة 5 لخدمة اختبارات التكامل.

### 9.2 المراحل

| المرحلة | المحتوى | مخرج/بوابة الخروج | معايير القبول الأساسية |
|---|---|---|---|
| **P0 — نواة المستودع والنزاهة** | هيكل المشروع · Postgres + Alembic · نواة Decimal/التقريب (ROU-01/04/05) · محمِّلات الكتالوج (أدوار · قواعد · آلات حالات) + **اختبار المطابقة** · صلاحيات INSERT-only ومحفزات الجمود · نواة التدقيق · CI مع قاعدة الاعتماديات | الكتالوج محمَّل 44/63/27 بلا انحراف · الجمود مُثبت على مستوى DB | AC-56 · AC-57 |
| **P1 — البيانات الأساسية للمنصة** | org (مواقع فيزيائية ومنطقية) · identity (السباعية · SoD · تفويض · صلاحية الحقل بمكوّن الإسقاط) · party · item/UoM/كمية مزدوجة/دفعات/تسلسلي/رموز أسباب · dimensions · currency/FX · policy engine (22) · periods · numbering | مستند اختباري يمر بحراس الصلاحية/SoD/الفترة | AC-35 · AC-37 · AC-38 · AC-67 |
| **P2 — نواة الأستاذ** | حسابات · سجل الأدوار · محرك الحل (9) · `journal` · محرك القواعد (اختيار · تركيب · قوالب · مصادر مبالغ · FX) · حالات الفشل · نواة العكس والمعلَم · هيكل Tax Engine (`FAIL-CFG-03`) | ترحيل قيد آلي من قاعدة اختبارية بكل الضمانات · فشل مهيكل بسلسلة الحل | AC-04 · AC-05 · AC-51 · AC-58 |
| **P3 — إطار المستند ومحرك الحالات** | الثلاثية · الانتقالات كبيانات · الحراس · المعاملات المركبة · سلسلة الأصل · التتبع الثلاثي · الأب/الابن · تنسيق العكس leaf-first · Approval Engine · Outbox | **أول مستند حقيقي من طرف لطرف: Treasury Transfer (PR-T-030)** Draft→Posted→Reversed · حقن فشل في كل خطوة ⇒ صفر أثر | AC-01 · AC-03 · AC-06 · AC-34 · AC-59 · AC-60 · AC-61 · AC-63 · AC-64 · AC-65 · AC-68 · AC-69 · AC-70 |
| **P4 — دفتر المخزون والتكلفة** | الحركات والدلاء · المجمّعات والطبقات · WMA (كيان×صنف) وFIFO · الاستهلاك · سلاسل COS/DIS · إعادة التقييم · موانع السالب · الحجز وATP · **مستندات:** Transfer · Adjustment · Issue · Kitting · Revaluation + سجل Reservation · **قواعد:** PR-I-010/011/012/020/021/030/040/041/050 · PR-S-010 | ثابت AC-02 يعمل بعد كل سيناريو | AC-02 · AC-07 · AC-09 · AC-11 · AC-12 · AC-13 · AC-17 · AC-53 · AC-54 |
| **P5 — المشتريات** | PR · RFQ · PO · GR (بما فيه `Awaiting Ownership` وجودة `Hold`) · Supplier Bill (الأسس الخمسة + الأعباء) · Purchase Return · GRNI · PPV · الأعباء تقديرية/فعلية (معلَم) · **قواعد:** PR-P-010/020/021/022/023/030/031/032/034/035/050/051/060/070 + `PR-P-033` محمَّلة كمسحوبة · API رقيقة تبدأ هنا | سيناريوهات `07` §10 رقم 1·3·4·16 | AC-14 · AC-15 · AC-18 · AC-19 · AC-20 · AC-21 · AC-47 · AC-48 · AC-49 · AC-50 · AC-52 |
| **P6 — المبيعات والاعتراف بالإيراد** | Quote · SO · Delivery (RRI-01) · Sales Invoice (مصفوفة 2×2 · PR-S-030/032/022/033) · Sales Return (SRC) · CN/DN · صرف مجاني · البيع الفوري المركّب · **قواعد:** PR-S-020/021/022/030/032/033/040/041/042/050 | السيناريوهات الخمسة في `06` §2.6 · سيناريوهات `07` §10 رقم 5·6·8·9·10·11 | AC-08 · AC-22 · AC-23 · AC-24 · AC-25 · AC-43 · AC-44 · AC-45 · AC-46 · AC-55 · AC-62 |
| **P7 — الخزينة والذمم والدفعات المقدمة** | بنود مفتوحة · Receipt/Payment/تخصيص · شيكات وارد/صادر · Cash Session · Customer/Supplier Advance (BR-601…608) · FX محقق/غير محقق · PR-X-010 وعكسها الآلي · **قواعد:** PR-A-010/011/012/013/020/030 · PR-S-031 · PR-T-010/011/012/013/020/021/022/040/050 · PR-X-010 | سيناريوهات `07` §10 رقم 2·7·18·19 | AC-26 · AC-27 · AC-28 · AC-29 · AC-30 · AC-31 · AC-32 · AC-33 · AC-66 |
| **P8 — الجاهزية والإقفال والتهيئة** | كائن التكلفة (PR-C-010…060) · بوابة الإقفال PR-X-020 · PR-I-060/061 (FIFO فقط) · الطبقة الدلالية الدنيا · معالج التهيئة والاستيراد (**خطوة الأرصدة الافتتاحية محجوبة — GAP-01**) · إطار التكامل الأدنى | **اختبار الجاهزية `03` §6.1 يمر بأحداث Core وحدها** | AC-10 · AC-16 · AC-36 · AC-39 · AC-40 · AC-41 · AC-42 |
| **P9 — التصلّب وإغلاق الموجة 1** | انحدار كامل للـ70 + الثوابت المرقّمة · اختبارات تزامن (المتوسط · الترقيم) · اختبار الحذف · مراجعة أمنية · وثائق التشغيل | تقرير قبول الموجة 1 | الـ70 كاملة + 84 ثابتاً مرقّماً |

> **نقطة التوقف المعلومة مسبقاً:** عند P8/التهيئة يتوقف العمل على الأرصدة الافتتاحية حتى ورود ملحق GAP-01 (§13). لا يتوقف باقي P8.

### 9.3 تغطية المراحل لعناصر السلطة
| العنصر | P3 | P4 | P5 | P6 | P7 | P8 | المجموع |
|---|---|---|---|---|---|---|---|
| قواعد الترحيل النافذة (62) | 1 | 10 | 14 (+1 مسحوبة) | 10 | 17 | 10 | **62 (+1)** |
| أنواع المستندات (27 تقنياً / 26 كتالوجياً) | 1 | 5 (+Reservation) | 6 | 7 | 7 | 1 | **27** |
| معايير القبول الأساسية (70) | 13 | 9 | 11 | 11 | 9 | 7 | + P0:2 + P1:4 + P2:4 = **70** |

التفصيل سطراً بسطر في `10A` و`10B`.

---

## 10 — استراتيجية التحقق

| النوع | ما يغطيه | آلية |
|---|---|---|
| **اختبار المطابقة للكتالوج** | معرِّفات الأدوار/القواعد/الحالات/رموز الفشل = الوثائق | يفشل CI عند أي انحراف أو قاعدة بلا `source_ref` |
| **اختبارات AC** (`test_AC_xx`) | الـ70 المرقّمة، كلٌّ باسمه | pytest على Postgres حقيقي؛ Given/When/Then كما في النص |
| **اختبارات الثوابت المرقّمة** | RRI · OWN · BIL · RES · RSP · PPV · COS · DIS · SRC · ROU · PM · GS · PS · CC · REV · PC · CX · NUM · MEX (84) | اختبارات خصائص (Property-based) حيث أمكن |
| **حقن الفشل** | AC-61 · AC-69 · PS-04 | إسقاط استثناء في كل خطوة من خطوات الخط (§4) والتحقق من صفر أثر وصفر رقم |
| **حزام الثوابت بعد كل اختبار** | مدين=دائن · دفتر المخزون = `ACC.INV.*` · لا سالب WMA · الفرعيات متسقة · لا مستند يتيم في معاملة مركبة · لا UPDATE على المُرحَّل | `assert_invariants()` يُنفَّذ تلقائياً بعد كل سيناريو |
| **اختبار الحذف** | P6 | CI يحذف `industry/*` ويعيد التشغيل |
| **التزامن** | المتوسط المرجح · الترقيم · التخصيص | معاملات متوازية على نفس الصنف/النطاق |
| **السيناريوهات العشرون** (`07` §10) | 19 قابلة (15 محجوب بـPD-101 على WMA؛ يُختبر على FIFO) | كل سيناريو اختبار تكامل |

---

## 11 — القرارات التقنية المطلوب اعتمادها (ليست وظيفية)

| # | القرار | البديل المرفوض/المكافئ | الأثر إن رُفض |
|---|---|---|---|
| TD-1 | Modular Monolith + PostgreSQL 17 | Microservices (يخالف P1) | — |
| TD-2 | Python 3.13 للنواة (Domain-first) | TypeScript/Node 20 مكافئ | إعادة كتابة صياغية فقط؛ التصميم ثابت |
| TD-3 | الجمود على مستوى DB (INSERT-only + محفزات) | جمود بالكود فقط (أضعف) | — |
| TD-4 | `layer_adjustment`/`layer_consumption` كسجلات Append-only بدل تعديل الطبقة | UPDATE على الطبقات (خرق CF-01) | — |
| TD-5 | اشتقاق الحالات الفرعية متزامناً داخل معاملة الترحيل | اشتقاق لاحق بالأحداث (يكسر AC-59/60 لحظياً) | — |
| TD-6 | عدّاد ترقيم معاملاتي مقفول | تسلسل غير معاملاتي + سجل فجوات | فجوات أكثر (مسموحة إن فُسِّرت) |
| TD-7 | تعدد المستأجرين بقاعدة بيانات لكل عميل (لا `tenant_id` في المخطط؛ `entity_id` في كل شيء) | `tenant_id` مشترك | يُضاف لاحقاً بهجرة إن لزم |
| TD-8 | رموز فشل تقنية مقترحة: `FAIL-RULE-01` (لا قاعدة منطبقة) · `FAIL-RULE-02` (تساوي تخصيص RSP-02) · `FAIL-CFG-04` (عتبة اعتماد غير مضبوطة) | إعادة استخدام رموز موجودة بدلالة أوسع | — |
| TD-9 | الاختبارات الآلية تستخدم ولاية ضريبية `TEST` صريحة غير مشحونة مع المنتج | لا اختبار للسيقان الضريبية إطلاقاً | فقدان تغطية PR-S-030/032… |
| TD-10 | واجهة HTTP رقيقة تُضاف من P5 لخدمة اختبارات التكامل — بلا شاشات | — | — |

---

## 12 — الأسئلة والفجوات المرفوعة (لا تُحل ذاتياً)

| ID | البند | التصنيف | الشدة | ماذا يحجب | ما فعلتُه ريثما يُحسم |
|---|---|---|---|---|---|
| **Q-A2-01** | **98 معيار قبول مقابل 70 مرقّماً.** الـ28 «المضافة» (`08` §2.4) غير مرقّمة ولا معرَّفة في أي وثيقة | فجوة توثيق | **عالية** (تحجب اكتمال مصفوفة التحقق لا التصميم) | إغلاق الموجة 1 بمعيار «98» | غطّيتُ الـ70 + 84 ثابتاً مرقّماً كاختبارات؛ أطلب تعريف الـ28 أو اعتماد الثوابت بديلاً |
| **Q-A2-02** | **Fixed Assets** «الموجة 1 (مخفف)» في `03` §2.2 بلا أي قاعدة ترحيل أو آلة حالات في `04`–`07` | FUNCTIONAL GAP | متوسطة | بناء محرك الأصول | مستبعَد من خطة البناء حتى ملحق وظيفي |
| **Q-A2-03** | **Correction Document** (SF-07 · PS-02) بلا قاعدة ولا آلة حالات | FUNCTIONAL GAP | متوسطة | مسار التصحيح الداخلي (تكلفة/بُعد) | خانة محجوزة؛ شجرة القرار تعرضه كمسار بديل غير مفعَّل |
| **Q-A2-04** | **إشعار مورد دائن/مدين** (شجرة `07` §4.3) بلا قاعدة | FUNCTIONAL GAP | منخفضة | تعديل قيمة فاتورة مورد بلا مرتجع | غير مبني؛ PR-P-031/032 تغطي فروق السعر فقط |
| **Q-A2-05** | **فاتورة أعباء فعلية (PR-P-051):** أسس الفاتورة الخمسة لا تحوي «عبء منسوب لاستلامات»، وAC-50 يتكلم عن «مساراتها الخمسة» | تفسير نمذجة | متوسطة | تنفيذ PR-P-051 | أقترح `line_kind = LANDED_COST` يشير إلى سطور GR، تحت قاعدة PR-P-051 القائمة، بلا أثر كمّي — **أطلب تأكيد التفسير** |
| **Q-A2-06** | مسار اعتماد يشير إلى **عتبة غير مضبوطة** (SD-02): منع الإرسال أم تجاوز الاعتماد؟ | قرار وظيفي صغير | متوسطة | توجيه المستندات قبل ضبط العتبات | المقترح التقني: منع بـ `FAIL-CFG-04` اتساقاً مع فلسفة «لا افتراض» |
| **Q-A2-07** | **GR: اجتياز الفحص (`GR.RELEASE`)** — `03` §5.1 يقول GL «—»، بينما `ACC.INV.HOLD` دور مستقل في `04`، ولا قاعدة إعادة تصنيف Hold→OnHand | تعارض ظاهري/فجوة | متوسطة | POL-INV-005 (معطّلة افتراضياً — لا يحجب الآن) | أطبّق Foundation (لا قيد) وأرفع السؤال: إما ربط `HOLD` بنفس حساب `ONHAND` تهيئةً، أو قاعدة إعادة تصنيف بملحق |
| **Q-A2-08** | القائمة القانونية للمستندات الـ26 (هل CN/DN نوع واحد؟ Cash Session ضمنها؟) | تأكيد | منخفضة | لا شيء | نمذجتُ 27 نوعاً تقنياً (`10A` §C) |
| **Q-A2-09** | فروق عدّ: «17 حالة فشل» مقابل 19 معرِّفاً؛ «58 قاعدة» في `04` مقابل 57 معرِّفاً | تأكيد | منخفضة | لا شيء | أنفّذ بالمعرِّفات؛ أطلب تثبيت الأعداد في الوثائق |
| **Q-A2-10** | هل `07` §1.3 (الحالات العامة لكل مستند) **حصري** أم ملخص؟ يؤثر على `Approved` (Adjustment) و`Ready to Pick` (Delivery) و`Rejected` | تأكيد | منخفضة | تعريفات آلات الحالات في P3 | طبّقتُ الأسبقية: `08` تُثبت `Approved`؛ والباقي كما في `05` |
| **Q-A2-11** | كتالوج مقاييس الطبقة الدلالية (C-20) غير موجود؛ و`PO.SUBMIT` تذكر «حد ائتمان المورد» بلا سياسة معرَّفة ضمن الـ22 | FUNCTIONAL GAP | منخفضة | C-20 الكامل · حارس ائتمان المورد | الحد الأدنى للمقاييس بدلالة الأدوار؛ حارس ائتمان المورد **غير مفعَّل** بلا سياسة |
| **GAP-01** | **Opening Balance Document** | BLOCKER معلوم | **عالية للتشغيل** | خطوة الأرصدة الافتتاحية في P8 وتشغيل أي كيان حقيقي | خانة محجوزة؛ متطلبات الملحق في §13؛ **أوصي ببدء Agent 1 فيه الآن بالتوازي** حتى لا تتوقف P8 |

---

## 13 — ما يحتاجه التصميم من ملحق GAP-01 (حتى يكتبه Agent 1 موجَّهاً)

> ليست اقتراحاً لمحتوى القواعد — بل قائمة الأسئلة التي يجب أن يجيب عنها الملحق حتى يكون قابلاً للتنفيذ.

1. **آلة حالات** مستند الرصيد الافتتاحي (هل يتبع الموحدة؟ صلاحية مراقب مالي؟ يُعكس؟).
2. **قواعد الترحيل لكل فئة رصيد:** مخزون (كمية + قيمة ⇒ طبقة مصدرها `OPENING_BALANCE` — بأي مصدر تكلفة؟ وهل يُعدّ «تاريخ تكلفة» لسلاسل COS/SRC؟) · ذمم مدينة/دائنة (بنود مفتوحة بتواريخ استحقاق وأسعار مثبتة؟) · نقد/بنك · دفعات مقدمة مفتوحة · GRNI/DNI مفتوحة · أرصدة حسابات أخرى.
3. **الدور المقابل:** هل يلزم دور حساب جديد (مثل رصيد افتتاحي/حقوق ملكية) — يرفع العدد عن 44؟
4. **تفاعله مع الفترات** (فترة افتتاحية خاصة؟) و**بوابة الإقفال** و**تقرير الأعمار**.
5. **حدود الاستخدام:** مرة واحدة لكل كيان؟ ماذا عن صنف جديد بعد التشغيل (`06` §7 يشير إلى أنه «ليس جرداً»)؟
6. **معايير قبول** خاصة به (تنضم إلى الـ98).

---

## 14 — ⛔ طلب الاعتماد

**المطلوب من Product Director (ومن Agent 1 فيما يخص الفجوات):**

1. اعتماد المعمارية ونموذج البيانات والمحركات (الأقسام 3–6) أو طلب تعديلات محددة.
2. اعتماد ترتيب البناء (القسم 9).
3. البتّ في القرارات التقنية TD-1…TD-10 (القسم 11).
4. الإجابة عن Q-A2-01…11 (القسم 12) — خاصة **Q-A2-01** (الـ28 معياراً) و**Q-A2-05** (فاتورة الأعباء) لأنهما يمسّان P5 والإغلاق.
5. توجيه Agent 1 لبدء ملحق **GAP-01** بالتوازي (القسم 13).

**لن يُكتب سطر كود قبل ورود الاعتماد.** عند الاعتماد، تبدأ P0 فوراً؛ وأي بند من §12 يُحسم لاحقاً يُدمج في مرحلته دون إعادة تصميم.

---

**نهاية Technical Design v0.1**
*لا قرار وظيفي جديد · لا قاعدة مخترعة · لا شاشات · لا كود*
