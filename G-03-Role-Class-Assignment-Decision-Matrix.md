# G-03 — ROLE_CLASS ASSIGNMENT DECISION MATRIX

**النوع:** 🟡 **ANALYSIS ONLY · NON-EXECUTABLE · NON-AUTHORITATIVE · NO GATE CLOSURE · NO DECISION**
**النطاق:** ⛔ **`G-03` فقط** · **الحالة:** 🔴 **`G-03 = OPEN`**
**التاريخ:** 2026-09-20 · **المُعِدّ:** Agent 1 — ERP Product & Functional Architect
**يبني على:** `G-03 — ROLE_CLASS SOURCE / PD DECISION PACKAGE` *(مقبول كـDecision Package)*

**الثوابت:** **`AC = 73` · `Screens = 136` · `Reports = 34` · `Document Types = 26` · `Roles = 44` · `Posting Rules = 63` · `Core = 24`**

> ⛔ **لا إغلاق `G-03` · لا اعتماد `OPT-1…6` · لا اعتماد `16-FRP-01` · لا اعتماد أي قيمة من الـ39 · لا اشتقاق آلي · لا اختراع `role_class` · لا تعديل `06`/`62`/Registry · لا Registry row · لا SHA · لا Agent 2 · لا Phase I · لا `B-0` · لا Coding/DB/API/Migration · لا `UI-W7` · لا Decision Record.**

---

## §1 — PURPOSE

**تمكين Product Director من اتخاذ قرار صريح على مستوى كل Role من الـ44 — دون أن يتخذ Agent 1 القرار نيابة عنه.**

| البند | الحالة |
|---|---|
| **ما تفعله هذه الوثيقة** | تعرض لكل دور: **ما هو مثبَّت سلطوياً** · **ما هو موجود كقرينة غير سلطوية** · **ما هو غائب تماماً** — بفصل صارم بين الثلاثة |
| **ما لا تفعله** | ⛔ **لا تقرر · لا ترجّح · لا تشتق · لا تكمل · لا تغلق** |
| **خانة `Final PD Decision`** | 🔲 **فارغة في كل صف — بلا استثناء** *(§11)* |

---

## §2 — SOURCE CONSTRAINTS

### 2.1 — القواعد المعتمدة الحاكمة

| القاعدة | النص | الحالة |
|---|---|---|
| **`RC-01`** | «كل دور من الـ**44** يحمل `role_class`: **`RESULT`** يُغلق في قائمة الدخل · **`POSITION`** يُرحَّل رصيده» | 🟢 **APPROVED** |
| **`RC-02`** | «**بيان صريح مخزَّن** … **ممنوع اشتقاقه من بادئة الرمز** … **بأي منطق نصي**» | 🟢 **APPROVED** |
| **`RC-03`** | «**22 `POSITION` · 22 `RESULT` · المجموع 44**» · **`L-04`:** لا إضافة ولا حذف | 🟢 **APPROVED** |
| **`RC-04`** | «**مدخل إلزامي** لسلسلة حل الحساب · **يُعرض** مع كل سطر قيد» | 🟢 **APPROVED** |
| **`L-05`** | «لا يُوسَّع `RC-01…RC-04` بالقياس» | 🟢 **APPROVED** |

### 2.2 — أسس الاشتقاق المحظورة *(أمر PD §4)*

| # | ⛔ **محظور كأساس تصنيف** | السند |
|---|---|---|
| 1 | **اسم الدور وحده** | `RC-02` |
| 2 | **`Prefix`** | `RC-02` نصّاً |
| 3 | **نوع المستند** | `L-05` |
| 4 | **عمود «النوع» في `04`** | أمر PD · `16` `R-03` *(رفض النهج)* |
| 5 | **نمط `ACC.REV.*`** | أمر PD §8 |
| 6 | **نمط `ACC.EXP.REASON.*`** | أمر PD §7 |
| 7 | **أي `pattern` مشابه** | أمر PD §4 |
| 8 | **`fallback` · `default`** | `RES-09` «بلا هبوط» · `62` §5.3 |

> ✅ **الاستثناء الوحيد:** **نصّ سلطوي يذكر `role_class` صراحةً.**

### 2.3 — حالة قائمة الـ44

| البند | الحالة |
|---|---|
| **المصدر** | **نفس قائمة `G-03 Package`** — `04` §1.1–1.5 *(43)* + `06` §1 *(`ACC.REV.DEFERRED`)* |
| **إضافة · حذف · إعادة ترقيم · تغيير `Role ID`** | ⛔ **صفر** — **44/44 مطابقة** |

### 2.4 — دلالة الأعمدة

| العمود | المعنى |
|---|---|
| **`Existing Explicit role_class`** | 🟢 **قيمة مثبَّتة في نصّ سلطوي** — أو **`NONE`** |
| **`Evidence Status`** | `APPROVED` / `PROVISIONAL` / `REFERENCE` / `UNKNOWN` |
| **`Candidate role_class`** | **`POSITION`** / **`RESULT`** **فقط إذا كانت سلطوية** · وإلا **`UNRESOLVED`** |
| 🟡 **`Candidate for PD review`** | **قرينة مصدرية منقولة — 🔴 ليست قراراً ولا اعتماداً ولا ترجيحاً من Agent 1** |
| **`Authoritative?`** | `YES` / **`NOT ESTABLISHED`** |
| **`Final PD Decision`** | 🔲 **فارغة دائماً** |

### 2.5 — 🔴 بيان حاكم على عمود «`Candidate for PD review`»

> **كل قيمة في هذا العمود منقولة حرفياً من `16-FRP-01-Revision-1.md` §3 — وهو:**
> **`Provisional Reference Only · خارج سلسلة السلطة · لا يُنفَّذ منه شيء`** *(`09` §2)* · **وخارج `GOV-01` Registry** *(`FND-G03-02`)* · **وحالته محل تعارض حاكم مفتوح** *(`FND-G03-01`)*.
>
> ⛔ **النقل ≠ الاعتماد.** ⛔ **الوجود في العمود ≠ ترشيح.** ⛔ **لم يُشتق أيٌّ منها ولم يُولَّد ولم يُراجَع موضوعياً من Agent 1.**
> **وظيفته الوحيدة:** وضع القرينة أمام Product Director **مفصولة عن الدليل السلطوي** — تنفيذاً لأمر PD §5.

---

## §3 — 44-ROLE MATRIX

