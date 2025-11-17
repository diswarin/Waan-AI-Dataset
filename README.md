# 📄 เอกสารสร้างและรวบรวม Dataset  
**สำหรับทีมงานและทีมแพทย์ที่ร่วมวิจัย "Waan AI"**  
**ภาษาไทย** – **ใช้ได้ทันที** – **อัปเดตเวอร์ชัน 1.0** (2025-06-25)

> **ชุดข้อมูลภาษาไทยสำหรับ Fine-tune LLM ในโดเมนเบาหวาน CGM และอาหาร โดย WaanAI**  
> พร้อมคำแนะนำที่ถูกต้องและใช้พาณิชย์ได้ (Apache 2.0)  
> **Discord**: [https://discord.gg/QWkwyjT5](https://discord.gg/QWkwyjT5)

> **ภาษา**: Thai / English  
> **ใบอนุญาติ**: Apache 2.0 – Commercial use allowed  
> **Domain**: Diabetes + CGM + Food (Thai language)

📊 **[ดู Mind Map ของเอกสารนี้](./markmap.svg)**

---

## 📌 สารบัญ
1. [วัตถุประสงค์](#1-วัตถุประสงค์)
2. [ขอบเขตข้อมูล](#2-ขอบเขตข้อมูล)
3. [รูปแบบข้อมูล (Template)](#3-รูปแบบข้อมูล-template)
4. [ขั้นตอนรวบรวม](#4-ขั้นตอนรวบรวม)
5. [เครื่องมือที่ใช้](#5-เครื่องมือที่ใช้)
6. [คุณภาพข้อมูล](#6-คุณภาพข้อมูล-checklist)
7. [การเก็บรักษาและความปลอดภัย](#7-การเก็บรักษาและความปลอดภัย)
8. [ตัวอย่างข้อมูล](#8-ตัวอย่างข้อมูล-1-แถว)
9. [Timeline & KPI](#9-timeline--kpi)
10. [ช่องทางส่งข้อมูล](#10-ช่องทางส่งข้อมูล)

---

## 1. วัตถุประสงค์
- สร้าง **Dataset ภาษาไทย** สำหรับ **Fine-tune LLM** ในโดเมน **เบาหวาน + CGM + อาหาร**
- ให้ **คำแนะนำภาษาไทย** ที่ **ถูกต้อง + อธิบายได้ + พูดได้**
- **ใช้พาณิชย์ได้** (Apache 2.0) → ขาย SaaS ได้ทันที

---

## 2. ขอบเขตข้อมูล
| ประเภท | ตัวอย่าง | จำนวนเป้า |
|--------|----------|------------|
| **มื้ออาหาร** | ข้าวหน้าปลา, ลาบ, ทอดมัน | ≥ 1,000 มื้อ |
| **CGM data** | ค่าน้ำตาลก่อน/หลังมื้อ | ≥ 2,000 ค่า |
| **คำแนะนำ** | "ลดข้าว 1 ช้อน + เดิน 10 นาที" | ≥ 2,000 คำแนะนำ |
| **ภาษา** | **ภาษาไทย (อังกฤษเสริมได้)** | 100 % |
| **License** | **Apache 2.0 → ใช้พาณิชย์ได้** | 100 % |

---

## 3. รูปแบบข้อมูล (Template)
**ส่งเป็นไฟล์ JSONL** (1 แถว = 1 มื้อ)  
```json
{
  "meal_id": "20250625_1337",
  "user_id": "U0001",
  "meal_time": "13:37",
  "baseline_glucose_mg_dl": 85,
  "foods": [
    {
      "name": "ข้าวหน้าปลาอินทรีแดดเดียว",
      "weight_g": 120,
      "carb_g": 40,
      "protein_g": 25,
      "fat_g": 8,
      "kcal": 335
    }
  ],
  "cgm_readings": [
    {"min": 0, "glucose_mg_dl": 85},
    {"min": 60, "glucose_mg_dl": 148},
    {"min": 120, "glucose_mg_dl": 95}
  ],
  "recommendation": "ลดข้าว 1 ช้อนและเดิน 10 นาที",
  "source": "user_U0001_CGM",
  "consent": true
}
```

---

## 4. ขั้นตอนรวบรวม
### A. **ทีมแพทย์ / พยาบาล**
1. **Export CGM** → มื้อ + ค่าน้ำตาล (CSV)
2. **ถ่ายภาพอาหาร** → ส่งไฟล์รูป + ชั่งน้ำหนัก (g)
3. **กรอกแบบฟอร์ม** → Google Forms (link ด้านล่าง)

### B. **ทีมงานเทคนิค**
1. **ใช้ LogMeal API** → แปลงรูป → คาร์บ/โปรตีน/ไขมัน
2. **ใช้ script คัดกรอง** → ภาษาไทย + ความยาว + duplicate
3. **สร้าง JSONL** → upload → GitHub / GDrive

---

## 5. เครื่องมือที่ใช้
| เครื่องมือ | ใช้ทำ | ลิงก์/คำสั่ง |
|------------|--------|-------------|
| **Google Forms** | กรอกมื้อ + CGM | [forms.gle/waan-dataset](https://forms.gle/waan-dataset) |
| **LogMeal API** | แปลงรูป → โภชนา | [logmeal.com](https://logmeal.com) |
| **Google Drive** | เก็บไฟล์รูป | folder: `waan-ai/dataset/raw/` |
| **Hugging Face** | เก็บเวอร์ชัน | repo: `your-org/waan-dataset` |
| **Python script** | คัดกรอง | `scripts/clean_thai_diabetes.py` |

---

## 6. คุณภาพข้อมูล (Checklist)
✅ **ภาษาไทย ≥ 90 %**  
✅ **ความยาว 50-500 ตัวอักษร**  
✅ **ไม่ duplicate**  
✅ **มีคำเบาหวาน** (HbA1c, คาร์บ, glucose, มื้อ, เดิน)  
✅ **License ชัดเจน** (Apache 2.0)  
✅ **ไม่มี PII** (ชื่อ, เบอร์, รหัส) → ใช้ user_id แทน

---

## 7. การเก็บรักษาและความปลอดภัย
- **Anonymize** → ใช้ **user_id** แทนชื่อ/เบอร์
- **Encrypt at rest** → Google Drive **เข้าถึงได้เฉพาะทีมงาน**
- **Consent Form** → ให้ผู้ใช้กด "ยินยอม" ใน Google Forms
- **Right to be forgotten** → ลบข้อมูลได้ตลอด (contact ทีมงาน)

---

## 8. ตัวอย่างข้อมูล (1 แถว)
```json
{
  "meal_id": "20250625_1337",
  "user_id": "U0001",
  "meal_time": "13:37",
  "baseline_glucose_mg_dl": 85,
  "foods": [
    {
      "name": "ข้าวหน้าปลาอินทรีแดดเดียว",
      "weight_g": 120,
      "carb_g": 40,
      "protein_g": 25,
      "fat_g": 8,
      "kcal": 335
    }
  ],
  "cgm_readings": [
    {"min": 0, "glucose_mg_dl": 85},
    {"min": 60, "glucose_mg_dl": 148},
    {"min": 120, "glucose_mg_dl": 95}
  ],
  "recommendation": "ลดข้าว 1 ช้อนและเดิน 10 นาที",
  "source": "user_U0001_CGM",
  "consent": true
}
```

---

## 9. Timeline & KPI
| วัน | กิจกรรม | KPI |
|-----|----------|-----|
| **Day 1-3** | เก็บ data ทีมแพทย์ + ถ่ายรูป | **≥ 500 มื้อ** |
| **Day 4-5** | คัดกรอง + clean | **≥ 1,000 มื้อ** |
| **Day 6** | fine-tune + serve | **Model พร้อมใช้** |
| **Day 7** | เทส + ส่ง HF | **Dataset v1.0 พร้อมใช้** |

---

## 10. ช่องทางส่งข้อมูล
- **Google Drive**: [https://drive.google.com/drive/folders/waan-dataset](https://drive.google.com/drive/folders/waan-dataset)  
- **Hugging Face**: [https://huggingface.co/datasets/waan-ai/diabetes-th](https://huggingface.co/datasets/waan-ai/diabetes-th)  
- **Email**: [diswarin@mrdiswarin.com](mailto:diswarin@mrdiswarin.com)

---

## 📞 ติดต่อทีมงาน
- **Discord**: [https://discord.gg/QWkwyjT5](https://discord.gg/QWkwyjT5)  
- **Email**: diswarin@mrdiswarin.com (ทีมเทคนิค)  
- **Facebook**: [fb.com/waanai](https://fb.com/waanai)

---
---

# 📄 Dataset Collection Guide – Waan AI (Thai Diabetes)

> **Thai-language dataset for fine-tuning LLMs in diabetes, CGM, and food domains by WaanAI.**  
> Provides accurate, explainable recommendations. Apache 2.0 licensed for commercial use.  
> **Discord**: [https://discord.gg/QWkwyjT5](https://discord.gg/QWkwyjT5)

> **Language**: Thai / English  
> **License**: Apache 2.0 – Commercial use allowed  
> **Domain**: Diabetes + CGM + Food (Thai language)

📊 **[View Mind Map of this Document](./markmap.svg)**

---

## 📌 Table of Contents
1. [Purpose](#1-purpose)
2. [Data Scope](#2-data-scope)
3. [Data Format (Template)](#3-data-format-template)
4. [Collection Steps](#4-collection-steps)
5. [Tools Used](#5-tools-used)
6. [Data Quality Checklist](#6-data-quality-checklist)
7. [Storage & Security](#7-storage--security)
8. [Sample Record](#8-sample-record-1-row)
9. [Timeline & KPI](#9-timeline--kpi-1)
10. [Submission Channels](#10-submission-channels)

---

## 1. Purpose
- Build a **Thai-language dataset** for fine-tuning LLMs in the **diabetes + CGM + food** domain.
- Generate **Thai advice** that is **correct, explainable, and speakable**.
- **Apache 2.0 licensed** – ready for commercial SaaS.

---

## 2. Data Scope
| Type | Example | Target Count |
|------|---------|--------------|
| **Meals** | rice with fish, larb, tod-man | ≥ 1,000 meals |
| **CGM data** | glucose before/after meal | ≥ 2,000 values |
| **Advice** | "reduce 1 spoon of rice and walk 10 min" | ≥ 2,000 advices |
| **Language** | **Thai (English allowed as supplement)** | 100 % |
| **License** | **Apache 2.0 – commercial use allowed** | 100 % |

---

## 3. Data Format (Template)
**Submit as JSONL** (1 row = 1 meal)
```json
{
  "meal_id": "20250625_1337",
  "user_id": "U0001",
  "meal_time": "13:37",
  "baseline_glucose_mg_dl": 85,
  "foods": [
    {
      "name": "ข้าวหน้าปลาอินทรีแดดเดียว",
      "weight_g": 120,
      "carb_g": 40,
      "protein_g": 25,
      "fat_g": 8,
      "kcal": 335
    }
  ],
  "cgm_readings": [
    {"min": 0, "glucose_mg_dl": 85},
    {"min": 60, "glucose_mg_dl": 148},
    {"min": 120, "glucose_mg_dl": 95}
  ],
  "recommendation": "ลดข้าว 1 ช้อนและเดิน 10 นาที",
  "source": "user_U0001_CGM",
  "consent": true
}
```

---

## 4. Collection Steps
### A. Medical Team
1. Export **CGM data** (CSV) – meal time + glucose values  
2. Take **food photos** – send image + weight (g)  
3. Fill **Google Forms** (link below)

### B. Technical Team
1. Use **LogMeal API** → convert image → macro (carb/protein/fat)  
2. Run **cleaning script** → Thai language + length + duplicate  
3. Export **JSONL** → upload to GitHub / GDrive

---

## 5. Tools Used
| Tool | Purpose | Link / Command |
|------|---------|----------------|
| **Google Forms** | Collect meal + CGM | [forms.gle/waan-dataset](https://forms.gle/waan-dataset) |
| **LogMeal API** | Image → macro | [logmeal.com](https://logmeal.com) |
| **Google Drive** | Store raw images | folder: `waan-ai/dataset/raw/` |
| **Hugging Face** | Version control | repo: `your-org/waan-dataset` |
| **Python script** | Clean & filter | `scripts/clean_thai_diabetes.py` |

---

## 6. Data Quality Checklist
✅ **Thai language ≥ 90 %**  
✅ **Length 50-500 characters**  
✅ **No duplicate instruction**  
✅ **Contains diabetes keywords** (HbA1c, คาร์บ, glucose, มื้อ, เดิน)  
✅ **Clear license** (Apache 2.0)  
✅ **No PII** (use user_id instead of name/phone)

---

## 7. Storage & Security
- **Anonymize** → use **user_id** instead of real name/phone
- **Encrypt at rest** → Google Drive **access only team**
- **Consent Form** → user must click "I agree" in Google Forms
- **Right to be forgotten** → delete data on request (contact team)

---

## 8. Sample Record (1 row)
```json
{
  "meal_id": "20250625_1337",
  "user_id": "U0001",
  "meal_time": "13:37",
  "baseline_glucose_mg_dl": 85,
  "foods": [
    {
      "name": "ข้าวหน้าปลาอินทรีแดดเดียว",
      "weight_g": 120,
      "carb_g": 40,
      "protein_g": 25,
      "fat_g": 8,
      "kcal": 335
    }
  ],
  "cgm_readings": [
    {"min": 0, "glucose_mg_dl": 85},
    {"min": 60, "glucose_mg_dl": 148},
    {"min": 120, "glucose_mg_dl": 95}
  ],
  "recommendation": "ลดข้าว 1 ช้อนและเดิน 10 นาที",
  "source": "user_U0001_CGM",
  "consent": true
}
```

---

## 9. Timeline & KPI
| Day | Activity | KPI |
|-----|----------|-----|
| **Day 1-3** | Collect data (medical team + photos) | ≥ 500 meals |
| **Day 4-5** | Clean & filter | ≥ 1,000 meals |
| **Day 6** | Fine-tune + serve | Model ready |
| **Day 7** | Test + upload to HF | Dataset v1.0 ready |

---

## 10. Submission Channels
- **Google Drive**: [https://drive.google.com/drive/folders/waan-dataset](https://drive.google.com/drive/folders/waan-dataset)  
- **Hugging Face**: [https://huggingface.co/datasets/waan-ai/diabetes-th](https://huggingface.co/datasets/waan-ai/diabetes-th)  
- **Email**: [diswarin@mrdiswarin.com](mailto:diswarin@mrdiswarin.com)

---

## 📞 Contact Team
- **Discord**: [https://discord.gg/QWkwyjT5](https://discord.gg/QWkwyjT5)  
- **Email**: [diswarin@mrdiswarin.com](mailto:diswarin@mrdiswarin.com) (Technical Team)  
- **Facebook**: [fb.com/waanai](https://fb.com/waanai)

---

## 📝 License
This dataset is released under the **Apache 2.0 License** – free for commercial use.

---

**Version 1.0** | Updated: 2025-06-25
