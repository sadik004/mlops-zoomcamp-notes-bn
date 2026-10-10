---
video_url: "https://www.youtube.com/watch?v=9yMO86SYvuI&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Kinesis integration test"
    path: code/integration-test/test_kinesis.py
  - label: "LocalStack Compose file"
    path: code/integration-test/docker-compose.yaml
prev_url: 02-docker-compose-tests-bn.md
next_url: 04-linting-formatting-bn.md
---

# LocalStack দিয়ে ক্লাউড সার্ভিসেস টেস্টিং (Testing Cloud Services with LocalStack)

বাস্তব ক্লাউডে প্রতিবার টেস্ট চালাতে গেলে সময় নষ্ট হয় এবং অনাকাঙ্ক্ষিত বিল আসার ঝুঁকি থাকে। **LocalStack** আপনার লোকাল কম্পিউটারে সম্পূর্ণ AWS ক্লাউডের একটি লোকাল এমুলেটর তৈরি করে—যাতে আসল AWS অ্যাকাউন্ট ছাড়াই Kinesis, S3 বা Lambda-র কোড ফ্রিতে টেস্ট করা যায়।

---

## ১. ক্লায়েন্টকে LocalStack-এর দিকে নির্দেশ করা

LocalStack-এর ডিফল্ট পোর্ট হলো `http://localhost:4566`। ডামি ক্রেডেনশিয়াল (`AWS_ACCESS_KEY_ID="test"`, `AWS_SECRET_ACCESS_KEY="test"`) ব্যবহার করে পাইথন কোড বা AWS CLI দিয়ে লোকাল স্ট্রিমে ডেটা পাঠানো যায়:

![LocalStack এবং Kinesis টেস্ট এনভায়রনমেন্ট](images/03-localstack-01-test-types.jpg)

টেস্টে প্রথমে একটি ডামি Kinesis স্ট্রিম তৈরি করা হয়, এরপর তাতে ইভেন্ট পুশ করা হয় এবং কনজিউমারের আউটপুট প্রেডিকশন ঠিক আছে কি না তা যাচাই করা হয়।

![একটি LocalStack কমান্ড এবং তার টেস্ট ফলাফল](images/03-localstack-02-results.jpg)

> [!TIP]
> LocalStack লোকাল ডেভেলপমেন্ট এবং দ্রুত টেস্ট চালানোর জন্য চমৎকার বিকল্প। তবে ফাইনাল প্রোডাকশনে যাওয়ার আগে আসল ক্লাউডে অন্তত একবার স্মোক টেস্ট করে নেওয়া ভালো।