> **الأعمدة:** `#` · `Role ID` · `Role Name` · `Source Description` · `Existing Explicit role_class` · `Evidence Source` · `Evidence Status` · `Candidate role_class` · 🟡`Candidate for PD review` · `Authoritative?` · `If not — why?` · `PD Decision Required` · `Conflict / Caveat`

### 3.1 — الأصول *(`04` §1.1)*

| # | Role ID | Role Name | Source Description | Existing Explicit | Evidence Source | Evidence Status | Candidate role_class | 🟡 Candidate for PD review *(غير سلطوي)* | Authoritative? | If not — why? | PD Decision | Conflict / Caveat |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | `ACC.INV.ONHAND` | مخزون في المواقع الفيزيائية | «أصل» · إلزامي: نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | المصدر الوحيد `16` = خارج سلسلة السلطة | ✅ **YES** | `FND-G03-01` |
| 2 | `ACC.INV.TRANSIT_INT` | مخزون في الطريق — تحويل داخلي | «أصل» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 3 | `ACC.INV.TRANSIT_IN` | بضاعة في الطريق واردة (انتقلت ملكيتها) | «أصل» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 4 | `ACC.INV.HOLD` | مخزون قيد الفحص | «أصل» · عند تفعيل `POL-INV-005` | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ **مشروط بسياسة** — أثره على «دور نشط» غير موصوف |
| 5 | `ACC.INV.COSTOBJ` | كائن التكلفة / تحت التشغيل (WIP) | «أصل (WIP)» · جاهزية L3 | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ **`G-07`/`TD-Q-05`** يخصّان `Cost Object` **كمستند** — ⛔ **موضوع مختلف · لا خلط** |
| 6 | `ACC.AR.TRADE` | ذمم عملاء تجارية | «أصل» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 7 | `ACC.AR.DNI` | مسلَّم غير مفوتر | «أصل» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ `62` §17 يذكر «فحص `ACC.REV.SALES` = 0» لـ`B-5` — **لا صلة بالتصنيف** |
| 8 | `ACC.AP.ADVANCE` | دفعات مقدمة لموردين | «أصل» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 9 | `ACC.CASH.ONHAND` | نقدية بالصندوق | «أصل» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 10 | `ACC.CASH.BANK` | حسابات بنكية | «أصل» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 11 | `ACC.CASH.CHQ_IN` | شيكات تحت التحصيل | «أصل» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ **`G-07`** يخصّ `Cheque Received` **كمستند** — ⛔ **لا خلط** |

### 3.2 — الالتزامات *(`04` §1.2)*

| # | Role ID | Role Name | Source Description | Existing Explicit | Evidence Source | Evidence Status | Candidate role_class | 🟡 Candidate for PD review *(غير سلطوي)* | Authoritative? | If not — why? | PD Decision | Conflict / Caveat |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 12 | `ACC.AP.TRADE` | ذمم موردين تجارية | «التزام» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | المصدر الوحيد `16` | ✅ **YES** | `FND-G03-01` |
| 13 | `ACC.AP.GRNI` | بضاعة مستلمة غير مفوترة | «التزام» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 14 | `ACC.AP.ACCR_LANDED` | أعباء شراء مستحقة | «التزام» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 15 | `ACC.AR.ADVANCE` | دفعات مقدمة من عملاء | «التزام» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ `06`: ترحيل دفعة مقدمة إلى `REV.DEFERRED` أو العكس ⇒ **`FAIL-REV-02`** — **حاجز بنيوي لا تصنيف** |
| 16 | `ACC.CASH.CHQ_OUT` | شيكات صادرة لم تُصرف | «التزام» · نعم | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ **`G-06`** يخصّ `Cheque Issued` **كمستند** — ⛔ **لا خلط** |
| 17 | `ACC.TAX.OUTPUT` | ضريبة مخرجات مستحقة | «التزام» · حسب الولاية | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ **`G-11`/`PD-102`** — الفتحات الضريبية محجوبة *(موضوع مستقل)* |
| 18 | `ACC.TAX.OUT_ADV` | ضريبة مستحقة على دفعات مقدمة | «التزام» · **معلّق — `OD-02`** | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 *(موسوم «معلّق OD-02»)* | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ **معلَّق بـ`OD-02`** · **`G-11`** · `62` §11.2 يجعل الساق الضريبية فتحة فارغة |

### 3.3 — الإيرادات والمكاسب *(`04` §1.3)*

| # | Role ID | Role Name | Source Description | Existing Explicit | Evidence Source | Evidence Status | Candidate role_class | 🟡 Candidate for PD review *(غير سلطوي)* | Authoritative? | If not — why? | PD Decision | Conflict / Caveat |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 19 | `ACC.REV.SALES` | إيراد المبيعات | «إيراد» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | المصدر الوحيد `16` | ✅ **YES** | 🔴 **`FND-G03-05`** — `62` §5.4 **Design Evidence فقط** *(§9)* |
| 20 | `ACC.REV.ACCRUED` | إيراد مستحق (تسليم بلا فوترة) | «إيراد» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | 🔴 **`FND-G03-05`** |
| 21 | `ACC.REV.RETURNS` | مردودات مبيعات | «إيراد مقابل» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | 🔴 **`FND-G03-05`** · ⚠️ **«إيراد مقابل» فئة مركَّبة** |
| 22 | `ACC.REV.DISCOUNT` | خصم مسموح به | «إيراد مقابل» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | 🔴 **`FND-G03-05`** · ⚠️ فئة مركَّبة |
| 23 | `ACC.REV.OTHER` | إيرادات أخرى (دفعات مصادَرة) | «إيراد» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | 🔴 **`FND-G03-05`** · ⚠️ `05`: `ADV.FORFEIT` يحتاج «صلاحية عليا» ⇒ **`TD-Q-06` — موضوع مختلف** |
| 24 | `ACC.GAIN.INV_SURPLUS` | زيادة مخزون من الجرد | «إيراد/تسوية» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ **«إيراد/تسوية» فئة مركَّبة** |
| 25 | `ACC.GAIN.CASH_OVER` | زيادة صندوق | «إيراد/تسوية» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ فئة مركَّبة · **`G-06`** يخصّ `Cash Session` فرق **كمستند** — ⛔ لا خلط |

### 3.4 — التكاليف والمصروفات *(`04` §1.4)*

