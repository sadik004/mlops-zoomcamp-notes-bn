---
video_url: "https://www.youtube.com/watch?v=D7wfMAdgdF8&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Flask web service"
    path: web-service/predict.py
prev_url: 01-deployment-modes-bn.md
next_url: 03-model-registry-serving-bn.md
---

# ওয়েব সার্ভিস: Flask এবং Docker দিয়ে মডেল ডিপ্লয়মেন্ট (Deploying Models with Flask and Docker)

প্রথম অনলাইন ডিপ্লয়মেন্টের জন্য আমরা একটি ছোট **Flask** ওয়েব সার্ভিস তৈরি করব। এটি ট্রেনিংয়ের সময় তৈরি হওয়া মডেল ফাইল লোড করবে, ইউজারের কাছ থেকে একটি ট্রিপের তথ্য গ্রহণ করবে এবং কত সময় লাগবে তা JSON আকারে রিটার্ন করবে।

---

## ১. মডেল আর্টিফ্যাক্ট লোড করা (Load the artifacts)

আমাদের ডিকশনারি ভেক্টরাইজার এবং লিনিয়ার রিগ্রেশন মডেলটি `.bin` বা `.pkl` ফাইল হিসেবে সংরক্ষিত থাকে।
> **গুরুত্বপূর্ণ নিয়ম:** মডেল ফাইলটি প্রতি রিকোয়েস্টে লোড না করে, সার্ভার যখন প্রথম স্টার্ট হয় তখনই গ্লোবালি একবার লোড করে মেমোরিতে রাখতে হয়। এতে প্রতি রিকোয়েস্ট খুব দ্রুত প্রসেস হয়।

![সার্ভিস কোড দ্বারা মডেল ফাইল লোড হওয়ার দৃশ্য](images/02-flask-docker-01-model-file.jpg)

সার্ভিসের একটি সুনির্দিষ্ট এন্ডপয়েন্ট থাকবে (যেমন: `/predict`)। ইনপুট হিসেবে আসবে ট্রিপের ডেটা এবং আউটপুটে আসবে প্রেডিক্টেড মিনিটের সংখ্যা।

---

## ২. প্রোডাকশন সার্ভারে সার্ভিস রান করা (Gunicorn)

ডেভেলপমেন্টের সময় সাধারণ `flask run` চললেও প্রোডাকশনের জন্য **Gunicorn**-এর মতো প্রোডাকশন-গ্রেড WSGI সার্ভার ব্যবহার করা হয়:

```bash
gunicorn --bind=0.0.0.0:9696 predict:app
```

টার্মিনাল থেকে বা পাইথন রিকোয়েস্ট দিয়ে পোর্ট `9696`-এ কল করে প্রেডিকশন পরীক্ষা করে নিন।

![Gunicorn সার্ভারের পেছনে লাইভ চলমান ওয়েব সার্ভিস](images/02-flask-docker-02-service.jpg)

---

## ৩. ডকার দিয়ে কন্টেইনারাইজ করা (Package it with Docker)

সার্ভিসটি যেন পৃথিবীর যেকোনো কম্পিউটারে হুবহু একভাবে কাজ করে, সেজন্য আমরা একটি `Dockerfile` তৈরি করি:

```dockerfile
FROM python:3.9-slim

WORKDIR /app

# ডিপেন্ডেন্সি ফাইল, স্ক্রিপ্ট এবং মডেল ফাইল কপি করা
COPY ["Pipfile", "Pipfile.lock", "predict.py", "lin_reg.bin", "./"]

# প্যাকেজ ইনস্টল করা
RUN pip install pipenv && pipenv install --system --deploy

# পোর্ট 9696-এ Gunicorn রান করা
CMD ["gunicorn", "--bind=0.0.0.0:9696", "predict:app"]
```

ডকার ইমেজ তৈরি ও রান করার কমান্ড:

```bash
# ইমেজ বিল্ড করা
docker build -t ride-duration-model .

# কন্টেইনার রান করা (পোর্ট 9696 ফরোয়ার্ড করে)
docker run --rm -p 9696:9696 ride-duration-model
```

![ডকার কন্টেইনার এবং এর রানটাইম ডিপেন্ডেন্সির চিত্র](images/02-flask-docker-03-container.jpg)
