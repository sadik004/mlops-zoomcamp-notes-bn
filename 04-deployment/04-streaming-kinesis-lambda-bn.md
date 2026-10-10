---
video_url: "https://www.youtube.com/watch?v=TCqr9HNcrsI&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Kinesis and Lambda example"
    path: streaming/lambda_function.py
prev_url: 03-model-registry-serving-bn.md
next_url: 05-batch-scoring-bn.md
---

# স্ট্রিমিং ডিপ্লয়মেন্ট: AWS Kinesis এবং Lambda (Streaming Deployment)

স্ট্রিমিং ডিপ্লয়মেন্টে প্রতিটি ইভেন্ট আসার সাথে সাথেই রিয়েল-টাইমে স্কোরিং (প্রেডিকশন) করা হয়। এই পাঠে **Amazon Kinesis** মেসেজ স্ট্রিম হিসেবে এবং **AWS Lambda** সার্ভারলেস ফাংশন হিসেবে মডেলটি এক্সিকিউট করে।

---

## ১. ইভেন্ট ফ্লো ও ডেটা পাইপলাইন (Event flow)

একটি প্রডিউসার (Producer) সার্ভিস ট্রিপের তথ্য Kinesis স্ট্রিমে পুশ করে। Kinesis রেকর্ডগুলোকে ব্যাচ আকারে AWS Lambda ট্রিগারে পাঠায়:
1. Lambda ফাংশন এনকোডেড রেকর্ডটিকে ডিকোড করে JSON পার্স করে।
2. ইনপুট ফিচার প্রস্তুত করে মডেল লোড করে।
3. প্রেডিকশন আউটপুট তৈরি করে আউটপুট স্ট্রিমে পাঠায় বা লগ করে।

![ডিপ্লয়মেন্টে ব্যবহৃত ইভেন্ট স্ট্রিমের CloudWatch ভিউ](images/04-kinesis-lambda-01-stream.jpg)

---

## ২. কনজিউমার প্যাকেজিং ও পরিচালনা (Package and operate the consumer)

ল্যাম্বডা ডিপেন্ডেন্সি এবং মডেল লোড করার কোড একটি ডকার ইমেজ হিসেবে প্যাকেজ করে AWS ECR (Elastic Container Registry)-তে পুশ করা হয়। মডেল ফাইলটি যেন ক্লাউড S3 বা রেজিস্ট্রি থেকে ডাইনামিকালি নামতে পারে সে ব্যবস্থা রাখা হয়।

![Lambda কনজিউমারের জন্য কন্টেইনার ইমেজ কনফিগারেশন](images/04-kinesis-lambda-02-function.jpg)

টেস্ট ইভেন্ট পাঠিয়ে CloudWatch লগ চেক করে প্রেডিকশন যাচাই করা হয়।

![CloudWatch ইভেন্টস এবং প্রেডিকশন সার্ভিসের লগস](images/04-kinesis-lambda-03-events.jpg)

> [!WARNING]
> **ক্লাউড খরচ সংক্রান্ত নোট:**  
> Kinesis, Lambda এবং ECR ব্যবহার করলে ক্লাউডে বিল আসতে পারে, তাই প্র্যাকটিস শেষে অপ্রয়োজনীয় স্ট্রিম ও রিসোর্স ডিলিট করে দিন।
