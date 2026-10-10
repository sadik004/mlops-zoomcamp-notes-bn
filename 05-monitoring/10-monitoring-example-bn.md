---
code:
  - label: "Monitoring services"
    path: docker-compose.yml
  - label: "Evidently metric calculation"
    path: evidently_metrics_calculation.py
  - label: "Debugging notebook"
    path: debugging_nyc_taxi_data.ipynb
prev_url: 09-debugging-tests-reports-bn.md
next_url: ../06-best-practices/01-pytest.md
---

# সম্পূর্ণ মনিটরিং হ্যান্ডস-অন উদাহরণ (Monitoring Example)

লোকাল Docker Compose স্ট্যাক ব্যবহার করে পুরো মনিটরিং পাইপলাইন একসাথে চালু করার পূর্ণাঙ্গ গাইড:

---

## ১. পূর্বশর্ত ও বেসলাইন তৈরি
1. পাইথন এনভায়রনমেন্টে `requirements.txt` ইনস্টল করুন।
2. `baseline_model_nyc_taxi_data.ipynb` নোটবুকটি চালান। এটি ডেটা ডাউনলোড করবে, বেসলাইন মডেল ট্রেন করবে এবং `data/reference.parquet` ফাইল প্রস্তুত করবে।

---

## ২. সার্ভিস চালু করা
টার্মিনালে কমান্ড দিন:
```bash
docker compose up -d
```
এটি ব্যাকগ্রাউন্ডে PostgreSQL, Adminer এবং Grafana চালু করবে।

---

## ৩. সিমুলেটেড লাইভ ডেটা পাঠানো
টার্মিনালে মেট্রিক জেনারেশন স্ক্রিপ্টটি চালান:
```bash
python evidently_metrics_calculation.py
```
স্ক্রিপ্টটি প্রতিদিনের ডেটা স্লাইস নিয়ে Evidently দিয়ে মেট্রিক হিসাব করবে এবং নিয়মিত বিরতিতে PostgreSQL-এ রো ইনসার্ট করবে।

---

## ৪. লাইভ ড্যাশবোর্ড দেখা
ব্রাউজারে যান `http://localhost:3000`। ড্যাশবোর্ডে গিয়ে দেখতে পাবেন:
- Prediction Drift
- Missing Values
- Drifted Columns কাউন্টার

---

## ৫. সমস্যা ডিবাগ করা
ড্যাশবোর্ডে কোনো অস্বাভাবিক অ্যালার্ট দেখলে `debugging_nyc_taxi_data.ipynb` নোটবুকটি ওপেন করে বিস্তারিত টেস্ট স্যুট রান করুন এবং রুট কজ (Root Cause) বের করুন।

---

## ৬. সার্ভিস বন্ধ করা
কাজ শেষে কন্টেইনারগুলো বন্ধ করতে চালান:
```bash
docker compose down
```
