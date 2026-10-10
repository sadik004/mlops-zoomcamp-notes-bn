---
video_url: "https://www.youtube.com/watch?v=-6scXrFcPNk&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK&index=49"
code:
  - label: "Kinesis Terraform module"
    path: code/infrastructure/modules/kinesis/main.tf
  - label: "Terraform root module"
    path: code/infrastructure/main.tf
prev_url: 07-terraform-introduction-bn.md
next_url: 09-terraform-pipeline-bn.md
---

# Terraform: মডিউল ও আউটপুট ভেরিয়েবল (Modules and Output Variables)

Terraform মডিউল পুনরায় ব্যবহারযোগ্য (reusable) ইনফ্রাস্ট্রাকচার প্যাকেজ তৈরিতে ব্যবহৃত হয়। একটি মডিউল ভেতরে তৈরি করা জটিল রিসোর্সগুলোকে লুকিয়ে রেখে কেবল ইনপুট ও আউটপুট ইন্টারফেস এক্সপোজ করে।

---

## ১. Kinesis মডিউল তৈরি (Build a Kinesis Module)

এই কোর্সে Kinesis স্ট্রিম রিসোর্সগুলোকে একটি ডেডিকেটেড মডিউলে আলাদা করা হয়েছে:
- রুট কনফিগারেশন (`root configuration`) স্ট্রিমের নাম এবং অন্যান্য ভেরিয়েবল মডিউলে পাস করে।
- মডিউলের ভেতর স্ট্রিম তৈরি হওয়ার পর, Terraform আউটপুট স্ট্রিম আইডেন্টিফায়ার (ARN বা নাম) ব্যবহার করে Lambda এবং অন্যান্য ডাউনস্ট্রিম রিসোর্স কনফিগার করে।

![A reusable Terraform module in the project tree](images/08-terraform-modules-01-modules.jpg)

---

## ২. ব্ল্যাক-বক্স আর্কিটেকচার নীতি

মডিউলকে একটি সুনির্দিষ্ট ইন্টারফেসযুক্ত **ব্ল্যাক বক্স (black box)** হিসেবে গণ্য করুন:
- **Variables**: কলার (caller) কোন কোন মান কনফিগার করতে পারবে তা নির্ধারণ করে।
- **Outputs**: ডাউনস্ট্রিম রিসোর্সের জন্য শুধুমাত্র প্রয়োজনীয় মানগুলো এক্সপোজ করে।

![The Kinesis module resources](images/08-terraform-modules-02-kinesis.jpg)

---

## ৩. ভেরিফিকেশন ও রিইউজেবিলিটি

মডিউলে কোনো পরিবর্তন আনার পর `terraform plan` চালিয়ে যাচাই করুন Terraform কোন কোন রিসোর্স তৈরি (create), পরিবর্তন (update), বা মুছে ফেলতে (destroy) যাচ্ছে। আলাদা মডিউল আর্কিটেকচার থাকলে স্ট্যাজিং ও প্রোডাকশনে কোড ডুপ্লিকেট না করেই ইনফ্রাস্ট্রাকচার সহজে রিইউজ করা যায়।
