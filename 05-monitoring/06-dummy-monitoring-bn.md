---
video_url: "https://www.youtube.com/watch?v=s3G4PMsOMOA&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Dummy metric calculation"
    path: dummy_metrics_calculation.py
  - label: "Monitoring Compose stack"
    path: docker-compose.yml
prev_url: 05-evidently-dashboard-bn.md
next_url: 07-data-quality-bn.md
---

# ডামি মনিটরিং ও পাইপলাইন ভেরিফিকেশন (Dummy Monitoring)

আসল মডেল ও ডেটা যুক্ত করার আগে সম্পূর্ণ ইনফ্রাস্ট্রাকচার (PostgreSQL $\to$ Grafana) ঠিকঠাক কাজ করছে কি না তা নকল বা ডামি (Synthetic) মান তৈরি করে যাচাই করে নেওয়া বুদ্ধিমানের কাজ।

---

## ১. ডামি টেবিল তৈরি ও ডেটা ইনসার্ট

একটি ছোট স্ক্রিপ্ট তৈরি করে প্রতি কয়েক সেকেন্ড পর পর একটি করে র‍্যান্ডম সংখ্যা ও টাইমস্ট্যাম্প PostgreSQL-এর `dummy_metrics` টেবিলে ইনসার্ট করা হয়:

![ডামি মনিটরিং মান তৈরি করার স্ক্রিপ্ট](images/06-dummy-monitoring-01-script.jpg)

`psycopg` লাইব্রেরি ব্যবহার করে টেবিল তৈরি এবং ডাটাবেজ কানেকশন নিশ্চিত করুন।

![ডামি মেট্রিক্স স্ক্রিপ্টের জন্য ডাটাবেজ সেটআপ](images/06-dummy-monitoring-02-database.jpg)

---

## ২. ড্যাশবোর্ড লুপ পরীক্ষা (Check the dashboard loop)

স্ক্রিপ্টটি ব্যাকগ্রাউন্ডে চলতে দিন এবং Grafana-তে PostgreSQL ডেটা সোর্স কানেক্ট করে একটি লাইভ টাইম-সিরিজ প্যানেল বানান:
- দেখুন প্রতি সেকেন্ডে নতুন নতুন ডেটা পয়েন্ট স্বয়ংক্রিয়ভাবে গ্রাফে যুক্ত হচ্ছে কি না।

![মেট্রিক জেনারেশন লুপ চলার দৃশ্য](images/06-dummy-monitoring-03-loop.jpg)

একবার যখন নিশ্চিত হবেন যে এই পাইপলাইনটি নিখুঁত কাজ করছে, তখন শুধু ডামি সংখ্যার জায়গায় **Evidently-র আসল ডেটা ড্রিফট মেট্রিক্স** বসিয়ে দিলেই সম্পূর্ণ সিস্টেম লাইভ হয়ে যায়।
