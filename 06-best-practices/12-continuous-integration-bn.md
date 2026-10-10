---
video_url: "https://www.youtube.com/watch?v=xkTWF9c33mU&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK&index=53"
code:
  - label: "Project quality commands"
    path: code/Makefile
  - label: "Project configuration"
    path: code/pyproject.toml
prev_url: 11-cicd-introduction-bn.md
next_url: 13-continuous-delivery-bn.md
---

# কন্টিনিউয়াস ইন্টিগ্রেশন (Continuous Integration)

**Continuous Integration (CI)** প্রস্তাবিত প্রতিটি কোড পরিবর্তনের জন্য প্রজেক্টের সমস্ত কোয়ালিটি চেক স্বয়ংক্রিয়ভাবে এক্সিকিউট করে। লোকাল মেশিনের কোয়ালিটি গেটটি ক্লাউডের একটি পরিচ্ছন্ন GitHub Actions রানারে পুনরাবৃত্তি (reproduce) করা এর মূল লক্ষ্য।

---

## ১. CI ওয়ার্কফ্লো ডিফাইন করা (Define the CI Workflow)

`.github/workflows/ci-tests.yml` ফাইল তৈরি করুন যাতে নিচের জবগুলো অন্তর্ভুক্ত থাকে:
- **Environment Setup**: পাইথন ভার্সন এবং ডিপেন্ডেন্সি ইনস্টলেশন।
- **Unit Tests**: দ্রুতগতির লজিক্যাল টেস্ট রান করা।
- **Integration Tests**: ডকার বা লোকালস্ট্যাক দিয়ে সার্ভিস ইন্টিগ্রেশন যাচাই।
- **Terraform Plan**: ইনফ্রাস্ট্রাকচারে কী পরিবর্তন ঘটবে তা দেখা।

ডেভেলপমেন্ট ব্রাঞ্চের পুল রিকোয়েস্টে এই ওয়ার্কফ্লো ট্রিগার করুন, যাতে কোড মার্জ করার আগেই টিম রিভিউয়াররা টেস্ট রেজাল্ট দেখতে পারেন।

![The GitHub Actions workflow files](images/12-continuous-integration-01-workflows.jpg)

---

## ২. বেস্ট প্র্যাকটিস ও আইসোলেশন

- ওয়ার্কফ্লো ফাইলে সরাসরি জটিল কমান্ড না লিখে প্রজেক্টের `Makefile` টার্গেট ব্যবহার করুন।
- সিক্রেট ও ক্রিডেনশিয়াল রিপোজিটরির বাইরে রাখুন। যেসব ইন্টিগ্রেশন টেস্টে আসল AWS রিসোর্সের প্রয়োজন নেই, সেগুলোতে **LocalStack** ব্যবহার করুন।

![The CI test steps in the repository](images/12-continuous-integration-02-tests.jpg)

---

## ৩. ডিবাগিং ও লগিং

কোনো চেক ফেইল করলে যেন বিস্তারিত লগ পাওয়া যায় তা নিশ্চিত করুন—যাতে সহজেই শনাক্ত করা যায় সমস্যাটি পাইথন ডিপেন্ডেন্সি, টেস্ট কোড, ডকার বা Terraform কনফিগারেশন কোথা থেকে সৃষ্টি হয়েছে।
