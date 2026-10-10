---
video_url: "https://www.youtube.com/watch?v=zjvYhDPzFlY&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Baseline model notebook"
    path: baseline_model_nyc_taxi_data.ipynb
  - label: "Grafana Compose stack"
    path: docker-compose.yml
prev_url: 04-evidently-metrics-bn.md
next_url: 06-dummy-monitoring-bn.md
---

# Evidently মনিটরিং ড্যাশবোর্ড (Evidently Monitoring Dashboard)

একটি একক HTML রিপোর্ট দিয়ে একবারের তুলনামূলক অবস্থা দেখা যায়, কিন্তু সময়ের সাথে সাথে (Time-series) কীভাবে পরিবর্তন হচ্ছে তা বোঝার জন্য একটি **মনিটরিং ড্যাশবোর্ড** প্রয়োজন।

---

## ১. প্রজেক্ট ও ওয়ার্কস্পেস তৈরি (Create a project and workspace)

Evidently-র নিজস্ব ড্যাশবোর্ড সার্ভিসের ভেতরে একটি প্রজেক্ট এবং ওয়ার্কস্পেস তৈরি করা হয়:
- ওয়ার্কস্পেসটি বিভিন্ন দিনের রিপোর্টের ইতিহাস জমা রাখে।
- ড্যাশবোর্ডে নির্দিষ্ট মেট্রিক্স (যেমন: কতগুলো কলামে ড্রিফট হয়েছে, মিসিং ভ্যালুর শতকরা হার) কার্ড ও গ্রাফ হিসেবে সাজানো থাকে।

![Evidently ড্যাশবোর্ড প্রজেক্ট তৈরি করার নোটবুক স্ক্রিনশট](images/05-evidently-dashboard-01-project.jpg)

রেফারেন্স এবং প্রতিদিনের কারেন্ট ব্যাচের রিপোর্ট ওয়ার্কস্পেসে নিয়মিত পুশ করা হয়।

![ওয়ার্কস্পেসে যুক্ত করা Evidently রিপোর্ট](images/05-evidently-dashboard-02-report.jpg)

---

## ২. কার্যকরী প্যানেলসমূহ বাছাই করা (Select useful panels)

ড্যাশবোর্ডে ৩ ধরনের মূল প্যানেল রাখা জরুরি:
1. **Trend Panel:** সময়ের সাথে মেট্রিক বাড়ছে নাকি কমছে তা রেখাচিত্র (line chart) আকারে দেখা।
2. **Counter Panel:** ঠিক এই মুহূর্তে মোট কতগুলো কলামে ডেটা ড্রিফট বিদ্যমান তার একটি বড় সংখ্যা।
3. **Data Quality Panel:** মিসিং বা ভুল ফরম্যাটের ডেটা হাইলাইট করে রাখা।

![Evidently ড্যাশবোর্ডে ডেটা কোয়ালিটি সম্পর্কিত তথ্য](images/05-evidently-dashboard-03-data-quality.jpg)

> **Evidently বনাম Grafana:** Evidently ডেটার ডিপ ডিস্ট্রিবিউশন তুলনা করতে সেরা, আর Grafana পুরো সিস্টেমের মেট্রিক্স ও অটোমেটিক স্ল্যাক অ্যালার্ট ফায়ার করার জন্য সেরা।
