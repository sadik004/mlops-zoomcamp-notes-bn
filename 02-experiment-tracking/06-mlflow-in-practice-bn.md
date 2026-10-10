---
video_url: "https://www.youtube.com/watch?v=1ykg4YmbFVA&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Scenario 1"
    path: running-mlflow-examples/scenario-1.ipynb
  - label: "Scenario 2"
    path: running-mlflow-examples/scenario-2.ipynb
  - label: "Scenario 3"
    path: running-mlflow-examples/scenario-3.ipynb
prev_url: 05-model-registry-bn.md
next_url: 07-mlflow-alternatives-bn.md
---

# বাস্তবে MLflow আর্কিটেকচার (MLflow in Practice)

MLflow কীভাবে সেটআপ করবেন তা নির্ভর করে টিমের সদস্য সংখ্যা, মডেলের সংখ্যা এবং কাজের পরিধির ওপর। বাস্তব কাজের ক্ষেত্রে মূলত ৩টি দৃশ্যপট (Scenarios) দেখা যায়:

---

## ১. সিনারিও ১: একক ডেভেলপার, সম্পূর্ণ লোকাল ট্র্যাকিং (Scenario 1)
- একজন ডেটা সায়েন্টিস্ট একা নিজের কম্পিউটারে কাজ করছেন।
- লোকাল MLflow UI এবং লোকাল ফোল্ডারে আর্টিফ্যাক্ট সংরক্ষণ করাই যথেষ্ট।
- কোনো বাড়তি ইনফ্রাস্ট্রাকচার বা ক্লাউড কনফিগারেশন লাগে না।

---

## ২. সিনারিও ২: একাধিক মডেল, লোকাল ডাটাবেজ ট্র্যাকিং (Scenario 2)
- একই ডেভেলপার একাধিক মডেল ও এক্সপেরিমেন্ট চালাচ্ছেন।
- লোকাল SQLite ডাটাবেজ ব্যাকএন্ড ব্যবহার করা হয় যাতে মডেল রেজিস্ট্রি সক্রিয় থাকে এবং সেরা মডেলটি নির্বাচন করা যায়।

![লোকাল এবং রিমোট MLflow আর্কিটেকচারের তুলনামূলক চিত্র](images/06-mlflow-in-practice-01-scenarios.jpg)

---

## ৩. সিনারিও ৩: শেয়ার্ড রিমোট ট্র্যাকিং (Scenario 3 - Enterprise Setup)
যখন একটি সম্পূর্ণ টিম একসাথে কাজ করে, তখন লোকাল পিসিতে ট্র্যাকিং সার্ভার রাখা যায় না। এর বদলে ক্লাউডে সেন্ট্রাল আর্কিটেকচার তৈরি করা হয়:
- **Compute (EC2):** একটি শেয়ার্ড EC2 ইনস্ট্যান্সে MLflow Tracking Server রান করে।
- **Backend Database (RDS PostgreSQL):** সকল মেটাডাটা, প্যারামিটার ও মেট্রিক্স একটি সেন্ট্রাল ডাটাবেজে জমা হয়।
- **Artifact Store (AWS S3 Bucket):** ভারী ট্রেইন্ড মডেল ফাইলগুলো সরাসরি S3 বালতিতে জমা হয়।

![AWS ক্লাউডে পরিচালিত রিমোট MLflow ট্র্যাকিং সার্ভার আর্কিটেকচার](images/06-mlflow-in-practice-02-remote-server.jpg)

যেকোনো ডেটা সায়েন্টিস্ট তার নিজস্ব ল্যাপটপ থেকে শুধু রিমোট সার্ভারের লিঙ্ক সেট করে এক্সপেরিমেন্ট চালাতে পারেন:

```python
import mlflow

# রিমোট ক্লাউড সার্ভারের ঠিকানা
mlflow.set_tracking_uri('http://<EC2_PUBLIC_DNS>:5000')
mlflow.set_experiment('nyc-taxi-experiment')
```

![রিমোট MLflow সার্ভারের সাথে যোগাযোগ করে রান লগ হওয়ার দৃশ্য](images/06-mlflow-in-practice-03-remote-run.jpg)

> [!WARNING]
> **ক্লাউড খরচ সংক্রান্ত সতর্কতা:**  
> রিমোট ক্লাউড সেটআপ ব্যবহারের পর অপ্রয়োজনীয় EC2 বা RDS ইন্সট্যান্সগুলো বন্ধ (Stop/Terminate) করে রাখবেন যাতে অনাকাঙ্ক্ষিত বিল না আসে।