| # | Role ID | Role Name | Source Description | Existing Explicit | Evidence Source | Evidence Status | Candidate role_class | 🟡 Candidate for PD review *(غير سلطوي)* | Authoritative? | If not — why? | PD Decision | Conflict / Caveat |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 26 | `ACC.COGS.MAIN` | تكلفة المبيعات | «تكلفة» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 **بتعليق صريح:** «رغم ارتباطه بالمخزون، **تكلفة المبيعات مصروف يُغلق في قائمة الدخل**… **الالتباس متوقع، ولذلك ثُبِّت نصاً**» | **NOT ESTABLISHED** | 🔴 **التعليق داخل `16` — لا يرفعه إلى السلطة** | ✅ **YES** | 🔴 **قرينة مشدَّدة — ⛔ لم تُرفَّع** |
| 27 | `ACC.COGS.ADJ` | تسوية تكلفة المبيعات (أثر رجعي) | «تكلفة» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | المصدر الوحيد `16` | ✅ **YES** | `FND-G03-01` |
| 28 | `ACC.EXP.PPV` | فرق سعر الشراء | «مصروف» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ `62` `B-4`: `PPV` مرتبط بـ`GAP-P1-05` *(عتبة التسامح)* — **موضوع مستقل** |
| 29 | `ACC.EXP.PROMO` | مصروف ترويجي وعينات | «مصروف» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 30 | `ACC.EXP.SHRINK` | عجز مخزون | «مصروف» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 31 | `ACC.EXP.SCRAP_ABN` | هالك فوق المعياري | «مصروف» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ **`TD-Q-04`** *(المرتجع التالف)* — **موضوع مستقل مفتوح** |
| 32 | `ACC.EXP.TRANSIT_LOSS` | عجز نقل | «مصروف» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 33 | `ACC.EXP.CASH_SHORT` | عجز صندوق | «مصروف» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ **`G-06`** — `Cash Session` فرق **كمستند** · ⛔ لا خلط |
| 34 | `ACC.EXP.BANK_FEES` | رسوم بنكية | «مصروف» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | `FND-G03-01` |
| 35 | `ACC.EXP.REASON.<code>` | **مصروف مرتبط برمز سبب (نمط ديناميكي)** | «مصروف» · **`04` §1.6: «ليس دوراً واحداً بل عائلة أدوار»** | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 *(صفّ واحد #37)* | **NOT ESTABLISHED** | نفس السبب · **+ طبيعة العدّ غير محسومة** | ✅ **YES — مزدوج** | 🔴 **`FND-G03-03`** — **عائلة أم دور؟ `UNKNOWN`** ⇒ **§8** |

### 3.5 — الفروق والوسائط *(`04` §1.5)*

| # | Role ID | Role Name | Source Description | Existing Explicit | Evidence Source | Evidence Status | Candidate role_class | 🟡 Candidate for PD review | Authoritative? | If not — why? | PD Decision | Conflict / Caveat |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 36 | `ACC.FX.REALIZED` | فروق عملة محققة | «إيراد/مصروف» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | المصدر الوحيد `16` | ✅ **YES** | ⚠️ **فئة مركَّبة** · `A-6`/`FX-NEG-01` **موضوع مستقل** |
| 37 | `ACC.FX.UNREALIZED` | فروق عملة غير محققة | «إيراد/مصروف» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ فئة مركَّبة · `PR-X-010` إعادة تقييم |
| 38 | `ACC.MISC.ROUNDING` | فروق التقريب | «إيراد/مصروف — **`OD-03`**» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `RESULT` — `16` §3.2 | **NOT ESTABLISHED** | نفس السبب | ✅ **YES** | ⚠️ فئة مركَّبة · **`OD-03`** · `ROU-07 = ROUND_HALF_UP` **موضوع مستقل** |
| 39 | **`ACC.CTRL.APPLIED_LABOR`** | عمالة محمّلة | «**حساب مقابل**» | 🟢 **POSITION** | **`06` §1.1 جدول `RC-02`** | 🟢 **APPROVED** | 🟢 **POSITION** | — *(لا حاجة)* | ✅ **YES** | — | ❌ **NO** | — |
| 40 | **`ACC.CTRL.APPLIED_OH`** | أعباء محمّلة | «**حساب مقابل**» | 🟢 **POSITION** | **`06` §1.1 جدول `RC-02`** | 🟢 **APPROVED** | 🟢 **POSITION** | — | ✅ **YES** | — | ❌ **NO** | — |
| 41 | **`ACC.CTRL.COSTOBJ_VAR`** | فروق تسوية كائن التكلفة | «مصروف/تكلفة» · `06`: «**فرق تسوية**» | 🟢 **RESULT** | **`06` §1.1 جدول `RC-02`** | 🟢 **APPROVED** | 🟢 **RESULT** | — | ✅ **YES** | — | ❌ **NO** | ⚠️ `06` يسجّل أن `ACC.CTRL.*` **تحمل تصنيفين** — دليل بطلان الاشتقاق |
| 42 | **`ACC.INV.REVAL`** | فرق إعادة تقييم المخزون | «مصروف/إيراد» | 🟢 **RESULT** | **`06` §1.1 جدول `RC-02`** | 🟢 **APPROVED** | 🟢 **RESULT** | — | ✅ **YES** | — | ❌ **NO** | ⚠️ **الحالة الثانية المبطِلة للاشتقاق بالبادئة** |
| 43 | `ACC.TAX.INPUT` | ضريبة مدخلات | «أصل» | **NONE** | — | **UNKNOWN** | 🔴 **UNRESOLVED** | `POSITION` — `16` §3.1 | **NOT ESTABLISHED** | المصدر الوحيد `16` | ✅ **YES** | ⚠️ **`G-11`** — الفتحات الضريبية محجوبة |

### 3.6 — الدور المضاف في `06`

| # | Role ID | Role Name | Source Description | Existing Explicit | Evidence Source | Evidence Status | Candidate role_class | 🟡 Candidate for PD review | Authoritative? | If not — why? | PD Decision | Conflict / Caveat |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 44 | **`ACC.REV.DEFERRED`** | إيراد مؤجَّل / التزام عقدي | «**التزام**» *(`06` §1)* — فاتورة صدرت قبل انتقال السيطرة | 🟢 **POSITION** | **`06` §1.1 جدول `RC-02`** | 🟢 **APPROVED** | 🟢 **POSITION** | — | ✅ **YES** | — | ❌ **NO** | ⚠️ **الحالة الأولى المبطِلة للاشتقاق** · `FAIL-REV-02` · 🔴 **`FND-G03-05`: بادئته `REV` ⇒ دليل قاطع على أن نمط `ACC.REV.*` لا يُعمَّم** |

---

## §4 — EXPLICITLY APPROVED VALUES

> **خمس قيم — كل منها بنصّ سلطوي في `06` §1.1 جدول `RC-02`.**

| # | Role ID | `role_class` | النصّ المثبِّت |
|---|---|---|---|
| 44 | **`ACC.REV.DEFERRED`** | 🟢 **POSITION** | «§1 يعرّفه **التزام** ⇒ يُرحَّل رصيده. اشتقاقه RESULT كان **سيُغلقه في قائمة الدخل فيعترف بإيراد مؤجَّل كإيراد محقق**» |
| 42 | **`ACC.INV.REVAL`** | 🟢 **RESULT** | «`04` §1.5 يصنّفه **مصروف/إيراد** · `PR-I-050` يجعله الطرف المقابل لتغيّر قيمة المخزون» |
| 39 | **`ACC.CTRL.APPLIED_LABOR`** | 🟢 **POSITION** | «`APPLIED_LABOR` · `APPLIED_OH` = **حساب مقابل** ⇒ POSITION» |
| 40 | **`ACC.CTRL.APPLIED_OH`** | 🟢 **POSITION** | *(نفس النص)* |
| 41 | **`ACC.CTRL.COSTOBJ_VAR`** | 🟢 **RESULT** | «`COSTOBJ_VAR` = **فرق تسوية** ⇒ RESULT» |

### 4.1 — 🔴 تحذير منهجي نافذ *(`FND-G03-04`)*

> **عنوان الجدول الحامل لهذه الخمس في `06` §1.1 حرفياً:** «**ثلاث حالات تُبطل الاشتقاق بالبادئة — وتُثبت وجوب `RC-02`**».
> ⇒ **وُضعت كـ*أدلة على فشل الاشتقاق*، لا كـ*نواة كتالوج*.**
> ⛔ **لا تُستنتج منها بقية القيم · لا تُقاس عليها · لا تُعامَل بداية قائمة** *(أمر PD §3)*.

---

## §5 — UNRESOLVED VALUES

| البند | العدد |
|---|---|
| 🔴 **`Candidate role_class = UNRESOLVED`** | **39 / 44** |
| **`Authoritative? = NOT ESTABLISHED`** | **39 / 44** |
| **`PD Decision Required = YES`** | **39 / 44** *(منها واحد مزدوج — `#35`)* |
| **`Evidence Status = UNKNOWN`** | **39 / 44** |

### 5.1 — سبب عدم الاعتماد — موحَّد

> **لكل الأدوار الـ39:** **لا يوجد نصّ في أي وثيقة Functional Authority يثبّت `role_class` لهذا الدور.**
> **القرينة الوحيدة المتوفرة** هي `16-FRP-01-Revision-1.md` §3 — **`Provisional Reference Only` · خارج سلسلة السلطة · خارج Registry · حالته محل تعارض حاكم مفتوح**.
> ⇒ **`NOT ESTABLISHED`** — **لا لأن القيمة «مشكوك فيها موضوعياً»، بل لأن المصدر لا يملك صلاحية التثبيت.**

### 5.2 — تصنيف فرعي للأدوار الـ39 *(وصفي — لا ترجيح)*

| الفئة | العدد | الأدوار |
|---|---|---|
| **بقرينة `16` فقط** | **32** | `#1`–`#3` · `#6` · `#8`–`#14` · `#19`–`#20` · `#22`–`#23` · `#27`–`#30` · `#32` · `#34` · `#36`–`#38` وما شابهها |
| **بقرينة `16` + تحفظ إضافي مسجَّل** | **7** | `#4` *(سياسة)* · `#5` *(L3)* · `#18` *(`OD-02`)* · `#21`/`#24`/`#25` *(فئة مركَّبة)* · `#26` *(تعليق `16` المشدَّد)* |
| **بقرينة `16` + فجوة طبيعة** | **1** | `#35` `ACC.EXP.REASON.<code>` |
| **متأثر بـ`FND-G03-05`** | **5** | `#19`–`#23` *(`ACC.REV.*` غير المثبَّتة)* |
| **متأثر بـ`G-11`** | **3** | `#17` · `#18` · `#43` |

> ⛔ **هذا تصنيف للتحفظات — لا للقيم. لا يقترب من تحديد `POSITION`/`RESULT` لأي دور.**

---

## §6 — EVIDENCE vs CANDIDATE SEPARATION

### 6.1 — القاعدة المطبَّقة

```
Evidence            : "المصدر X يذكر ..."            ← نقل نصّي
Evidence Status     : APPROVED / PROVISIONAL / REFERENCE / UNKNOWN
Candidate role_class: POSITION | RESULT  ← فقط إن كان المصدر سلطوياً
                      UNRESOLVED         ← في كل ما عدا ذلك
Candidate for PD review : قرينة منقولة — 🔴 ليست قراراً
Authoritative status    : YES | NOT ESTABLISHED
```

### 6.2 — أمثلة تطبيقية من المصفوفة

| الحالة | Evidence | Evidence Status | Candidate role_class | Authoritative? |
|---|---|---|---|---|
| **`ACC.REV.DEFERRED`** | «`06` §1.1: §1 يعرّفه **التزام** ⇒ يُرحَّل رصيده» | 🟢 **APPROVED** | 🟢 **POSITION** | ✅ **YES** |
| **`ACC.INV.ONHAND`** | «`16` §3.1 يدرجه ضمن الأصول والالتزامات» | 🔴 **UNKNOWN** *(المصدر Provisional)* | 🔴 **UNRESOLVED** | **NOT ESTABLISHED** |
| **`ACC.COGS.MAIN`** | «`16` §3.2 يعلّق: تكلفة المبيعات **مصروف يُغلق في قائمة الدخل** … **ثُبِّت نصاً**» | 🔴 **UNKNOWN** | 🔴 **UNRESOLVED** | **NOT ESTABLISHED** |
| **`ACC.REV.SALES`** | «`62` §5.4: الدخل يُقرأ من أدوار `ACC.REV.*` (**RESULT**)» | ⚠️ **REFERENCE — Design Evidence** | 🔴 **UNRESOLVED** | **NOT ESTABLISHED** |

### 6.3 — ما لم يُكتب في أي صف

| ⛔ **صيغة محظورة** | الحالة |
|---|---|
| «POSITION — لأنه منطقي» | ⛔ **صفر ورود** |
| «RESULT — لأنه يبدو ناتجاً» | ⛔ **صفر ورود** |
| «غالباً» · «يبدو» · «من المرجَّح» · «بديهي» | ⛔ **صفر ورود** |
| «يمكن اشتقاقه من نوع الدور» | ⛔ **صفر ورود** |
| «يمكن استخدام تصنيف FRP» | ⛔ **صفر ورود** — **`16` منقول كقرينة موسومة، لا كتوصية** |

---

## §7 — RC-03 ARITHMETIC CHECK

### 7.1 — العدّ

| البند | POSITION | RESULT | المجموع |
|---|---|---|---|
| **`Explicitly approved`** | **3** | **2** | **5** |
| **`Unresolved — POSITION candidate`** *(غير سلطوي)* | **19** | — | **19** |
| **`Unresolved — RESULT candidate`** *(غير سلطوي)* | — | **20** | **20** |
| **`Fully unresolved Roles`** *(بلا أي قرينة)* | — | — | **0** |
| **إجمالي غير المحسوم** | — | — | **39** |
| **الإجمالي** | — | — | **44** ✅ |

**تفصيل المرشَّحين غير السلطويين:**
**`POSITION` (19):** `#1`–`#18` · `#43`
**`RESULT` (20):** `#19`–`#38`

### 7.2 — فحص `RC-03` على المعتمَد سلطوياً **فقط**

```
المطلوب بـRC-03 : 22 POSITION + 22 RESULT = 44
المعتمَد سلطوياً :  3 POSITION +  2 RESULT =  5
النتيجة          :  3 ≠ 22  ·  2 ≠ 22  ·  5 ≠ 44
```

> # 🔴 **`RC-03` غير مستوفى بالقيم المعتمدة سلطوياً.**
> **الفجوة:** **19 `POSITION` + 20 `RESULT` = 39 قيمة مفقودة.**
> ⇒ **فجوة تحتاج قرار Product Director.**

### 7.3 — ملاحظة حسابية على مجموعة القرائن *(رصد لا تصديق)*

```
لو أُضيفت قرائن 16 §3 إلى المعتمَد سلطوياً:
POSITION :  3 +  19  =  22
RESULT   :  2 +  20  =  22
المجموع  :             44
```

| البند | التسجيل |
|---|---|
| **الملاحظة** | **مجموعة القرائن غير السلطوية تُنتج حسابياً 22/22/44** |
| **السند المستقل** | `28` §3.4 سجّل تحققاً آلياً سابقاً: «44 صفاً · لا مكرر ولا مفقود · POSITION 22 · RESULT 22 · **أدوار في FRP وليست في `04`: `ACC.REV.DEFERRED` فقط** · **أدوار في `04` وليست في FRP: لا شيء**» |
| 🔴 **حدود هذه الملاحظة** | **التطابق الحسابي ليس إثباتاً سلطوياً.** **`RC-03` يشترط 22/22 — ولا يقول إن كل مجموعة تحقق 22/22 صحيحة.** |
| ⛔ | **لا تُقرأ ترجيحاً · لا تصديقاً · لا توصية باعتماد `16`** · ⛔ **لم أُجبر المصفوفة على 22/22** — الأرقام محسوبة كما وردت |

### 7.4 — قيود حسابية إضافية

| # | القيد |
|---|---|
| 1 | **`#35` `ACC.EXP.REASON.<code>` محسوب وحدة واحدة** — وفق `04` §1 و`62` §5.2. ⚠️ **وطبيعة العدّ غير محسومة** *(`FND-G03-03`)* ⇒ **كل حسابات §7 مشروطة به** |
| 2 | **`62` §5.2:** «التوزيع 22/22 **يُفحص بنائياً**» ⇒ **الفحص يقع في `B-0`، لا في هذه الوثيقة** |
| 3 | **`62` §5.3:** «فحص التحميل **يرفض** أي كتالوج لا يحقق 22/22 **أو يترك دوراً بلا قيمة**» ⇒ **39 دوراً بلا قيمة = رفض تحميل** |

---

## §8 — `ACC.EXP.REASON.<code>` ANALYSIS

> ⛔ **لا قرار في «Role أم Role Family». لا دلالات جديدة.** *(أمر PD §7)*

### 8.1 — النصوص والمواضع

| الموضع | النصّ الحرفي |
|---|---|
| **`04` §1.4** | «`ACC.EXP.REASON.<code>` \| **مصروف مرتبط برمز سبب (نمط ديناميكي)** \| مصروف» |
| **`04` §1.6** | «**نمط الأدوار الديناميكية** — `ACC.EXP.REASON.<code>` **ليس دوراً واحداً بل عائلة أدوار**: كل رمز سبب معرَّف (تلف، عينة، دعاية، استهلاك داخلي، سرقة) يولّد…» |
| **`62` §5.2** *(قائمة الـ44)* | «… `ACC.EXP.BANK_FEES` · **`ACC.EXP.REASON.<code>` (عائلة)** · `ACC.FX.REALIZED` …» |
| **`06` §5.2 `RES-07`** | «المستوى 2 (Reason Code) يسري **حصراً على أدوار `role_class = RESULT`**» |
| **`06` §5.2 `RES-08`** | «تعدد أدوار RESULT ⇒ **تطبيق مستقل لكل دور**» |
| **`06` §5.2 `RES-09`** | «فشل حل RESULT ⇒ **`FAIL-CFG-02` بلا هبوط**» |
| **`16` §3.2** | يعدّه **صفاً واحداً (#37)** — 🔴 **مصدر غير سلطوي** |

### 8.2 — الأثر على العدّ

| البند | التسجيل |
|---|---|
| **وحدة العدّ في `04` §1** | **دور واحد** *(ضمن 43)* |
| **وحدة العدّ في `62` §5.2** | **بند واحد** موسوم «(عائلة)» *(ضمن 44)* |
| **عدد الأعضاء المتولَّدين** | 🔴 **غير محدَّد مسبقاً** — «كل رمز سبب معرَّف» |
| **التوتر البنيوي** | **`04` §1.6 يصرّح «ليس دوراً واحداً»** — بينما **العدّ يحتسبه واحداً** ⇒ **وصف مصدري متوتر، لا حسم** |

### 8.3 — الأسئلة الأربعة

| # | السؤال | الجواب |
|---|---|---|
| **① هل يؤثر على اختبار 44/44؟** | ⚠️ **محتمل — غير محسوم.** العدّ الحالي يحتسبه **واحداً** فيستقيم 44. 🔴 **لكن إن عُدّ كل عضو متولَّد دوراً مستقلاً، فالعدد يتجاوز 44 ويصطدم بـ`L-04`** *(«لا يضيف دوراً»)*. **لا مصدر يحسم أي العدَّين يُطبَّق في الفحص.** |
| **② هل يؤثر على اختبار 22/22؟** | ⚠️ **محتمل — غير محسوم.** إن عُدّ واحداً فأثره **قيمة واحدة**. 🔴 **إن عُدّت الأعضاء أفراداً فالتوزيع يختلّ بعدد غير معروف مسبقاً** — و**`RC-03` يشترط 22/22 بالضبط**. |
| **③ هل يوجد حسم سلطوي؟** | ❌ **لا.** `PD-109`/`A-4` لا يذكره · `RC-01…RC-04` لا تذكره · `62` يوسمه «(عائلة)» **ولا يصف معالجته في الفحص** · `62` §20/§20.1 **لا يرفعه كـ`TD-Q` ولا كـGate** |
| **④ الحالة؟** | 🔴 **`UNKNOWN`** |

### 8.4 — التسجيل النهائي

| البند | الحالة |
|---|---|
| **`role_class`** | 🔴 **`UNRESOLVED — PD DECISION REQUIRED`** *(صف `#35`)* |
| **Role أم Role Family** | 🔴 **`UNKNOWN`** — ⛔ **لم أقرر** |
| **أثره على 44/44** | 🔴 **`UNKNOWN`** |
| **أثره على 22/22** | 🔴 **`UNKNOWN`** |
| **دلالات جديدة** | ⛔ **لم تُصمَّم** |
| ⚠️ **ملاحظة نطاق** | **البند الوحيد مزدوج الفجوة:** ① قيمة مفقودة *(كبقية الـ39)* ② **طبيعة العدّ غير محسومة** *(منفرداً به)* |

---

## §9 — `ACC.REV.*` ANALYSIS

> ⛔ **لا تحويل لأي دليل تصميمي إلى `Approved role_class`.** *(أمر PD §8)*

### 9.1 — ما يقوله `62` — **Design Evidence فقط**

| الموضع | النصّ الحرفي | الصفة |
|---|---|---|
| **`62` §5.4** | «**الطبقة الدلالية:** الدخل يُقرأ من أدوار **`ACC.REV.*` (RESULT)** لا من حالات المستندات (`PS-03` · `RRI-05`)» | ⚠️ **Design Evidence** |
| **`62` §17 `B-5`** | بوابة الخروج: «تقرير DNI · **فحص `ACC.REV.SALES` = 0 قبل التسليم**» | ⚠️ **معيار تحقق — لا تصنيف** |

### 9.2 — لماذا لا يُعتمد

| # | السبب |
|---|---|
| 1 | **`62` = `Design Baseline` — وليس `Functional Authority`** — بنصّ `TR-03` و`G-01-DR-01` §13 |
| 2 | **`62` §5.3 يصرّح بامتناعه:** «**لا تشتق هذه الوثيقة القيم الـ44 ولا تنسخها من `16`**» ⇒ **الوثيقة نفسها تنفي أنها مصدر قيم** |
| 3 | 🔴 **`ACC.REV.DEFERRED` نقض قاطع للتعميم:** بادئته **`REV`** وقيمته المعتمدة **`POSITION`** — و`06` §1.1 يسجّلها **الحالة الأولى المبطِلة للاشتقاق بالبادئة** ⇒ **عبارة «`ACC.REV.*` (RESULT)» لا تصحّ كقاعدة شاملة** |
| 4 | **`RC-02` يحظر الاشتقاق من البادئة** — و`ACC.REV.*` **نمط بادئة** |
| 5 | **أمر PD §4/5 يحظر التصنيف بنمط `ACC.REV.*`** |

### 9.3 — أثره على الأدوار

| # | Role ID | Existing Explicit | الأثر |
|---|---|---|---|
| 19 | `ACC.REV.SALES` | **NONE** | 🔴 **`UNRESOLVED`** — قرينة تصميمية لا تكفي |
| 20 | `ACC.REV.ACCRUED` | **NONE** | 🔴 **`UNRESOLVED`** |
| 21 | `ACC.REV.RETURNS` | **NONE** | 🔴 **`UNRESOLVED`** — ⚠️ «إيراد مقابل» |
| 22 | `ACC.REV.DISCOUNT` | **NONE** | 🔴 **`UNRESOLVED`** — ⚠️ «إيراد مقابل» |
| 23 | `ACC.REV.OTHER` | **NONE** | 🔴 **`UNRESOLVED`** |
| 44 | **`ACC.REV.DEFERRED`** | 🟢 **POSITION** | ✅ **مثبَّت سلطوياً — ويناقض التعميم** |

### 9.4 — التسجيل

| البند | الحالة |
|---|---|
| **`FND-G03-05`** | 🔴 **مفتوح** — سُجِّل كقرينة تحتاج PD |
| **هل له أثر على القرار؟** | ✅ **نعم — محتمل**: قد يقرأه PD تأكيداً لخمسة أدوار · **أو** يستبعده لأن `62` ليس Authority ولأن `ACC.REV.DEFERRED` ينقض التعميم. ⛔ **لم أرجّح** |
| **التحويل إلى `Approved role_class`** | ⛔ **لم يحدث** |

---

## §10 — `FND-G03-01` / `FND-G03-05`

### 10.1 — `FND-G03-01` — **GOVERNANCE CONFLICT** *(⛔ غير محسوم)*

| المصدر | النصّ الحرفي | الاتجاه |
|---|---|---|
| **`09` §2** | «**`16-FRP-01-Revision-1.md` — ليس مرجعاً ملزماً:** **Provisional Reference Only · خارج سلسلة السلطة · لا يُنفَّذ منه شيء.** ما اعتُمد منه **محصور فيما نصّ عليه `29` صراحةً**» | 🔴 **إقصاء** |
| **`29` الرأس** | «**يحكم:** `16-FRP-01-Revision-1.md` — الذي **يفقد صفة `PROVISIONAL REFERENCE ONLY` جزئياً**» · §1: «**لكل بند فيها حالته الخاصة**» | 🟡 **ترقية جزئية** |
| **`30` §2** | «**`FRP-01` لم يدخل سلسلة السلطة**؛ ما دخل هو **قرار `PD-109`**» · «ترتيب الأسبقية **لم تُمس**» | 🔴 **إقصاء** |

| الحقل | التسجيل |
|---|---|
| **التصنيف** | 🔴 **`GOVERNANCE CONFLICT` — مفتوح** |
| **الحسم** | ⛔ **لم يحدث** *(أمر PD §9)* |
| **الاستخدام لتبرير اعتماد `16`** | ⛔ **لم يحدث** — **بالعكس:** ورد في **39 صفاً** كـ`Conflict/Caveat` **يمنع** الاعتماد |
| **أثره على المصفوفة** | **كل قيمة من `16` بقيت في عمود `Candidate for PD review` وحده** — **ولم تنتقل إلى `Existing Explicit` ولا إلى `Candidate role_class`** |
| **مسجَّل سابقاً** | `G-03 Analysis` §11.1 · `G-03 Package` §5 |

### 10.2 — `FND-G03-05` — **DESIGN EVIDENCE ≠ AUTHORITY**

| الحقل | التسجيل |
|---|---|
| **المحتوى** | `62` §5.4: «الدخل يُقرأ من أدوار **`ACC.REV.*` (RESULT)**» — و**`62` = Design Baseline لا Functional Authority** |
| **التصنيف** | ⚠️ **`DESIGN EVIDENCE` — قرينة تحتاج PD** |
| **الأدوار المتأثرة** | **5** — `#19`–`#23` |
| **النقض الداخلي** | 🔴 **`ACC.REV.DEFERRED`** = **POSITION** رغم بادئة `REV` |
| **التحويل إلى قيمة معتمدة** | ⛔ **لم يحدث** |
| **الحالة** | 🔴 **مفتوح** — §9 |

### 10.3 — اكتشافات مرتبطة قائمة *(تسجيل)*

| ID | الحالة |
|---|---|
| **`FND-G03-02`** — `16` خارج `GOV-01` Registry | 🔴 **مفتوح** · ⛔ **لا صف · لا اقتراح · لا SHA** |
| **`FND-G03-03`** — `ACC.EXP.REASON.<code>` | 🔴 **`UNKNOWN`** — §8 |
| **`FND-G03-04`** — الخمس = أدلة بطلان الاشتقاق لا نواة قائمة | 🔴 **تحذير منهجي نافذ** — §4.1 |
| **`CONF-TD-09`** · **`TD-Q-01`** | 🔴 **مفتوحان** |

---

## §11 — PD DECISION SURFACE

> 🔲 **خانة `Final PD Decision` فارغة في كل صف — بلا استثناء.**
> ⛔ **عمود `Candidate for PD review` = قرينة منقولة من مصدر غير سلطوي — ليس ترشيحاً من Agent 1.**

| # | Role ID | Role Name | Current authoritative value | 🟡 Candidate for PD review *(غير سلطوي — `16` §3)* | **Final PD Decision** |
|---|---|---|---|---|---|
| 1 | `ACC.INV.ONHAND` | مخزون في المواقع الفيزيائية | **NONE** | `POSITION` | 🔲 |
| 2 | `ACC.INV.TRANSIT_INT` | مخزون في الطريق — تحويل داخلي | **NONE** | `POSITION` | 🔲 |
| 3 | `ACC.INV.TRANSIT_IN` | بضاعة في الطريق واردة | **NONE** | `POSITION` | 🔲 |
| 4 | `ACC.INV.HOLD` | مخزون قيد الفحص | **NONE** | `POSITION` | 🔲 |
| 5 | `ACC.INV.COSTOBJ` | كائن التكلفة / WIP | **NONE** | `POSITION` | 🔲 |
| 6 | `ACC.AR.TRADE` | ذمم عملاء تجارية | **NONE** | `POSITION` | 🔲 |
| 7 | `ACC.AR.DNI` | مسلَّم غير مفوتر | **NONE** | `POSITION` | 🔲 |
| 8 | `ACC.AP.ADVANCE` | دفعات مقدمة لموردين | **NONE** | `POSITION` | 🔲 |
| 9 | `ACC.CASH.ONHAND` | نقدية بالصندوق | **NONE** | `POSITION` | 🔲 |
| 10 | `ACC.CASH.BANK` | حسابات بنكية | **NONE** | `POSITION` | 🔲 |
| 11 | `ACC.CASH.CHQ_IN` | شيكات تحت التحصيل | **NONE** | `POSITION` | 🔲 |
| 12 | `ACC.AP.TRADE` | ذمم موردين تجارية | **NONE** | `POSITION` | 🔲 |
| 13 | `ACC.AP.GRNI` | بضاعة مستلمة غير مفوترة | **NONE** | `POSITION` | 🔲 |
| 14 | `ACC.AP.ACCR_LANDED` | أعباء شراء مستحقة | **NONE** | `POSITION` | 🔲 |
| 15 | `ACC.AR.ADVANCE` | دفعات مقدمة من عملاء | **NONE** | `POSITION` | 🔲 |
| 16 | `ACC.CASH.CHQ_OUT` | شيكات صادرة لم تُصرف | **NONE** | `POSITION` | 🔲 |
| 17 | `ACC.TAX.OUTPUT` | ضريبة مخرجات مستحقة | **NONE** | `POSITION` | 🔲 |
| 18 | `ACC.TAX.OUT_ADV` | ضريبة على دفعات مقدمة *(معلّق `OD-02`)* | **NONE** | `POSITION` | 🔲 |
| 19 | `ACC.REV.SALES` | إيراد المبيعات | **NONE** | `RESULT` | 🔲 |
| 20 | `ACC.REV.ACCRUED` | إيراد مستحق | **NONE** | `RESULT` | 🔲 |
| 21 | `ACC.REV.RETURNS` | مردودات مبيعات | **NONE** | `RESULT` | 🔲 |
| 22 | `ACC.REV.DISCOUNT` | خصم مسموح به | **NONE** | `RESULT` | 🔲 |
| 23 | `ACC.REV.OTHER` | إيرادات أخرى | **NONE** | `RESULT` | 🔲 |
| 24 | `ACC.GAIN.INV_SURPLUS` | زيادة مخزون من الجرد | **NONE** | `RESULT` | 🔲 |
| 25 | `ACC.GAIN.CASH_OVER` | زيادة صندوق | **NONE** | `RESULT` | 🔲 |
| 26 | `ACC.COGS.MAIN` | تكلفة المبيعات | **NONE** | `RESULT` *(بتعليق مشدَّد في `16`)* | 🔲 |
| 27 | `ACC.COGS.ADJ` | تسوية تكلفة المبيعات | **NONE** | `RESULT` | 🔲 |
| 28 | `ACC.EXP.PPV` | فرق سعر الشراء | **NONE** | `RESULT` | 🔲 |
| 29 | `ACC.EXP.PROMO` | مصروف ترويجي وعينات | **NONE** | `RESULT` | 🔲 |
| 30 | `ACC.EXP.SHRINK` | عجز مخزون | **NONE** | `RESULT` | 🔲 |
| 31 | `ACC.EXP.SCRAP_ABN` | هالك فوق المعياري | **NONE** | `RESULT` | 🔲 |
| 32 | `ACC.EXP.TRANSIT_LOSS` | عجز نقل | **NONE** | `RESULT` | 🔲 |
| 33 | `ACC.EXP.CASH_SHORT` | عجز صندوق | **NONE** | `RESULT` | 🔲 |
| 34 | `ACC.EXP.BANK_FEES` | رسوم بنكية | **NONE** | `RESULT` | 🔲 |
| 35 | `ACC.EXP.REASON.<code>` | **مصروف برمز سبب — عائلة/دور `UNKNOWN`** | **NONE** | `RESULT` *(+ طبيعة العدّ `UNKNOWN`)* | 🔲 |
| 36 | `ACC.FX.REALIZED` | فروق عملة محققة | **NONE** | `RESULT` | 🔲 |
| 37 | `ACC.FX.UNREALIZED` | فروق عملة غير محققة | **NONE** | `RESULT` | 🔲 |
| 38 | `ACC.MISC.ROUNDING` | فروق التقريب | **NONE** | `RESULT` | 🔲 |
| 39 | **`ACC.CTRL.APPLIED_LABOR`** | 🟢 **POSITION** *(`06` §1.1)* | — *(لا حاجة)* | 🔲 |
| 40 | **`ACC.CTRL.APPLIED_OH`** | 🟢 **POSITION** *(`06` §1.1)* | — | 🔲 |
| 41 | **`ACC.CTRL.COSTOBJ_VAR`** | 🟢 **RESULT** *(`06` §1.1)* | — | 🔲 |
| 42 | **`ACC.INV.REVAL`** | 🟢 **RESULT** *(`06` §1.1)* | — | 🔲 |
| 43 | `ACC.TAX.INPUT` | ضريبة مدخلات | **NONE** | `POSITION` | 🔲 |
| 44 | **`ACC.REV.DEFERRED`** | 🟢 **POSITION** *(`06` §1.1)* | — | 🔲 |

### 11.1 — قرارات إطارية مرافقة *(خارج مستوى الدور)*

| # | القرار | الحالة |
|---|---|---|
| **A** | **مصدر السلطة للقيم الـ39** — `OPT-1`…`OPT-6` أو مسار آخر | 🔲 |
| **B** | **مصير `16-FRP-01`** — يُستخدم / لا يُستخدم / مدخل مراجعة | 🔲 |
| **C** | **حسم `FND-G03-01`** — `09` §2 أم `29` أم صيغة ثالثة | 🔲 |
| **D** | **معالجة `ACC.EXP.REASON.<code>`** *(`FND-G03-03`)* | 🔲 |
| **E** | **معالجة `FND-G03-05`** *(`62` §5.4 كقرينة)* | 🔲 |
| **F** | **آلية التحقق من 44/44 و22/22** | 🔲 |
| **G** | **الإذن بتعديل `06` §1.1** *(استثناء READ-ONLY)* | 🔲 |
| **H** | **موقع المصدر المختار من `GOV-01` Registry** *(`FND-G03-02`)* | 🔲 |
| **I** | **الجهة المنفِّذة** *(سابقة `29` §9/1)* | 🔲 |

---

## §12 — EXPLICIT NON-DECISION STATEMENT

| البند | الحالة |
|---|---|
| **إغلاق `G-03`** | ⛔ **لم يحدث** — 🔴 **`G-03 = OPEN`** |
| **اختيار `OPT-1…6`** | ⛔ **لم يحدث** |
| **اعتماد `16-FRP-01`** | ⛔ **لم يحدث** — قيمه في **عمود قرائن موسوم فقط** |
| **اعتماد أي قيمة من الـ39** | ⛔ **لم يحدث** — **39 × `UNRESOLVED` · 39 × `NOT ESTABLISHED`** |
| **اختراع `role_class`** | ⛔ **لم يحدث** |
| **اشتقاق بالاسم/البادئة/نوع المستند/عمود «النوع»/`ACC.REV.*`/`ACC.EXP.REASON.*`/أي نمط** | ⛔ **لم يحدث** |
| **ترقية قرينة إلى قيمة معتمدة** | ⛔ **لم يحدث** — **الفصل قائم في كل صف** |
| **إجبار المصفوفة على 22/22** | ⛔ **لم يحدث** — **الفجوة معلنة: 3 ≠ 22 · 2 ≠ 22** |
| **حسم `FND-G03-01`/`02`/`03`/`05`** | ⛔ **لم يحدث** |
| **حسم `CONF-TD-09` · `TD-Q-01`** | ⛔ **لم يحدث** |
| **تعديل `06` · `62` · Registry · أي Authority** | ⛔ **لم يحدث** — **كل البصمات ثابتة** |
| **Registry row · SHA** | ⛔ **لم يحدث** |
| **Decision Record · Implementation Order · `TR-05`** | ⛔ **لم يُنشأ أيٌّ منها** |
| **Agent 2 · Phase I · `B-0` · Coding · DB/API/Migration · `UI-W7`** | ⛔ **لم يحدث** |
| **استخدام `11`/`13`/Bundle/`erp/`** | ⛔ **لم يحدث** |
| **`Final PD Decision` مملوءة في أي صف** | ⛔ **صفر — 44 خانة فارغة** |
| **`Execution`** | **`ZERO`** |
| **الثوابت** | ✅ **`AC = 73` · `Screens = 136` · `Reports = 34` · `Document Types = 26` · `Roles = 44` · `Posting Rules = 63` · `Core = 24`** |

---

> # 🔴 **`G-03 = OPEN`**
> **"Authority source for complete 44-role `role_class` catalog has not yet been selected/approved."**

---

> ## 🛑 **توقف بعد تسليم `G-03 — ROLE_CLASS ASSIGNMENT DECISION MATRIX` — بانتظار Product Director.**

---

**نهاية `G-03 — ROLE_CLASS ASSIGNMENT DECISION MATRIX`**
