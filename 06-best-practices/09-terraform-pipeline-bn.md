---
video_url: "https://www.youtube.com/watch?v=JVydd1K6R7M&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK&index=50"
code:
  - label: "Terraform root configuration"
    path: code/infrastructure/main.tf
  - label: "Manual deployment script"
    path: code/scripts/deploy_manual.sh
prev_url: 08-terraform-modules-bn.md
next_url: 10-terraform-testing-bn.md
---

# এন্ড-টু-এন্ড রাইড প্রেডিকশন ওয়ার্কফ্লো নির্মাণ (Build an End-to-end Ride Prediction Workflow)

পুনর্ব্যবহারযোগ্য Kinesis মডিউল তৈরি করার পর, এবার রাইড-প্রেডিকশন পাইপলাইনের বাকি ইনফ্রাস্ট্রাকচার যুক্ত করার পালা। 
- **Terraform** রিসোর্স এবং তাদের মধ্যকার কানেকশনগুলো ডিক্লেয়ার করবে।
- **Deployment scripts** ডেটা ও মডেল রিলেটেড অপারেশনগুলো হ্যান্ডেল করবে যা সরাসরি Terraform রিসোর্স নয়।

---

## ১. AWS রিসোর্সসমূহ যুক্ত করা (Add the AWS Resources)

- **S3 Bucket**: মডেল আর্টিফ্যাক্ট সংরক্ষণ করতে।
- **ECR Repository**: ডকার কন্টেইনার ইমেজ রাখতে।
- **Lambda Function**: প্রেডিকশন রিকোয়েস্ট প্রসেস করতে।
- **Kinesis Streams**: পাইপলাইনের ইনপুট এবং আউটপুট ইভেন্ট আদান-প্রদান করতে।

রুট কনফিগারেশনে Terraform সংশ্লিষ্ট কম্পোনেন্টের নাম এবং ARN গুলো একসাথে যুক্ত করে দেয়।

![The pipeline resources in the Terraform project](images/09-terraform-pipeline-01-streams.jpg)

---

## ২. ডিপ্লয়মেন্ট প্রসেস (Deployment Process)

১. স্ট্যাজিং ভেরিয়েবল ফাইলের জন্য `terraform init` এবং `terraform apply` চালান।  
২. ইনফ্রাস্ট্রাকচার তৈরি হয়ে গেলে, ডিপ্লয়মেন্ট স্ক্রিপ্ট দিয়ে ডকার ইমেজ পাবলিশ করুন, মডেল আর্টিফ্যাক্ট S3-তে কপি করুন এবং Lambda এনভায়রনমেন্ট ভেরিয়েবল সেট করুন।

![Terraform initializing the infrastructure](images/09-terraform-pipeline-02-init.jpg)

---

## ৩. দায়িত্বের বিভাজন (Separation of Concerns)

ইনফ্রাস্ট্রাকচার ও অ্যাপ্লিকেশন ডিপ্লয়মেন্টকে সবসময় আলাদা রাখুন:
- **Terraform**: ইনফ্রাস্ট্রাকচার স্টেট ও ক্লাউড রিসোর্স ম্যানেজ করে।
- **Application Deployment**: ইমেজ ট্যাগ (image tags), মডেল রান আইডি (model run IDs) এবং টেস্ট ইভেন্ট ডেটা পরিচালনা করে।
