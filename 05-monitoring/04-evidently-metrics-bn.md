---
video_url: "https://www.youtube.com/watch?v=kP3lzh_HfWY&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Evidently metric calculation"
    path: evidently_metrics_calculation.py
prev_url: 03-reference-model-bn.md
next_url: 05-evidently-dashboard-bn.md
---

# Evidently দিয়ে মেট্রিক্স হিসাব করা (Evidently Metrics Calculation)

**Evidently** রেফারেন্স ডেটাসেটের সাথে বর্তমান লাইভ ডেটাসেটের তুলনা করে একটি বিস্তৃত অ্যানালাইসিস রিপোর্ট তৈরি করে।

---

## ১. মেট্রিক্স নির্বাচন এবং কলাম ম্যাপিং (Column Mapping)

আমরা ৩টি গুরুত্বপূর্ণ বিষয় হিসাব করব:
1. **Prediction Drift:** মডেলের প্রেডিকশনে কোনো অস্বাভাবিক পরিবর্তন এসেছে কি না।
2. **Dataset Drift:** ইনপুট ফিচার কলামগুলোর ডিস্ট্রিবিউশন কতটা বদলেছে।
3. **Missing Values Share:** লাইভ ডেটায় কত শতাংশ মিসিং বা নাল ভ্যালু আছে।

Evidently যেন বুঝতে পারে কোন কলামটি নিউমেরিক্যাল আর কোনটি ক্যাটেগরিক্যাল, সেজন্য একটি `ColumnMapping` তৈরি করা বাধ্যতামূলক:

![নির্বাচিত মেট্রিক্স সহ Evidently রিপোর্টের দৃশ্য](images/04-evidently-metrics-01-report.jpg)

```python
from evidently.report import Report
from evidently.metric_preset import DataDriftPreset, DataQualityPreset

report = Report(metrics=[
    DataDriftPreset(),
    DataQualityPreset(),
])

report.run(
    reference_data=reference_data,
    current_data=current_data,
    column_mapping=column_mapping,
)
```

রিপোর্টটি HTML ফাইল হিসেবে সেভ করে ব্রাউজারে সুন্দর ইন্টারঅ্যাক্টিভ গ্রাফ দেখা যায়।

![একটি মনিটরিং ব্যাচ থেকে হিসাব করা মেট্রিক্সের মানসমূহ](images/04-evidently-metrics-02-metrics.jpg)

---

## ২. ফলাফল ডাটাবেজে সংরক্ষণ (Persist to PostgreSQL)

গ্রাফের পাশাপাশি এর ভেতরের গাণিতিক সংখ্যাগুলো বের করে **PostgreSQL** ডাটাবেজে টাইমস্ট্যাম্প সহ ইনসার্ট করা হয়। প্রতিদিন রাতে নতুন ব্যাচের জন্য এই স্ক্রিপ্টটি চলবে এবং ডাটাবেজে একটি করে নতুন রো যোগ করবে।

![Grafana-র জন্য প্রস্তুত মনিটরিং মেট্রিক্স](images/04-evidently-metrics-03-grafana.jpg)
