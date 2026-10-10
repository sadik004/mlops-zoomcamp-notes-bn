---
video_url: "https://www.youtube.com/watch?v=sNSk3ojISh8&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Debugging notebook"
    path: debugging_nyc_taxi_data.ipynb
prev_url: 08-save-grafana-dashboard-bn.md
next_url: 10-monitoring-example-bn.md
---

# টেস্ট স্যুট এবং রিপোর্ট দিয়ে ডিবাগিং (Debugging with Test Suites and Reports)

মনিটরিং ড্যাশবোর্ড কেবল আমাদের জানায় যে কোনো পরিবর্তন বা সমস্যা ঘটেছে। কিন্তু **সমস্যাটি ঠিক কোথায় এবং কেন ঘটেছে**—তা বের করার জন্য Evidently-র **Test Suites** এবং বিস্তারিত রিপোর্ট দিয়ে ডিবাগিং করা হয়।

---

## ১. ড্যাশবোর্ড অ্যালার্ট থেকে তদন্ত শুরু

কোন মেট্রিকটি অ্যালার্ট ট্রিগার করেছে তা আগে চিহ্নিত করুন:
- প্রেডিকশন ড্রিফট?
- নির্দিষ্ট কোনো ইনপুট কলামের ড্রিফট?
- নাকি প্রচুর মিসিং ভ্যালু এসেছে?

![ডিবাগিং নোটবুক এবং Grafana ড্যাশবোর্ডের যৌথ দৃশ্য](images/09-debugging-01-suite.jpg)

---

## ২. টেস্ট স্যুট রান করা (Run an Evidently Test Suite)

Evidently Test Suites কোনো ধারণার ওপর নয়, বরং সরাসরি **PASS** অথবা **FAIL** রেজাল্ট দেয়:
- টেস্ট স্যুটে সুনির্দিষ্ট শর্ত থাকে (যেমন: "PULocationID-এর ড্রিফট p-value অবশ্যই ০.০৫-এর বেশি হতে হবে")।
- রেফারেন্স ডেটা এবং বর্তমান ফেইল করা ব্যাচের ওপর টেস্ট স্যুটটি রান করুন।

![ডিবাগিং ওয়ার্কফ্লোতে একক টেস্টগুলোর দৃশ্য](images/09-debugging-02-tests.jpg)

টেস্ট ফেল করলে রিপোর্ট থেকে সরাসরি দেখা যায় কোন নির্দিষ্ট কলামটির কারণে টেস্ট ফেইল করেছে। এরপর সেই ব্যাচের র ডেটা এবং প্রিপ্রসেসিং কোড পরীক্ষা করে বাগ ফিক্স করা যায়।

![টেস্ট রেজাল্ট সম্বলিত ডিবাগিং রিপোর্ট](images/09-debugging-03-report.jpg)
