---
video_url: "https://www.youtube.com/watch?v=-c4iumyZMyw&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Grafana dashboard configuration"
    path: dashboards/data_drift.json
  - label: "Grafana provisioning"
    path: config/grafana_dashboards.yaml
prev_url: 07-data-quality-bn.md
next_url: 09-debugging-tests-reports-bn.md
---

# গ্রাফানা ড্যাশবোর্ড সেভ ও প্রভিশনিং (Save Grafana Dashboard)

হাতে তৈরি করা Grafana ড্যাশবোর্ড কন্টেইনার মুছে গেলে হারিয়ে যেতে পারে। Grafana-তে ড্যাশবোর্ডকে **JSON** ফরম্যাটে এক্সপোর্ট করে **Dashboard Provisioning** ফাইলের মাধ্যমে সংরক্ষণ করা হয়—যাতে কন্টেইনার রিস্টার্ট হলেও ড্যাশবোর্ড নিজে নিজেই লোড হয়ে যায়।

---

## ১. ড্যাশবোর্ড এক্সপোর্ট ও মাউন্ট করা

ড্যাশবোর্ডের সেটিংস থেকে JSON ফাইলটি ডাউনলোড করে `dashboards/data_drift.json`-এ সেভ করুন। এরপর `config/grafana_dashboards.yaml` ফাইলে প্রভিশনিং ডিরেক্টরি ডিফাইন করে ডকার ভলিউমে মাউন্ট করুন।

![সংরক্ষিত ড্যাশবোর্ডের জন্য Grafana কনফিগারেশন ফাইল](images/08-save-dashboard-01-config.jpg)

> **সতর্কতা:** ড্যাশবোর্ড JSON ফাইলে গ্রাফ ও কোয়েরি থাকে, কিন্তু কোনো পাসওয়ার্ড বা সিক্রেট থাকা উচিত নয়। ডাটাবেজ পাসওয়ার্ড সবসময় এনভায়রনমেন্ট ভ্যারিয়েবলে রাখবেন।

---

## ২. রিলোড ও ভেরিফিকেশন (Reload and verify)

ডকার কম্পোজ রিস্টার্ট দিয়ে Grafana ওপেন করুন:
- দেখুন অটোমেটিক ড্যাশবোর্ডটি লোড হয়েছে কি না।
- প্রিডিকশন ড্রিফট ট্রেন্ড, মিসিং ভ্যালু এবং ড্রিফটেড কলামের সংখ্যা ঠিকঠাক গ্রাফে দেখাচ্ছে কি না।

![সংরক্ষিত কনফিগারেশন থেকে রিলোড হওয়া ড্যাশবোর্ড](images/08-save-dashboard-02-dashboard.jpg)

![সংরক্ষিত ড্যাশবোর্ডের প্যানেলসমূহ](images/08-save-dashboard-03-panels.jpg)
