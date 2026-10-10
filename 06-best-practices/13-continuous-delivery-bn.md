---
video_url: "https://www.youtube.com/watch?v=jCNxqXCKh2s&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK&index=54"
code:
  - label: "Manual deployment steps"
    path: code/scripts/deploy_manual.sh
  - label: "Project deployment commands"
    path: code/README.md
prev_url: 12-continuous-integration-bn.md
---

# কন্টিনিউয়াস ডেলিভারি (Continuous Delivery)

**Continuous Delivery (CD)** ইন্টিগ্রেট করা কোড পরিবর্তনটিকে সরাসরি টার্গেট এনভায়রনমেন্টে স্বয়ংক্রিয়ভাবে ডিপ্লয় করে। এই প্রজেক্টে, CI ওয়ার্কফ্লো কোড অনুমোদন করার পর ডেভেলপমেন্ট ব্রাঞ্চে পুশ হলে এই ডেলিভারি পাইপলাইন ট্রিগার হয়।

---

## ১. ডেলিভারি জব তৈরি (Build the Delivery Job)

`.github/workflows/cd-deploy.yml` ফাইলের মাধ্যমে নিচের ধাপগুলো পরিচালিত হয়:
- `terraform plan` ও `terraform apply` চালিয়ে ক্লাউড ইনফ্রাস্ট্রাকচার আপডেট করা।
- নতুন কোড দিয়ে ডকার ইমেজ বিল্ড করা।
- ডকার ইমেজ ECR-এ পুশ করা।
- নতুন ইমেজ ট্যাগ দিয়ে Lambda ফাংশন আপডেট করা।

ওয়ার্কফ্লোতে সুস্পষ্ট এনভায়রনমেন্ট ভেরিয়েবল হিসেবে ইমেজ ট্যাগ, মডেল রান আইডি, ক্লাউড রিজিয়ন এবং স্ট্রিম নেমগুলো পাস করা হয়।

![The delivery workflow and deployment resources](images/13-continuous-delivery-01-trigger.jpg)

---

## ২. CI এবং CD-র দায়িত্বের বিভাজন

- **CI**: কোড মার্জ করা নিরাপদ কি না তা যাচাই করে।
- **CD**: সরাসরি ক্লাউড ইনফ্রাস্ট্রাকচার ও রানিং সার্ভিস পরিবর্তন করে।
- নিরাপত্তা বজায় রাখতে CD রান করার জন্য নির্দিষ্ট ব্রাঞ্চ রেস্ট্রিকশন এবং সীমিত এক্সেস পারমিশন নিশ্চিত করুন।

![The deployment job commands](images/13-continuous-delivery-02-deploy.jpg)

---

## ৩. পোস্ট-ডিপ্লয়মেন্ট ভেরিফিকেশন ও রোলব্যাক

ডিপ্লয়মেন্ট সম্পন্ন হওয়ার পর:
- পূর্ববর্তী ইউনিটে তৈরি করা এন্ড-টু-এন্ড টেস্ট চালিয়ে সার্ভিস যাচাই করুন।
- CloudWatch লগ পর্যবেক্ষণ করুন।
- যেকোনো অনাকাঙ্ক্ষিত পরিস্থিতিতে পূর্বাবস্থায় ফিরে যেতে Lambda ইমেজ এবং Terraform স্টেট উভয়ের জন্যই প্রস্তুত **রোলব্যাক প্ল্যান (rollback plan)** রাখুন।
