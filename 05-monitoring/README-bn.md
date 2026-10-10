# মডিউল ৫: মডেল মনিটরিং (Module 5: Model Monitoring)

এই মডিউলে আমরা প্রোডাকশনে লাইভ ডিপ্লয় করা মডেল ও তার ইনপুট ডেটার স্বাস্থ্য পর্যবেক্ষণ (Monitoring) করা শিখব। কীভাবে **Evidently** দিয়ে ডেটা ড্রিফট ও কোয়ালিটি যাচাই করতে হয়, **PostgreSQL**-এ মেট্রিক্স স্টোর করতে হয় এবং **Grafana** দিয়ে লাইভ ড্যাশবোর্ড ও প্রভিশনিং করতে হয় তা বিস্তারিত আলোচনা করা হয়েছে।

---

## 📑 বাংলা পাঠ্যসূচি ও গাইডসমূহ:

| পাঠ | বিষয়বস্তু | বাংলা ফাইল |
| :---: | :--- | :--- |
| **৫.১** | **ML মনিটরিং পরিচিতি ও ৪টি মূল মেট্রিক গ্রুপ** | 📖 [01-ml-monitoring-bn.md](01-ml-monitoring-bn.md) |
| **৫.২** | **মনিটরিং এনভায়রনমেন্ট সেটআপ (Docker, Postgres, Grafana)** | 📖 [02-monitoring-environment-bn.md](02-monitoring-environment-bn.md) |
| **৫.৩** | **রেফারেন্স ডেটাসেট ও বেসলাইন মডেল তৈরি** | 📖 [03-reference-model-bn.md](03-reference-model-bn.md) |
| **৫.৪** | **Evidently দিয়ে ডেটা ড্রিফট ও কোয়ালিটি মেট্রিক্স হিসাব** | 📖 [04-evidently-metrics-bn.md](04-evidently-metrics-bn.md) |
| **৫.৫** | **Evidently মনিটরিং ড্যাশবোর্ড ও প্রজেক্ট** | 📖 [05-evidently-dashboard-bn.md](05-evidently-dashboard-bn.md) |
| **৫.৬** | **ডামি মেট্রিক্স দিয়ে পাইপলাইন ভেরিফিকেশন** | 📖 [06-dummy-monitoring-bn.md](06-dummy-monitoring-bn.md) |
| **৫.৭** | **ডেটা কোয়ালিটি মনিটরিং ও শিডিউলিং** | 📖 [07-data-quality-bn.md](07-data-quality-bn.md) |
| **৫.৮** | **Grafana ড্যাশবোর্ড সংরক্ষণ ও প্রভিশনিং (JSON)** | 📖 [08-save-grafana-dashboard-bn.md](08-save-grafana-dashboard-bn.md) |
| **৫.৯** | **টেস্ট স্যুট ও রিপোর্ট দিয়ে সমস্যা ডিবাগিং** | 📖 [09-debugging-tests-reports-bn.md](09-debugging-tests-reports-bn.md) |
| **৫.১০** | **সম্পূর্ণ মনিটরিং হ্যান্ডস-অন এন্ড-টু-এন্ড উদাহরণ** | 📖 [10-monitoring-example-bn.md](10-monitoring-example-bn.md) |
| **প্র্যাকটিস** | **মডিউল ৫ হোমওয়ার্ক প্রশ্ন ও গাইড** | 📝 [homework-bn.md](homework-bn.md) |

---

### মূল রিসোর্স:
- **ডকার কম্পোজ ফাইল:** [docker-compose.yml](docker-compose.yml)
- **মেট্রিক্স ক্যালকুলেশন স্ক্রিপ্ট:** [evidently_metrics_calculation.py](evidently_metrics_calculation.py)
- **ডামি স্ক্রিপ্ট:** [dummy_metrics_calculation.py](dummy_metrics_calculation.py)
- **ছবির ডিরেক্টরি:** [images ফোল্ডার](images/)
