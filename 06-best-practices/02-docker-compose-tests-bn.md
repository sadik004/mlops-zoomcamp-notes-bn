---
video_url: "https://www.youtube.com/watch?v=lBX0Gl7Z1ck&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Docker integration test"
    path: code/integration-test/test_docker.py
  - label: "Integration test Compose file"
    path: code/integration-test/docker-compose.yaml
prev_url: 01-pytest-bn.md
next_url: 03-localstack-bn.md
---

# ডকার কম্পোজ দিয়ে ইন্টিগ্রেশন টেস্টিং (Integration Tests with docker-compose)

ইউনিট টেস্ট শুধুমাত্র পাইথন ফাংশনগুলোকে আলাদাভাবে পরীক্ষা করে। কিন্তু একটি **ইন্টিগ্রেশন টেস্ট (Integration Test)** পুরো সার্ভিসটিকে ডকারে চালু করে, আসল HTTP রিকোয়েস্ট পাঠায় এবং সম্পূর্ণ প্রসেস বাউন্ডারির ওপার থেকে রেসপন্স সঠিক কি না তা নিশ্চিত করে।

---

## ১. টেস্টের আওতাধীন সার্ভিস চালু করা (Start the service under test)

`docker-compose.yaml` ফাইল কন্টেইনার ও তার এনভায়রনমেন্ট পরিচালনা করে। একটি টেস্ট ক্লায়েন্ট স্ক্রিপ্ট চলমান ডকার সার্ভিসে নমুনা ইভেন্ট পাঠায় এবং প্রত্যাশিত প্রেডিকশনের সাথে তুলনা করে:

![ইন্টিগ্রেশন টেস্ট কোড এবং সার্ভিসের রেসপন্স](images/02-docker-compose-tests-01-refactor.jpg)

টেস্ট ডেটাকে সবসময় নির্ধারিত ও অপরিবর্তনীয় (Deterministic) রাখুন। ফিক্সড ফিক্সচার ব্যবহার করলে যেকোনো ফেইলিওর সহজে ট্র্যাক করা যায়।

![ডকার-ভিত্তিক ইন্টিগ্রেশন টেস্ট রান হওয়ার দৃশ্য](images/02-docker-compose-tests-02-integration.jpg)

> [!IMPORTANT]
> **কেন ইন্টিগ্রেশন টেস্ট জরুরি:** ইউনিট টেস্ট পাস করলেই এটা প্রমাণিত হয় না যে ডকার কন্টেইনার আসলেই ঠিকমতো স্টার্ট হবে, ডিপেন্ডেন্সিগুলো ঠিক আছে, বা HTTP API নেটওয়ার্কে রেসপন্স দিচ্ছে।
