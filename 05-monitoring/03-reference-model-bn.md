---
video_url: "https://www.youtube.com/watch?v=IjNrkqMYQeQ&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Baseline model notebook"
    path: baseline_model_nyc_taxi_data.ipynb
prev_url: 02-monitoring-environment-bn.md
next_url: 04-evidently-metrics-bn.md
---

# রেফারেন্স ডেটা এবং বেসলাইন মডেল তৈরি (Prepare Reference and Model)

ডেটা ড্রিফট বা পারফরম্যান্স ড্রপ হিসাব করার আগে আমাদের একটি **রেফারেন্স ডেটাসেট (Reference Dataset)** এবং সেই ডেটাতে ট্রেইন্ড একটি বেসলাইন মডেল তৈরি করে নিতে হবে।

---

## ১. বেসলাইন তৈরি করা (Build the baseline)

NYC Taxi Parquet ডেটা ডাউনলোড করে নির্দিষ্ট ট্রেনিং পিরিয়ড নির্বাচন করুন। আগের মডিউলগুলোর মতো ফিচার ভেক্টরাইজ করে একটি সাধারণ Linear Regression মডেল ট্রেন করুন।

![বেসলাইনের জন্য হিস্টোরিক্যাল ডেটা ডাউনলোড করার দৃশ্য](images/03-reference-model-01-download.jpg)

ট্রেইন্ড মডেলটিকে `models/` ডিরেক্টরিতে এবং রেফারেন্স ডেটাকে `data/reference.parquet` হিসেবে সেভ করুন। রেফারেন্স ফাইলে ফিচার কলাম, টার্গেট এবং প্রেডিকশনের মান সংরক্ষিত থাকতে হবে।

![বেসলাইন মডেল ট্রেনিং ও সেভ করার স্ক্রিনশট](images/03-reference-model-02-baseline.jpg)

---

## ২. রেফারেন্স ডেটার মূল ভূমিকা (The role of the reference)

ভবিষ্যতে প্রতিদিন যে লাইভ নতুন ডেটা আসবে, Evidently সেই নতুন ব্যাচের সাথে এই `reference.parquet` ডেটাকে তুলনা করবে।
- এটি ইনপুট ফিচারের আসল ডিস্ট্রিবিউশন নির্ধারণ করে।
- ডেটা ড্রিফট, মিসিং ভ্যালু এবং প্রেডিকশন ড্রিফট পরিমাপ করার ভিত্তি হিসেবে কাজ করে।

![মনিটরিং তুলনার জন্য বর্তমান লাইভ ডেটা প্রস্তুত করার দৃশ্য](images/03-reference-model-03-current-data.jpg)

> [!NOTE]
> রেফারেন্স ডেটাকে চিরস্থায়ী ধ্রুবক ভাববেন না। যদি বাস্তব পরিস্থিতির বড় পরিবর্তন ঘটে এবং মডেলকে নতুন ডেটা দিয়ে রি-ট্রেন করা হয়, তবে একটি নতুন রেফারেন্স ফাইল বানিয়ে আগেরটিকে আপডেট করতে হবে।
