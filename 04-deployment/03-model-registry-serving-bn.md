---
video_url: "https://www.youtube.com/watch?v=aewOpHSCkqI&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "MLflow-backed web service"
    path: web-service-mlflow/predict.py
prev_url: 02-flask-docker-bn.md
next_url: 04-streaming-kinesis-lambda-bn.md
---

# ওয়েব সার্ভিস: মডেল রেজিস্ট্রি থেকে সরাসরি মডেল লোড করা (Getting Models from the Model Registry)

ডকার ইমেজের ভেতরে সরাসরি `.bin` বা `.pkl` মডেল ফাইল কপি করে ঢুকিয়ে দেওয়া প্রথম প্র্যাকটিসের জন্য ঠিক আছে, কিন্তু এটি একটি বড় ত্রুটি তৈরি করে—প্রতিবার মডেল বদলালে পুরো ডকার ইমেজ আবার নতুন করে বিল্ড করতে হয়। **মডেল রেজিস্ট্রি** সার্ভিস কোডকে মডেলের ফাইল থেকে আলাদা করে দেয়।

---

## ১. মডেল রেজিস্ট্রি থেকে মডেল নির্বাচন (Register and select a model)

ট্রেনিংয়ের সময় আমরা মডেলটিকে MLflow-তে রেজিস্টার করে একটি সুনির্দিষ্ট নাম দিই (যেমন: `duration-prediction`)। এরপর ওয়েব সার্ভিসটি ডকারে নতুন করে ফাইল কপি না করে সরাসরি MLflow-র মডেল রেজিস্ট্রি থেকে নির্দিষ্ট ভার্সন বা ট্যাগ (`@champion` বা `Production`) টেনে নিয়ে আসে।

![সার্ভিস কোড দ্বারা মডেল আর্টিফ্যাক্ট লোড হওয়ার দৃশ্য](images/03-registry-serving-01-registry.jpg)

ফিচার প্রিপারেশন লজিক একই থাকে, শুধু মডেল লোড করার জায়গাটিতে লোকাল ফাইলের পরিবর্তে **MLflow Model URI** ব্যবহার করা হয়:
যেমন: `models:/duration-prediction/Production` অথবা `models:/duration-prediction@champion`

![MLflow-ট্র্যাকড ট্রেনিং পাইপলাইনের দৃশ্য](images/03-registry-serving-02-model-code.jpg)

---

## ২. MLflow URI দিয়ে লোড ও প্রেডিকশন (Load through the MLflow URI)

সার্ভিস কোডে `mlflow.pyfunc.load_model()` দিয়ে মাত্র ২ লাইনে যেকোনো মডেল সরাসরি লোড করা যায়:

```python
import mlflow

# মডেল রেজিস্ট্রি URI থেকে মডেল নামানো
model_uri = "models:/duration-prediction/Production"
model = mlflow.pyfunc.load_model(model_uri)

# প্রেডিকশন তৈরি করা
prediction = model.predict(features)
```

![MLflow ডকুমেন্টেশনে মডেল URI এবং এর আর্টফ্যাক্ট লোকেশন](images/03-registry-serving-03-model-uri.jpg)

> [!TIP]
> **বেস্ট প্র্যাকটিস:**  
> ট্র্যাকিং URI এবং মডেলের নাম সবসময় এনভায়রনমেন্ট ভ্যারিয়েবলে (Environment variables) রাখুন। যদি নতুন কোনো ভার্সন রেজিস্ট্রি করা হয়, শুধু কনফিগারেশনে ভার্সন আপডেট করে দিলেই সার্ভিস স্বয়ংক্রিয়ভাবে নতুন মডেল ব্যবহার শুরু করে—ডকার ইমেজ পুনরায় বিল্ড করার দরকার হয় না।
