---
video_url: "https://www.youtube.com/watch?v=OMwwZ0Z_cdk&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK&index=52"
code:
  - label: "Best-practices project code"
    path: code/README.md
prev_url: 10-terraform-testing-bn.md
next_url: 12-continuous-integration-bn.md
---

# CI/CD: পরিচিতি (Introduction)

**Continuous Integration (CI)** এবং **Continuous Delivery (CD)** কোড পরিবর্তন থেকে শুরু করে একটি টেস্টেড ও ডিপ্লয়ড সার্ভিসে রূপান্তরের প্রক্রিয়াকে সম্পূর্ণরূপে অটোমেট করে।
- **CI**: প্রতিটি কোড পরিবর্তন স্বয়ংক্রিয়ভাবে টেস্ট করে যাচাই করে।
- **CD**: অনুমোদিত ও ভ্যালিডেট করা কোড টার্গেট এনভায়রনমেন্টে ডিপ্লয় করে।

---

## ১. ওয়ার্কফ্লো ডিজাইন (Workflow Design)

কোর্সের পাইপলাইনে দুটি স্বতন্ত্র পর্যায় রয়েছে:
1. **Integration Workflow**: ইউনিট টেস্ট, ইন্টিগ্রেশন টেস্ট এবং `terraform plan` এক্সিকিউট করে।
2. **Delivery Workflow**: `terraform apply` চালায়, ডকার ইমেজ বিল্ড ও ECR-এ পুশ করে এবং Lambda সার্ভিস আপডেট করে।

![The complete CI/CD workflow for the ride-prediction service](ci_cd_zoomcamp.png)

---

## ২. গিটহাব অ্যাকশনস ওয়ার্কফ্লো কাঠামো

ওয়ার্কফ্লো ফাইলগুলো রিপোজিটরির `.github/workflows/` ডিরেক্টরিতে থাকে:
- **Pull Request**: পুল রিকোয়েস্ট ওপেন হলে স্বয়ংক্রিয়ভাবে CI চেক রান করে মূল ব্রাঞ্চকে সুরক্ষিত রাখে।
- **Controlled Push/Merge**: CI সফলভাবে পাস করার পর মার্জ বা পুশ ইভেন্টে স্বয়ংক্রিয়ভাবে ডেলিভারি পাইপলাইন ট্রিগার হয়।

![The CI/CD architecture in the project](images/11-cicd-introduction-02-repository.jpg)
