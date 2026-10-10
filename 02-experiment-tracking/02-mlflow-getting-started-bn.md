---
video_url: "https://www.youtube.com/watch?v=cESCQE9J3ZE&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "MLflow requirements"
    path: requirements.txt
  - label: "Duration prediction notebook"
    path: duration-prediction.ipynb
prev_url: 01-experiment-tracking-intro-bn.md
next_url: 03-experiment-tracking-bn.md
---

# MLflow শুরু করা ও সেটআপ (Getting Started with MLflow)

এই পাঠে আমরা MLflow ইনস্টল করব, লোকাল ড্যাশবোর্ড (UI) চালু করব এবং আমাদের ট্যাক্সি ডিউরেশন নোটবুকে প্রথম ট্র্যাকিং কোড যুক্ত করব।

---

## ১. এনভায়রনমেন্ট তৈরি করা (Create the environment)

অন্যান্য কাজের সাথে যেন প্যাকেজের সংঘর্ষ না হয়, সেজন্য একটি আলাদা ভার্চুয়াল এনভায়রনমেন্ট তৈরি করে প্রয়োজনীয় লাইব্রেরি ইনস্টল করুন:

```bash
conda create -n experiment-tracking python=3.9
conda activate experiment-tracking
pip install -r requirements.txt
```

![MLflow এনভায়রনমেন্ট এবং প্যাকেজ ইনস্টলেশনের স্ক্রিনশট](images/02-mlflow-getting-started-01-environment.jpg)

---

## ২. লোকাল MLflow UI চালু করা (Start the MLflow UI)

লোকালে মেটাডাটা সংরক্ষণ ও মডেল রেজিস্ট্রি সক্রিয় রাখতে আমরা **SQLite** ডাটাবেজ ব্যাকএন্ড হিসেবে ব্যবহার করব:

```bash
mlflow ui --backend-store-uri sqlite:///mlflow.db
```

কমান্ডটি রান করার পর টার্মিনালে একটি লোকাল লিংক আসবে (সাধারণত `http://127.0.0.1:5000`)। ব্রাউজারে লিংকটি ওপেন করলেই আপনি MLflow-এর দৃষ্টিনন্দন ড্যাশবোর্ড দেখতে পাবেন। SQLite ব্যাকএন্ড ব্যবহারের কারণে মডেল রেজিস্ট্রি (Model Registry) ট্যাবটিও স্বয়ংক্রিয়ভাবে সক্রিয় হয়ে যায়।

![লোকাল MLflow সার্ভার এবং ট্র্যাকিং UI](images/02-mlflow-getting-started-02-server.jpg)

---

## ৩. জুপিটার নোটবুকে MLflow কনফিগার করা (Configure the notebook)

আপনার পাইথন কোড যেন লোকাল SQLite ডাটাবেজে তথ্য পাঠাতে পারে, সেজন্য নোটবুকের শুরুতে ট্র্যাকিং URI এবং এক্সপেরিমেন্টের নাম নির্ধারণ করে দিন:

```python
import mlflow

# SQLite ডাটাবেজকে ট্র্যাকিং স্টোর হিসেবে সেট করা
mlflow.set_tracking_uri('sqlite:///mlflow.db')

# এক্সপেরিমেন্টের নাম সেট করা
mlflow.set_experiment('nyc-taxi-experiment')
```

যদি এই নামের কোনো এক্সপেরিমেন্ট আগে থেকে না থাকে, MLflow স্বয়ংক্রিয়ভাবে একটি নতুন এক্সপেরিমেন্ট তৈরি করে নেবে এবং পরবর্তী সকল রান এর আন্ডারে জমা করবে। 

![নোটবুকে MLflow এক্সপেরিমেন্ট কনফিগার করার দৃশ্য](images/02-mlflow-getting-started-03-experiment.jpg)
