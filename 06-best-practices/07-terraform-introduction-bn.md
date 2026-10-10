---
video_url: "https://www.youtube.com/watch?v=zRcLgT7Qnio&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK&index=48"
code:
  - label: "Terraform infrastructure"
    path: code/infrastructure/main.tf
prev_url: 06-makefiles-bn.md
next_url: 08-terraform-modules-bn.md
---

# Terraform: পরিচিতি (Introduction)

**Infrastructure as Code (IaC)** ক্লাউড রিসোর্সগুলোকে ভার্সন-কন্ট্রোল করা ফাইলে কোড হিসেবে ডিফাইন করে। Terraform এই ডিক্লারেশনগুলোকে একটি এক্সিকিউশন প্ল্যানে রূপান্তর করে, যা AWS-এ কোনো পরিবর্তন কার্যকর করার আগেই পর্যালোচনা (review) করা যায়।

---

## ১. স্ট্রিম পাইপলাইন মডেলিং (Model the Stream Pipeline)

আমাদের উদাহরণ প্রজেক্টে স্ট্রিম-ভিত্তিক ride-prediction সার্ভিসের ক্লাউড ইনফ্রাস্ট্রাকচার প্রোভিশন করা হয়েছে:

- **Kinesis streams**: ইনপুট এবং আউটপুট ইভেন্টের জন্য।
- **Lambda serving function**: প্রেডিকশন হ্যান্ডলার হিসেবে।
- **S3 bucket**: মডেল আর্টিফ্যাক্ট (model artifacts) সংরক্ষণের জন্য।
- **ECR repository**: ডকার কন্টেইনার ইমেজ হোস্ট করার জন্য।

![The AWS stream-based ride-prediction architecture](AWS-stream-pipeline.png)

---

## ২. Terraform-এর মূল উপাদানসমূহ

- **Provider**: AWS API-র সাথে যোগাযোগ করার ব্রিজ।
- **Resources**: নির্দিষ্ট ক্লাউড অবজেক্ট ডিফাইন করে (যেমন S3 bucket, Lambda function)।
- **Variables**: পরিবেশ-নির্দিষ্ট (environment-specific) প্যারামিটার ডাইনামিক রাখার জন্য।
- **State**: বর্তমান ক্লাউডে ঠিক কী কী রিসোর্স ম্যানেজ করা হচ্ছে তার ট্র্যাকিং রেকর্ড।

![The Terraform project and its AWS resources](images/07-terraform-introduction-01-architecture.jpg)

---

## ৩. কমান্ড লাইফসাইকেল

১. `terraform init` দিয়ে প্রয়োজনীয় প্রোভাইডার প্লাগইন ইনিশিয়ালাইজ করুন।  
২. `terraform plan` চালিয়ে কী কী পরিবর্তন হতে যাচ্ছে তা পুঙ্খানুপুঙ্খভাবে রিভিউ করুন।  
৩. সবকিছু সঠিক থাকলে `terraform apply` দিয়ে পরিবর্তন ডিপ্লয় করুন।  
৪. প্র্যাকটিস বা টেস্টিং শেষে `terraform destroy` চালিয়ে রিসোর্স ডিলিট করুন, কারণ ক্লাউড রিসোর্সগুলো চালু থাকলে খরচ (charges) বৃদ্ধি পেতে পারে।
