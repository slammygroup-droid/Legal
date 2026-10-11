# GOV-01 — Hash Registry

> ## ✅ **FINAL — بصمات مُحدَّثة بعد تنفيذ `ID-7` بتاريخ 2026-09-14**
>
> **اكتملت العمليات OP-4A · OP-1 · OP-2 · OP-3 · OP-4B، وتم التحقق الفعلي من شروط `PD-2a` الخمسة.**
> **هذا السجل هو مرجع التحقق المعتمد لبصمات نطاق `GOV-01` §5.**

| البند | القيمة |
|---|---|
| **السلطة المُنشِئة** | `GOV-01` *(السجل `43`)* · `GOV-01-A` *(السجل `50`)* — **M-4 / M-D1…M-D6** |
| **النطاق** | `GOV-01` §5 حصراً — **11 ملفاً** · ⛔ لا توسعة |
| **آلية التحديث** | **يدوية** مع كل تعديل معتمد — ⛔ لا Automation · لا CI · لا Hooks |
| **تاريخ تنفيذ `ID-7`** | **2026-09-14** *(`EXEC_DATE` — توقيت Asia/Aden · يقابله `2026-09-13T23:xx UTC` في بيئة التنفيذ)* |
| **الحالة** | ✅ **FINAL — OP-4B** |

## تعريف الحقول

- **`Last Updated`** = **تاريخ آخر تعديل فعلي لمحتوى الملف نفسه**، مستخرجاً من سلسلة القرارات المعتمدة *(`OI-2` — الخيار ①، السجل `54`)*.
  ⛔ **ليس تاريخ تنفيذ `ID-7`** · ⛔ **ولا `mtime`** *(ثبت عدم موثوقيته — بيان تشخيصي فقط)*.
- **`OPEN EVIDENCE GAP`** = تعذّر إثبات التاريخ بدليل موثَّق ⇒ **لا يُوضع تاريخ افتراضي**.

---

| File | SHA-256 | Classification | Last Updated | Validity Status | Triggering Decision/Report |
|---|---|---|---|---|---|
| `03-ERP-Functional-Foundation-v0.1.md` | `44316d6aba279a59a386be9053635c6a06e073037b435d6a28ef1a211cdfd297` | AUTHORITATIVE | 2026-09-04 | VALID | `GOV-01` |
| `04-Posting-Rule-Catalogue-v1.md` | `4ba3c19e948204d7236ec4acf576e019da79809363f22bd9ca5c2ead4fd77945` | AUTHORITATIVE | 🔴 OPEN EVIDENCE GAP | VALID | `GOV-01` |
| `05-Document-State-Machine-Catalogue-v1.md` | `6f9d3f8cd651b1112f20f90d0c79a68f88caa2138e307323b107191456b59782` | AUTHORITATIVE | 2026-09-12 | VALID | `GOV-01` · `PD-111` *(T1/T3/T4/T5)* |
| `06-Posting-Rule-Catalogue-v1.1-Revision.md` | `778684a0607b9511d03b15cf7b2c16d77d8dcc4d2b87384f3b9c6016489fb0a7` | AUTHORITATIVE | 2026-09-12 | VALID | `GOV-01` · `PD-109` *(A-4)* |
| `07-Document-State-Machine-Catalogue-v1.1-Revision.md` | `884ae2084e601a6a462d74a32d5706aecacfc71cf8de9a86aa379a2813ac8714` | AUTHORITATIVE | 🔴 OPEN EVIDENCE GAP | VALID | `GOV-01` |
| `08-Functional-Baseline-v1.1-PD-Approved.md` | `588ab450e157b051d6f7738c6343c8134aba6960cc421897f6bcac8c8ac8a70b` | AUTHORITATIVE | 2026-09-12 | VALID | `GOV-01` · `PD-109` |
| `09-Agent-2-Handoff-Brief.md` | `c893c8a2bc692afb1041fcc479259716e5fc7279f41111bf74ba3fd1610766d5` | BINDING INDEX | 2026-09-14 | VALID | `GOV-01` · `GOV-01-A` · `ID-7` / OP-2 |
| `29-PD-109-Final-Decision-Record.md` | `18db2a5c2b46927942ebb9b4fcfb1ca5c650b51680dd604d4318663623590a21` | AUTHORITATIVE | 2026-09-12 | VALID | `PD-109` |
| `36-PD-111-Final-Decision-Record.md` | `6ba2ca5c973711ad55de22e1f02d836510448834a17103b4fd044189207538d9` | AUTHORITATIVE | 2026-09-12 | VALID | `PD-111` |
| `ARCHIVED-ERP-Functional-Authority-Bundle-2026-09-14.md` | `4f6e31489327d7b74a1c9b4dce0ed5bf6869da7d31afb03b99aaa33e646a42c3` | ARCHIVED · DERIVED · NON-AUTHORITATIVE | 2026-09-14 | 🔴 INVALIDATED | `GOV-01` · `GOV-01-A` · `ID-7` / OP-3 |
| `رسالة-الإرسال-لوكيل-2.txt` | `615c363f34dbdcba1e9bee828d9fa757594044829b5abf4fb631231452b722d4` | DERIVED | 2026-09-14 | VALID | `GOV-01` · `GOV-01-A` · `ID-7` / OP-1 |

---

## ملاحظات

1. **`04` و`07`** — `OPEN EVIDENCE GAP` مُثبَت في السجل `54` §1.1: لا يحمل أيٌّ منهما أي تاريخ، والتاريخ الوحيد في رأسيهما هو **«تاريخ السريان»** *(مشروط بحدث لا تحرير)*. ⛔ **لا تخمين.**
2. **الأرشيف و`09` ورسالة الإرسال** — `Last Updated = 2026-09-14` **لأنها عُدِّلت فعلاً في ذلك التاريخ** ضمن OP-3/OP-2/OP-1 — لا لأن `ID-7` نُفِّذ فيه.
3. **خارج النطاق** — `01` · `16` · `43` · `50` **ليست في M-4 Scope** *(`M-D5`)* · `43` و`50` يُتحقَّق من بصمتيهما ضمن **Execution Integrity Verification** فقط.
4. ⚠ **`RR-2`:** سجل لا يُحدَّث **أسوأ من لا سجل**.
