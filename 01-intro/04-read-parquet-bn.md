---
video_url: "https://www.youtube.com/watch?v=r94QjpX9vSE&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Duration prediction notebook"
    path: duration-prediction.ipynb
prev_url: 03-aws-vm-bn.md
next_url: 05-train-duration-model-bn.md
---

# পারকেট (Parquet) ডেটা পড়া ও প্রসেসিং

মডেল ট্রেনিংয়ের জন্য ব্যবহৃত NYC Taxi ডেটাসেটটি আগে CSV ফরম্যাটে ছিল, তবে বর্তমানে এটি **Parquet** ফরম্যাটে রূপান্তরিত হয়েছে। Parquet ফাইল সাইজে অনেক ছোট হয় এবং প্রতিটি কলামের সঠিক ডেটা টাইপ (Schema) ধরে রাখে। তবে Pandas দিয়ে এই ফাইল পড়তে হলে একটি Parquet ইঞ্জিন ইনস্টল থাকা আবশ্যক।

---

## ১. ডেটা ফাইলগুলো ডাউনলোড করা (Download the files)

টার্মিনাল থেকে জানুয়ারি ও ফেব্রুয়ারি মাসের ডেটা ফাইল দুটি নামানোর কমান্ড:

```bash
wget https://d37ci6vzurychx.cloudfront.net/trip-data/yellow_tripdata_2021-01.parquet
wget https://d37ci6vzurychx.cloudfront.net/trip-data/yellow_tripdata_2021-02.parquet
```

![টার্মিনালে দুটি NYC Taxi Parquet ফাইল ডাউনলোড হওয়ার দৃশ্য](images/04-read-parquet-01-download.jpg)

---

## ২. পারকেট ইঞ্জিন ইনস্টল করা (Install a Parquet engine)

Pandas যেন Parquet ফাইল ডিকোড করতে পারে, সেজন্য `pyarrow` অথবা `fastparquet` প্যাকেজটি ইনস্টল থাকতে হবে।

জুপিটার নোটবুকের সেলে নিচের কমান্ডটি চালিয়ে `pyarrow` ইনস্টল করুন:

```python
!pip install pyarrow
```

যদি আপনার এনভায়রনমেন্টে `pyarrow` বা `fastparquet` ইনস্টল না থাকে, তবে `pandas.read_parquet` রান করার সময় এরর দেবে যে কোনো কার্যকর Parquet ইঞ্জিন খুঁজে পাওয়া যায়নি।

![Parquet ইঞ্জিন মিসিং সংক্রান্ত Pandas এররের স্ক্রিনশট](images/04-read-parquet-02-missing-engine.jpg)

---

## ৩. ডেটা রিড করা (Read the data)

CSV-এর মতো `read_csv` না লিখে সরাসরি `read_parquet` ব্যবহার করুন:

```python
import pandas as pd

df = pd.read_parquet('data/green_tripdata_2021-01.parquet')
```

**Parquet-এর সুবিধা:**  
পিকআপ এবং ড্রপ-অফের সময়গুলো Parquet ফাইলে আগে থেকেই আসল **Datetime** ফরম্যাটে সংরক্ষিত থাকে। তাই পুরনো CSV ফাইলের মতো আলাদা করে তারিখ/সময় টেক্সট থেকে পার্স (string parsing) করার কোনো বাড়তি ঝামেলা পোহাতে হয় না।

![নোটবুকে Parquet ডেটা পড়া এবং রাইড ডিউরেশন হিসাব করার স্ক্রিনশট](images/04-read-parquet-03-read-data.jpg)
