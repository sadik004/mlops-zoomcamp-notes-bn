# মডিউল ১: সম্পূর্ণ মাস্টার গাইড ও ইঞ্জিনিয়ারিং হ্যান্ডবুক (Module 1 Master Codex)

> **ডকুমেন্ট উদ্দেশ্য**: এই হ্যান্ডবুকটি কোনো সংক্ষিপ্ত সামারি নয়। এটি MLOps Zoomcamp-এর মডিউল ১-এর প্রতিটি লেকচার, প্রতিটি কোড লাইন, গাণিতিক যুক্তি, আর্কিটেকচারাল সিদ্ধান্ত এবং প্রোডাকশন পিটফলগুলোর একটি **পূর্ণাঙ্গ ইঞ্জিনিয়ারিং হ্যান্ডবুক**। প্রতিটি কোড ব্লকের সাথে তার বিস্তারিত পেছনের কারণ (**"কোড কেন এভাবে লেখা হলো"**) বিশদভাবে ব্যাখ্যা করা হয়েছে।

---

## সূচিপত্র (Table of Contents)
1. [অধ্যায় ১: MLOps-এর মূল দর্শন ও বিজনেস কনটেক্সট](#অধ্যায়-১-mlops-এর-মূল-দর্শন-ও-বিজনেস-কনটেক্সট)
   - ১.১ প্রচলিত সফটওয়্যার ইঞ্জিনিয়ারিং বনাম MLOps (Code + Data + Model)
   - ১.২ বিজনেস সমস্যা: নিউ ইয়র্ক ট্যাক্সি রাইড ডিউরেশন প্রেডিকশন
   - ১.৩ মেশিন লার্নিং লাইফসাইকেল: Design, Train, Operate
2. [অধ্যায় ২: ডেভেলপমেন্ট ইনফ্রাস্ট্রাকচার ও এনভায়রনমেন্ট আর্কিটেকচার](#অধ্যায়-২-ডেভেলপমেন্ট-ইনফ্রাস্ট্রাকচার-ও-এনভায়রনমেন্ট-আর্কিটেকচার)
   - ২.১ কেন লোকাল ওএস পরিহার করে লিনাক্স কন্টেইনার/ক্লাউড জরুরি?
   - ২.২ GitHub Codespaces এনভায়রনমেন্ট কনফিগারেশন
   - ২.৩ AWS EC2 ভার্চুয়াল মেশিন, SSH সিকিউরিটি ও ডকার ডিমেন সেটআপ
3. [অধ্যায় ৩: ডেটা ইনজেশন ও স্টোরেজ অপটিমাইজেশন (Parquet বনাম CSV)](#অধ্যায়-৩-ডেটা-ইনজেশন-ও-স্টোরেজ-অপটিমাইজেশন-parquet-বনাম-csv)
   - ৩.১ NYC TLC ডেটাসেটের গঠন ও কলাম পরিচিতি
   - ৩.২ কেন CSV বাদ দিয়ে Parquet ফরম্যাট ব্যবহার করা হলো? (ইঞ্জিনিয়ারিং কারণ)
   - ৩.৩ PyArrow / fastparquet ইঞ্জিনের ভূমিকা
4. [অধ্যায় ৪: ডেটা ক্লিনিং ও ফিচার ইঞ্জিনিয়ারিং — লাইন-বাই-লাইন "কোড কেন লেখা হলো"](#অধ্যায়-৪-ডেটা-ক্লিনিং-ও-ফিচার-ইঞ্জিনিয়ারিং--লাইন-বাই-লাইন-কোড-কেন-লেখা-হলো)
   - ৪.১ টার্গেট ভেরিয়েবল ক্যালকুলেশন (`duration`)
   - ৪.২ আউটলায়ার ফিল্টারিং (১ থেকে ৬০ মিনিট): গাণিতিক ও ব্যবসায়িক কারণ
   - ৪.৩ ক্যাটাগরিক্যাল ভেরিয়েবল টাইপ কাস্টিং (`astype(str)`)
   - ৪.৪ ফিচার ক্রসিং (Feature Interaction / Route Encoding)
5. [অধ্যায় ৫: ভেক্টরাইজেশন ও স্পার্স ম্যাট্রিক্স আর্কিটেকচার](#অধ্যায়-৫-ভেক্টরাইজেশন-ও-স্পার্স-ম্যাট্রিক্স-আর্কিটেকচার)
   - ৫.১ কেন `pd.get_dummies` বাদ দিয়ে `DictVectorizer` ব্যবহার করা হলো?
   - ৫.২ মেমরি আর্কিটেকচার: SciPy CSR Sparse Matrix
   - ৫.৩ `fit_transform` বনাম `transform`: ডেটা লিকেজ প্রতিরোধের বাঁধন
6. [অধ্যায় ৬: অ্যালগরিদম ম্যাথমেটিক্স, বেসলাইন মডেল ও রেগুলারাইজেশন](#অধ্যায়-৬-অ্যালগরিদম-ম্যাথমেটিক্স-বেসলাইন-মডেল-ও-রেগুলারাইজেশন)
   - ৬.১ Ordinary Least Squares (OLS) লিনিয়ার রিগ্রেশন
   - ৬.২ ইভ্যালুয়েশন মেট্রিক: Root Mean Squared Error (RMSE)
   - ৬.৩ রেগুলারাইজেশন: কেন Lasso (L1) এবং Ridge (L2) প্রয়োজন?
7. [অধ্যায় ৭: মডেল ডায়াগনস্টিকস ও রেসিডুয়াল বিশ্লেষণ](#অধ্যায়-৭-মডেল-ডায়াগনস্টিকস-ও-রেসিডুয়াল-বিশ্লেষণ)
   - ৭.১ এরর ডিস্ট্রিবিউশন প্লট (Prediction vs Actual)
   - ৭.২ আন্ডার-এস্টিমেশন সমস্যা ও মডেলের সীমাবদ্ধতা
8. [অধ্যায় ৮: মডেল সিরিয়ালাইজেশন ও প্রোডাকশন আর্টিফ্যাক্ট সেভিং](#অধ্যায়-৮-মডেল-সিরিয়ালাইজেশন-ও-প্রোডাকশন-আর্টিফ্যাক্ট-সেভিং)
   - ৮.১ কেন `pickle.dump((dv, lr), f)`-এ ভেক্টরাইজার ও মডেল একসাথে সেভ করা হলো?
   - ৮.২ প্রোডাকশনে পাইপলাইন মিসম্যাচ দূরীকরণের কৌশল
9. [অধ্যায় ৯: জুপিটার নোটবুক থেকে মডুলার কোড পাইপলাইনে রূপান্তর](#অধ্যায়-৯-জুপিটার-নোটবুক-থেকে-মডুলার-কোড-পাইপলাইনে-রূপান্তর)
   - ৯.১ জুপিটার নোটবুকের লুকানো বিপদ (Hidden State Bug)
   - ৯.২ রিইউজেবল মডুলার পাইথন স্ক্রিপ্ট আর্কিটেকচার
10. [অধ্যায় ১০: MLOps ম্যাচিউরিটি মডেল (Level 0 থেকে Level 2)](#অধ্যায়-১০-mlops-ম্যাচিউরিটি-মডেল-level-0-থেকে-level-2)
11. [অধ্যায় ১১: মডিউল ১ হোমওয়ার্কের পুঙ্খানুপুঙ্খ সমাধান ও গাণিতিক বিশ্লেষণ](#অধ্যায়-১১-মডিউল-১-হোমওয়ার্কের-পুঙ্খানুপুঙ্খ- সমাধান-ও-গাণিতিক-বিশ্লেষণ)
12. [অধ্যায় ১২: সম্পূর্ণ এক্সিকিউটেবল প্রোডাকশন পাইথন কোড](#অধ্যায়-১২-সম্পূর্ণ-এক্সিকিউটেবল-প্রোডাকশন-পাইথন-কোড)

---

## অধ্যায় ১: MLOps-এর মূল দর্শন ও বিজনেস কনটেক্সট

### ১.১ প্রচলিত সফটওয়্যার ইঞ্জিনিয়ারিং বনাম MLOps
চিরাচরিত সফটওয়্যার সিস্টেমে:
$$\text{Input Data} + \text{Code (Business Rules)} = \text{Output}$$
এখানে কোড ডিটারমিনিস্টিক। একই ইনপুটের জন্য সবসময় একই আউটপুট পাওয়া যায়। একবার ইউনিট টেস্ট পাস করলে এবং কোড ডিপ্লয় হলে সাধারণত কোড নিজে নিজে পরিবর্তিত হয় না।

কিন্তু মেশিন লার্নিং সিস্টেমে:
$$\text{Input Data} + \text{Output} = \text{Model (Learned Rules)}$$
এবং রানটাইমে:
$$\text{New Data} \times \text{Model} = \text{Prediction}$$

এখানে ৩টি চলমান চলক রয়েছে:
1. **Code**: পাইপলাইন লজিক, স্কলার্ন মডেল, স্ক্রিপ্ট।
2. **Data**: প্রতিনিয়ত পরিবর্তনশীল রিয়েল-ওয়ার্ল্ড ডেটা।
3. **Model**: ডেটা এবং কোডের ইন্টারঅ্যাকশনে তৈরি হওয়া আর্টিফ্যাক্ট।

![The Taxi Trip Prediction Problem](images/01-introduction-01-taxi-trip.jpg)

#### কেন MLOps দরকার?
- **Data Drift**: মডেল ট্রেইনিংয়ের সময়ের ডেটার ডিস্ট্রিবিউশন প্রোডাকশনে বদলে যায়। (যেমন: নতুন রাস্তা তৈরি হওয়া, আবহাওয়া খারাপ হওয়া)।
- **Concept Drift**: ইনপুট এবং আউটপুটের মধ্যকার সম্পর্ক বদলে যায়। (যেমন: মূল্যস্ফীতির কারণে একই দূরত্বের ভাড়া বা ট্রাফিকের সময়ের সম্পর্ক পরিবর্তন)।
- **The "It worked on my notebook" Syndrome**: একজন ডেটা সায়েন্টিস্টের জুপিটার নোটবুকে একটি সেল এক্সিকিউট করে ৯৫% অ্যাকুরেসি পাওয়া খুবই সাধারণ। কিন্তু সেই মডেলটি যখন প্রতি সেকেন্ডে ৫০০টি রিয়েল-টাইম রিকোয়েস্ট হ্যান্ডেল করতে যায়, তখন ফিচার ট্রান্সফরমেশন মিসম্যাচ, মেমরি লিক এবং ডিপেন্ডেন্সি সমস্যার কারণে সিস্টেম ক্র্যাশ করে।

---

### ১.২ বিজনেস সমস্যা: নিউ ইয়র্ক ট্যাক্সি রাইড ডিউরেশন প্রেডিকশন
আমরা নিউ ইয়র্ক সিটির ট্যাক্সি ও লিমুজিন কমিশন (TLC)-এর ডেটাসেট নিয়ে কাজ করছি।
- **ব্যবসায়িক লক্ষ্য**: একজন যাত্রী ট্যাক্সিতে ওঠার মুহূর্তে (Pickup) আমাদের নিখুঁতভাবে প্রেডিক্ট করতে হবে গন্তব্যে পৌঁছাতে তার আনুমানিক **কত মিনিট (duration)** লাগবে।
- **কেন এটি গুরুত্বপূর্ণ?**
  - যাত্রী সঠিক আনুমানিক সময় (ETA) দেখতে পাবেন, যা সার্ভিসের বিশ্বস্ততা বাড়ায়।
  - ট্যাক্সি কোম্পানিগুলো ডায়নামিক প্রাইসিং ও ড্রাইভারদের শিডিউলিং সঠিকভাবে নির্ধারণ করতে পারবে।
  - যদি মডেল বাস্তব সময়ের চেয়ে অনেক কম সময় প্রেডিক্ট করে, তবে যাত্রী অসন্তুষ্ট হবেন। আর অনেক বেশি প্রেডিক্ট করলে যাত্রী রাইড বুক না করে চলে যাবেন।

---

### ১.৩ মেশিন লার্নিং লাইফসাইকেল: Design, Train, Operate

MLOps কোনো একক টুল নয়; এটি একটি চলমান ৩-পর্যায়ের সাইকেল:

```
┌────────────────────────────────────────────────────────┐
│                   1. DESIGN PHASE                      │
│   - Identify business problem & success metrics        │
│   - Check data availability & legal compliance         │
│   - Architectural decisions (Batch vs Streaming)       │
└──────────────────────────┬─────────────────────────────┘
                           │
                           ▼
┌────────────────────────────────────────────────────────┐
│                   2. TRAIN PHASE                       │
│   - Data Extraction, Validation & Cleaning             │
│   - Feature Engineering & Model Experimentation        │
│   - Model Evaluation against Baseline                  │
│   - Model Packaging & Versioning                       │
└──────────────────────────┬─────────────────────────────┘
                           │
                           ▼
┌────────────────────────────────────────────────────────┐
│                   3. OPERATE PHASE                     │
│   - CI/CD Deployment to Production                     │
│   - Real-time Serving (API/Streams)                    │
│   - Monitoring Data Drift, Concept Drift & Latency     │
│   - Automated Retraining Trigger                       │
└────────────────────────────────────────────────────────┘
```

![ML Deployment Architecture](images/01-introduction-02-deployment.jpg)
![Design, Train, Operate Lifecycle](images/01-introduction-03-design-train-operate.jpg)

---

## অধ্যায় ২: ডেভেলপমেন্ট ইনফ্রাস্ট্রাকচার ও এনভায়রনমেন্ট আর্কিটেকচার

### ২.১ কেন লোকাল অপারেটিং সিস্টেম (Windows/Mac) প্রোডাকশনের জন্য ঝুঁকিপূর্ণ?
উইন্ডোজ মেশিনে লোকাল পাথ ফরম্যাট (`C:\Users\...`, ব্যাকস্ল্যাশ `\`), প্রি-কম্পাইল্ড C++ এক্সটেনশন (যেমন `xgboost`, `pyarrow`, `scikit-learn`-এর Cython বাইনারি) এবং লোকাল এনভায়রনমেন্ট ভেরিয়েবল লিনাক্স প্রোডাকশন সার্ভারের মতো আচরণ করে না। প্রোডাকশন ডকার কন্টেইনার সবসময় Ubuntu/Debian ভিত্তিক লিনাক্সে রান করে। তাই ডেভেলপমেন্টের প্রথম দিন থেকেই একটি লিনাক্স ক্লাউড বা কন্টেইনারাইজড এনভায়রনমেন্ট নিশ্চিত করা অত্যন্ত জরুরি।

---

### ২.২ GitHub Codespaces এনভায়রনমেন্ট কনফিগারেশন
GitHub Codespaces সরাসরি রিপোজিটরি থেকে ক্লাউডে ডকার-বেসড ভার্চুয়াল মেশিন স্পিন-আপ করে দেয়।

![Codespaces Editor Interface](images/02-codespaces-01-editor.jpg)

#### Codespaces ব্যবহারের প্রধান ধাপসমূহ:
1. GitHub রিপোজিটরির **Code** বাটনে ক্লিক করে **Codespaces** ট্যাবে যান।
2. নতুন কোডস্পেস তৈরি করলে ব্রাউজারে একটি পূর্ণাঙ্গ VS Code ইন্টারফেস চালু হয়।
3. টার্মিনালে পাইথন ৩.৯+ এনভায়রনমেন্ট এবং লিনাক্স টুলস বিল্ট-ইন থাকে।

![Codespaces Terminal Commands](images/02-codespaces-02-terminal.jpg)
![Codespaces Jupyter Extension](images/02-codespaces-03-jupyter.jpg)

---

### ২.৩ AWS EC2 ভার্চুয়াল মেশিন, SSH সিকিউরিটি ও ডকার ডিমেন সেটআপ
যদি আপনার প্রজেক্টের জন্য বড় র‍্যাম বা জিপিইউ প্রয়োজন হয়, তবে AWS EC2 ব্যবহার করা স্ট্যান্ডার্ড প্যাটার্ন।

![AWS EC2 AMI Selection](images/03-aws-vm-01-ami.jpg)

#### স্টেপ-বাই-স্টেপ সেটআপ গাইড:
1. **AMI (Amazon Machine Image)**: `Ubuntu Server 22.04 LTS (HVM), SSD Volume Type` সিলেক্ট করুন।
2. **Instance Type**: ন্যূনতম `t2.medium` (২ vCPU, ৪ GB RAM) বা `t3.large` সিলেক্ট করুন।
3. **Key Pair**: একটি নতুন SSH Key Pair তৈরি করুন (যেমন `mlops-zoomcamp.pem`) এবং ডাউনলোড করুন।

![AWS SSH Key Pair Configuration](images/03-aws-vm-02-key-pair.jpg)

4. **Security Group কনফিগারেশন**:
   - `Port 22 (SSH)`: শুধুমাত্র আপনার নিজস্ব আইপি (`My IP`) দিয়ে সুরক্ষিত রাখুন।
   - `Port 8888 (Jupyter Notebook)` বা `Port 5000 (MLflow)`: পোর্ট ফরওয়ার্ডিং বা ভিপিএন দিয়ে ওপেন করুন।

5. **SSH কানেকশন কমান্ড (লিনাক্স/ম্যাক/উইন্ডোজ টার্মিনাল)**:
```bash
# কি-ফাইলের পারমিশন শুধুমাত্র রিড-ওনলি করা (নিরাপত্তার জন্য বাধ্যতামূলক)
chmod 400 mlops-zoomcamp.pem

# EC2 ইনস্ট্যান্সে লগইন করা
ssh -i "mlops-zoomcamp.pem" ubuntu@<ec2-public-ip-address>
```

6. **সার্ভারে ডকার ও প্রয়োজনীয় ডিপেন্ডেন্সি ইনস্টল করা**:
```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install -y docker.io docker-compose git wget

# রুট ইউজার ছাড়া সাধারণ ব্যবহারকারী দিয়ে ডকার চালাতে
sudo usermod -aG docker ubuntu
```

![AWS Docker Service Setup](images/03-aws-vm-03-docker.jpg)

---

## অধ্যায় ৩: ডেটা ইনজেশন ও স্টোরেজ অপটিমাইজেশন (Parquet বনাম CSV)

### ৩.১ NYC TLC ডেটাসেটের গঠন ও কলাম পরিচিতি
নিউ ইয়র্ক সিটিতে দুই ধরণের প্রধান ট্যাক্সি চলাচল করে:
- **Yellow Taxis (TPEP)**: ম্যানহাটনের প্রধান অংশে চলাচলকারী ঐতিহ্যবাহী হলুদ ট্যাক্সি।
- **Green Taxis (LPEP)**: ম্যানহাটনের বাইরের বোরোগুলো (ব্রুকলিন, কুইন্স, ব্রঙ্কস, স্টেটেন আইল্যান্ড) এবং আপার ম্যানহাটনে চলাচলের অনুমতিপ্রাপ্ত ট্যাক্সি।

আমরা জানুয়ারি ২০২১ এবং ফেব্রুয়ারি ২০২১-এর গ্রিন ট্যাক্সি ডেটা ব্যবহার করব:
```bash
mkdir -p data
wget https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2021-01.parquet -O data/green_tripdata_2021-01.parquet
wget https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2021-02.parquet -O data/green_tripdata_2021-02.parquet
```

![Dataset Download](images/04-read-parquet-01-download.jpg)

#### মূল কলামসমূহের অর্থ:
- `lpep_pickup_datetime`: ট্যাক্সি ভ্রমণের শুরুর তারিখ ও সময়।
- `lpep_dropoff_datetime`: ট্যাক্সি ভ্রমণের শেষের তারিখ ও সময়।
- `PULocationID`: পিকআপ ট্যাক্সি জোন আইডি (১ থেকে ২৬৫ পর্যন্ত সংখ্যা)।
- `DOLocationID`: ড্রপঅফ ট্যাক্সি জোন আইডি (১ থেকে ২৬৫ পর্যন্ত সংখ্যা)।
- `trip_distance`: ট্যাক্সি মিটারে পরিমাপকৃত ভ্রমণের দূরত্ব (মাইলে)।
- `fare_amount`: মিটারে প্রদর্শিত বেস ভাড়া।
- `passenger_count`: যাত্রীর সংখ্যা।

---

### ৩.২ কেন CSV বাদ দিয়ে Parquet ফরম্যাট ব্যবহার করা হলো? (ইঞ্জিনিয়ারিং কারণ)

বিগত বছরগুলোতে NYC TLC ডেটা CSV ফরম্যাটে ছিল। ২০২২ সালের পর থেকে তারা এটি সম্পূর্ণভাবে **Apache Parquet** ফরম্যাটে রূপান্তরিত করে।

#### ইঞ্জিনিয়ারিং তুলনা টেবিল:
| মানদণ্ড | CSV (Comma-Separated Values) | Apache Parquet | কেন Parquet বিজয়ী? |
| :--- | :--- | :--- | :--- |
| **স্টোরেজ ফরম্যাট** | Row-oriented (সারি-ভিত্তিক টেক্সট) | Columnar storage (কলাম-ভিত্তিক বাইনারি) | যদি মডেলে মাত্র ৩টি কলাম লাগে, Parquet শুধুমাত্র সেই ৩টি কলামের ডাটা ব্লক ডিস্ক থেকে পড়বে। CSV পুরো ফাইলের প্রতিটি ক্যারেক্টার স্ক্যান করে। |
| **ফাইল সাইজ** | ~১২০-১৫০ মেগাবাইট প্রতি মাস | ~১১-১২ মেগাবাইট প্রতি মাস | Parquet বিল্ট-ইন Snappy/Gzip অ্যালগরিদমে কলাম-ভিত্তিক কম্প্রেশন করে। স্টোরেজ খরচ ৯০% হ্রাস পায়। |
| **ডেটা টাইপ প্রিজারভেশন (Schema)** | কোনো স্কিমা নেই; সব টেক্সট হিসেবে থাকে। | বাইনারি মেটাডাটাতে প্রতিটি কলামের সুনির্দিষ্ট টাইপ সংরক্ষিত থাকে। | CSV পড়ার সময় Pandas-কে অনুমান করতে হয় কোনটি ইনটিজার, কোনটি ডেট। Parquet-এ `datetime` সরাসরি আসল টাইমস্ট্যাম্প হিসেবে লোড হয়। |
| **I/O রিডিং স্পিড** | অত্যন্ত ধীর (কয়েক মিনিট লাগতে পারে) | পলকের মধ্যে (কয়েক সেকেন্ড) | নেটওয়ার্ক ব্যান্ডউইথ ও ডিস্ক থ্রুপুট সর্বনিম্ন ব্যবহৃত হয়। |

---

### ৩.৩ PyArrow / fastparquet ইঞ্জিনের ভূমিকা
Python-এর Pandas লাইব্রেরির কোর মূলত C/C++ এ লেখা। কিন্তু Parquet ডিকোড করার জন্য Pandas-এর সাথে একটি বিশেষ ইঞ্জিন প্রয়োজন হয়:

```bash
pip install pyarrow fastparquet
```

যদি `pyarrow` ইনস্টল না থাকে, তবে Pandas নিচের মতো এরর প্রদান করে:
`ImportError: Unable to find a usable engine; tried using: 'pyarrow', 'fastparquet'.`

![Missing Parquet Engine](images/04-read-parquet-02-missing-engine.jpg)
![Reading Data in Pandas](images/04-read-parquet-03-read-data.jpg)

---

## অধ্যায় ৪: ডেটা ক্লিনিং ও ফিচার ইঞ্জিনিয়ারিং — লাইন-বাই-লাইন "কোড কেন লেখা হলো"

এখন আমরা মূল জুপিটার নোটবুক (`duration-prediction.ipynb`)-এর প্রতিটি গুরুত্বপূর্ণ কোড ব্লক পুঙ্খানুপুঙ্খভাবে ব্যবচ্ছেদ করব।

```python
import pandas as pd

df = pd.read_parquet('./data/green_tripdata_2021-01.parquet')
```

---

### ৪.১ টার্গেট ভেরিয়েবল ক্যালকুলেশন (`duration`)

```python
df['duration'] = df.lpep_dropoff_datetime - df.lpep_pickup_datetime
df.duration = df.duration.apply(lambda td: td.total_seconds() / 60)
```
*(অথবা ভেক্টরাইজড ভার্সন: `df['duration'] = (df['lpep_dropoff_datetime'] - df['lpep_pickup_datetime']).dt.total_seconds() / 60`)*

#### 🔍 কোড কেন লেখা হলো?
1. **টাইমস্ট্যাম্প ডিফারেন্স**: Parquet ফাইলে পিকআপ ও ড্রপঅফের সময় আগে থেকেই `pd.Timestamp` ফরম্যাটে থাকে। ড্রপঅফ থেকে পিকআপ বিয়োগ করলে Pandas একটি `Timedelta` সিরিজ তৈরি করে (উদাহরণ: `0 days 00:15:34`)।
2. **মিনিট এককে রূপান্তর**: 
   - ট্যাক্সি সার্ভিসে কেউ ট্রিপের সময় সেকেন্ডে মাপে না (যেমন: "আপনার ড্রাইভ ৯৩৪ সেকেন্ড সময় নেবে" — এটি অবাস্তব)।
   - আবার ঘণ্টা এককে নিলে মানগুলো খুব ক্ষুদ্র ফ্র্যাকশনে চলে আসে (যেমন: `0.259 ঘণ্টা`) যা ফ্লোটিং পয়েন্ট প্রিসিশন এবং লস ফাংশন ক্যালকুলেশনে সমস্যা করে।
   - **মিনিট** হলো মানব-ব্যবহারযোগ্য ও ব্যবসায়িক দৃষ্টিকোণ থেকে সবচেয়ে উপযুক্ত স্কেল। তাই `.total_seconds() / 60` দিয়ে সেকেন্ডকে ফ্লোট মিনিটে রূপান্তর করে এটিকেই আমাদের সুপারভাইজড লার্নিংয়ের টার্গেট ভ্যারিয়েবল ($y$) বানানো হয়েছে।

---

### ৪.২ আউটলায়ার ফিল্টারিং (১ থেকে ৬০ মিনিট): গাণিতিক ও ব্যবসায়িক কারণ

ডেটার ডিস্ট্রিবিউশন দেখতে আমরা চালাই:
```python
df.duration.describe(percentiles=[0.90, 0.95, 0.98, 0.99])
```

ফলাফলে দেখা যায়:
- মিনিমাম সময়: `-1.5` মিনিট বা নেগেটিভ মান! (মিটার রিসেট এরর)।
- ম্যাক্সিমাম সময়: `1440` মিনিট (২৪ ঘণ্টা) বা তারও বেশি!
- কিন্তু ৯৮% ট্রিপের সময় ৬০ মিনিটের নিচে!

তাই কোডে লেখা হলো:
```python
df = df[(df.duration >= 1) & (df.duration <= 60)]
```

#### 🔍 কোড কেন লেখা হলো? (গাণিতিক ও প্রকৌশলগত কারণ)
1. **নেগেটিভ ও জিরো মিনিট ট্রিপ**: কোনো ট্রিপের ডিউরেশন নেগেটিভ হতে পারে না। ১ মিনিটের কম ট্রিপগুলো সাধারণত যাত্রী ট্যাক্সিতে ওঠার সাথে সাথে বুকিং বাতিল করেছে অথবা ড্রাইভার ভুল বোতাম চেপে ট্রিপ ক্যান্সেল করে দিয়েছে। এগুলো কোনো বাস্তব ভ্রমণের প্রতিনিধিত্ব করে না।
2. **MSE লস ফাংশনের স্কয়ারড পেনাল্টি**: লিনিয়ার রিগ্রেশন অপটিমাইজেশনের জন্য Mean Squared Error (MSE) ব্যবহার করে:
   $$MSE = \frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2$$
   যদি একটি অস্বাভাবিক আউটলায়ার থাকে যার প্রকৃত সময় $y = 1200$ মিনিট, এবং মডেল প্রেডিক্ট করে $\hat{y} = 20$ মিনিট, তবে এর স্কয়ারড এরর হবে:
   $$(1200 - 20)^2 = 1180^2 = 1,392,400!$$
   এই একটিমাত্র এরর অপটিমাইজারের গ্র্যাডিয়েন্টকে এতটাই বিশৃঙ্খল করে দেবে যে মডেল বাকি হাজার হাজার স্বাভাবিক ট্রিপের জন্য ভুল প্রেডিকশন করতে শুরু করবে।
3. **বিজনেস স্কোপিং**: ৬০ মিনিটের চেয়ে দীর্ঘ ট্রিপ পুরো ডেটাসেটের ১-২%-এরও কম। প্রোডাকশন আর্কিটেকচারে ৬০ মিনিটের বেশি দীর্ঘ দূরত্বের ভ্রমণের জন্য আলাদা ডেডিকেটেড রুট অপটিমাইজার ব্যবহার করা হয়। সাধারণ রাইডের জন্য ১-৬০ মিনিটের উইন্ডো রাখা মডেলের ভ্যারিয়েন্সকে নিয়ন্ত্রণে রাখে।

![Dataframe Inspection](images/05-train-duration-model-01-dataframe.jpg)

---

### ৪.৩ ক্যাটাগরিক্যাল ভেরিয়েবল টাইপ কাস্টিং (`astype(str)`)

```python
categorical = ['PULocationID', 'DOLocationID']
numerical = ['trip_distance']

df[categorical] = df[categorical].astype(str)
```

#### 🔍 কোড কেন লেখা হলো? (বিপদজনক বাগ প্রতিরোধ)
- `PULocationID` (পিকআপ লোকেশন) এবং `DOLocationID` (ড্রপঅফ লোকেশন) Parquet ফাইলে পূর্ণসংখ্যা (Integer) হিসেবে সংরক্ষিত থাকে (যেমন: `43`, `86`, `120`)।
- **মারাত্মক ভুল**: যদি আমরা এই কলামগুলোকে সরাসরি মডেলে দিয়ে দিই, তবে মেশিন লার্নিং অ্যালগরিদম ধরে নেবে এটি একটি ধারাবাহিক গাণিতিক সংখ্যা (Continuous Numerical Feature)! 
  - অর্থাৎ মডেল ভাববে: জোন ৮৬ হলো জোন ৪৩-এর ঠিক **দ্বিগুণ**! 
  - কিন্তু বাস্তবে জোন ৪৩ হলো সেন্ট্রাল পার্ক এবং জোন ৮৬ হলো ব্রঙ্কসের একটি আবাসিক এলাকা। এদের মধ্যে কোনো দ্বিগুণ বা তিনগুণের সম্পর্ক নেই।
- **সমাধান**: `.astype(str)` দিয়ে এদেরকে স্ট্রিংয়ে রূপান্তর করা হলো (যেমন: `'43'`, `'86'`)। এর ফলে ভেক্টরাইজার বুঝতে পারবে এরা সংখ্যা নয়, স্বতন্ত্র ক্যাটাগোরিক্যাল লেবেল।

---

### ৪.৪ ফিচার ক্রসিং (Feature Interaction / Route Encoding)

মডেলের প্রথম ভার্সনে আলাদাভাবে `PULocationID` এবং `DOLocationID` দেওয়া হয়েছিল। কিন্তু পরবর্তী ধাপে কোডে একটি নতুন শক্তিশালী ফিচার তৈরি করা হয়:

```python
df['PU_DO'] = df['PULocationID'] + '_' + df['DOLocationID']
categorical = ['PU_DO']
```

#### 🔍 কোড কেন লেখা হলো? (কেন RMSE ৯ মিনিট থেকে ৫ মিনিটে নেমে আসলো?)
1. **স্বাধীন বনাম যৌথ প্যাটার্ন**:
   - যদি আমরা শুধু জানি পিকআপ লোকেশন `A` এবং ড্রপঅফ লোকেশন `B`, তবে সাধারণ লিনিয়ার মডেল যোগফল শিখবে: $\text{Effect}(A) + \text{Effect}(B)$।
   - কিন্তু বাস্তবে লোকেশন `A` থেকে `B`-তে যাওয়ার ট্রিপ ডিউরেশন সম্পূর্ণ নির্ভর করে তাদের মধ্যকার **সুনির্দিষ্ট রুট, দূরত্ব এবং ট্রাফিক কন্ডিশনের** ওপর!
   - `A` থেকে `B`-তে যাওয়ার অভিজ্ঞতা আর `A` থেকে `C`-তে যাওয়ার অভিজ্ঞতা সম্পূর্ণ ভিন্ন।
2. **নন-লিনিয়ার রিলেশনশিপ ক্যাপচার**:
   - লিনিয়ার রিগ্রেশন সরাসরি দুটি ফিচারের ক্রস-প্রোডাক্ট শিখতে পারে না।
   - কিন্তু যখন আমরা `'43_100'` স্ট্রিং তৈরি করি, তখন মডেল প্রতিটি নির্দিষ্ট রুটের জন্য একটি স্বতন্ত্র ওয়ান-হট কো-এফিশিয়েন্ট ($w_{\text{route}}$) বরাদ্দ করতে পারে।
   - একে মেশিন লার্নিংয়ের ভাষায় বলা হয় **Feature Crossing (বা Feature Interaction)**। এই একটি ফিচার যোগ করার ফলেই মডেলের ভ্যালিডেশন RMSE প্রায় অর্ধেক কমে যায়!

![Features Representation](images/05-train-duration-model-02-features.jpg)

---

## অধ্যায় ৫: ভেক্টরাইজেশন ও স্পার্স ম্যাট্রিক্স আর্কিটেকচার

### ৫.১ কেন `pd.get_dummies` বাদ দিয়ে `DictVectorizer` ব্যবহার করা হলো?
অনেক ডেটা সায়েন্টিস্ট ডেটা এক্সপ্লোরেশনের সময় Pandas-এর `pd.get_dummies(df)` ব্যবহার করেন। কিন্তু প্রোডাকশন MLOps-এ `pd.get_dummies` ব্যবহার করা একটি মারাত্মক অ্যান্টি-প্যাটার্ন (Anti-pattern)।

#### তুলনামূলক বিশ্লেষণ:
1. **প্রোডাকশন টেস্ট সেটে কলাম অমিল (Schema Mismatch)**:
   - ধরুন, ট্রেইনিং ডেটাতে পিকআপ জোন ছিল `43, 86, 120`। `pd.get_dummies` ৩টি কলাম তৈরি করবে।
   - প্রোডাকশনে এমন একজন যাত্রী আসলেন যার পিকআপ জোন `999` (নতুন জোন)। `pd.get_dummies` তখন একদম ভিন্ন কলাম তৈরি করবে, অথবা জোন `86` না থাকলে সেই কলামটি বাদ দিয়ে দেবে। এর ফলে স্ক্র্যাচ থেকে তৈরি হওয়া ম্যাট্রিক্স মডেলে ঢুকলে `Dimension mismatch error` দিয়ে এপিআই ক্র্যাশ করবে।
2. **মেমরি লিক (Dense Matrix Disaster)**:
   - `pd.get_dummies` মেমরিতে সাধারণ ডেন্স (Dense) 2D অ্যারে তৈরি করে, যেখানে লাখ লাখ শূন্য (`0`) স্টোর করতে গিগাবাইট গিগাবাইট র‍্যাম অপচয় হয়।

#### `DictVectorizer`-এর শ্রেষ্ঠত্ব:
```python
from sklearn.feature_extraction import DictVectorizer

train_dicts = df[categorical + numerical].to_dict(orient='records')

dv = DictVectorizer()
X_train = dv.fit_transform(train_dicts)
```

1. `DictVectorizer` একটি **Scikit-Learn Transformer**। এটি ট্রেইনিং ডেটাতে দেখা প্রতিটি ক্যাটাগরির ইনডেক্স ম্যাপিং নিজের ভেতরে সংরক্ষণ করে (`dv.vocabulary_`)।
2. নতুন ডেটা আসলে এটি শুধুমাত্র সেই পরিচিত ক্যাটাগরিগুলোকে এনকোড করে এবং সম্পূর্ণ নতুন বা অজানা ক্যাটাগরি আসলে নীরবে উপেক্ষা করে, ফলে কোনো ডাইমেনশন এরর হয় না।
3. এটি ইনপুট হিসেবে ডিকশনারির লিস্ট নেয় (`to_dict(orient='records')`), যা রিয়েল-টাইম প্রোডাকশন API-তে ইনকামিং JSON রিকোয়েস্টের হুবহু অনুরূপ!

---

### ৫.২ মেমরি আর্কিটেকচার: SciPy CSR Sparse Matrix

যখন আমরা `df['PU_DO']` (হাজার হাজার রুট) ওয়ান-হট এনকোড করি, তখন ১৩,০০০-এর বেশি কলাম তৈরি হয়।
- প্রতিটি রো-তে মাত্র একটি `PU_DO` এবং একটি `trip_distance` উপস্থিত থাকে।
- অর্থাৎ একটি সারির ১৩,০০০ কলামের মধ্যে **১২,৯৯৮টি কলামের মানই হলো 0 (শূন্য)**!
- একে বলা হয় **Sparsity (শূন্যের আধিক্য)**।

`dv.fit_transform()` কল করলে এটি সাধারণ NumPy অ্যারে তৈরি না করে রিটার্ন করে:
`<73908x13221 sparse matrix of type '<class 'numpy.float64'>' with 147816 stored elements in Compressed Sparse Row format>`

#### CSR (Compressed Sparse Row) কীভাবে কাজ করে?
সাধারণ অ্যারেতে `73,908 × 13,221 × 8 bytes ≈ 7.8 GB` র‍্যাম লাগত!
কিন্তু CSR ফরম্যাট শুধুমাত্র যেখানে অশূন্য (non-zero) মান আছে তাদের ইনডেক্স এবং ভ্যালু স্টোর করে। ফলে ৭.৮ গিগাবাইটের ম্যাট্রিক্স মাত্র **কয়েক মেগাবাইট** মেমরিতে এঁটে যায়!

---

### ৫.৩ `fit_transform` বনাম `transform`: ডেটা লিকেজ প্রতিরোধের বাঁধন

```python
# ১. ট্রেইনিং ডেটায় ফিট এবং ট্রান্সফর্ম উভয়ই করা হবে
X_train = dv.fit_transform(train_dicts)

# ২. ভ্যালিডেশন ডেটায় শুধুমাত্র ট্রান্সফর্ম করতে হবে!
val_dicts = df_val[categorical + numerical].to_dict(orient='records')
X_val = dv.transform(val_dicts)
```

#### 🔍 কোড কেন লেখা হলো?
- `fit()` কল করার অর্থ হলো ডেটাসেট থেকে সব ইউনিক ক্যাটাগরি আবিষ্কার করা এবং তাদের একটি নির্দিষ্ট কলাম ইনডেক্স বরাদ্দ করা।
- যদি আমরা ভ্যালিডেশন সেটেও `fit_transform` কল করি, তবে দুটি ধ্বংসাত্মক ঘটনা ঘটবে:
  1. ভ্যালিডেশন সেটের নিজস্ব ক্যাটাগরির ওপর ভিত্তি করে কলামের সংখ্যা ও ক্রম বদলে যাবে। ফলে $X_{\text{train}}$-এর কলাম ৫ যদি হয় `'PU_DO=43_100'`, তবে $X_{\text{val}}$-এর কলাম ৫ হতে পারে `'PU_DO=10_20'`। মডেল সম্পূর্ণ ভুল কলামে ভুল ওয়েট গুণ করে ভুল প্রেডিকশন দেবে।
  2. ভ্যালিডেশন সেটের কোনো তথ্য ট্রেইনিং ফেজে লিক হয়ে যাওয়া (Data Leakage)।
- তাই নিয়ম: **"Fit only once on Train; Transform everywhere else."**

---

## অধ্যায় ৬: অ্যালগরিদম ম্যাথমেটিক্স, বেসলাইন মডেল ও রেগুলারাইজেশন

### ৬.১ Ordinary Least Squares (OLS) লিনিয়ার রিগ্রেশন

```python
from sklearn.linear_model import LinearRegression

target = 'duration'
y_train = df[target].values

lr = LinearRegression()
lr.fit(X_train, y_train)
```

#### গাণিতিক ভিত্তি:
লিনিয়ার রিগ্রেশনের সমীকরণ:
$$\hat{y} = w_0 + w_1 x_1 + w_2 x_2 + \dots + w_p x_p = X w$$
এখানে $w$ হলো মডেলের প্যারামিটার (Weights বা Coefficients)।

সর্বোত্তম $w$ খুঁজে পেতে লস ফাংশন (Residual Sum of Squares) মিনিমাইজ করা হয়:
$$L(w) = \|y - X w\|_2^2$$
ম্যাট্রিক্স ক্যালকুলাস দিয়ে ডেরিভেটিভ শূন্য ধরলে আমরা পাই বিখ্যাত **Normal Equation**:
$$w = (X^T X)^{-1} X^T y$$

#### MLOps ইনসাইট:
- সাধারণ ডেটাসেটে OLS খুব দ্রুত হিসাব করা যায়।
- কিন্তু যখন ফিচারের সংখ্যা ১৩,০০০ ছাড়িয়ে যায়, তখন $(X^T X)$ হলো একটি $13000 \times 13000$ ম্যাট্রিক্স। এর ইনভার্স বের করা অত্যন্ত ব্যয়বহুল। এছাড়া কিছু রুট যদি অত্যন্ত দুর্লভ হয়, তবে ম্যাট্রিক্সটি সিংগুলার বা কলিনিয়ার হয়ে যেতে পারে।
- তা সত্ত্বেও, বেসলাইন হিসেবে Linear Regression বেছে নেওয়ার কারণ হলো এর সরলতা, দ্রুত ইনফারেন্স ল্যাটেন্সি এবং ইন্টারপ্রেটেবিলিটি।

![Linear Regression Training](images/05-train-duration-model-03-linear-regression.jpg)

---

### ৬.২ ইভ্যালুয়েশন মেট্রিক: Root Mean Squared Error (RMSE)

```python
from sklearn.metrics import root_mean_squared_error

y_pred = lr.predict(X_val)
rmse = root_mean_squared_error(y_val, y_pred)
print(f"Validation RMSE: {rmse:.2f}")
```

#### 🔍 কেন RMSE বেছে নেওয়া হলো? (MAE নয় কেন?)
- **RMSE সূত্র**:
  $$RMSE = \sqrt{\frac{1}{N} \sum_{i=1}^{N} (y_i - \hat{y}_i)^2}$$
- **ইউনিট সমতা**: স্কয়ার রুট নেওয়ার কারণে RMSE-এর ইউনিট সরাসরি টার্গেটের ইউনিটের (মিনিট) সমান হয়। যদি $RMSE = 7.8$, এর অর্থ হলো আমাদের মডেল গড়ে প্রায় **৭.৮ মিনিট ভুল প্রেডিকশন** করে।
- **বড় ভুলের জন্য কঠোর শাস্তি**: MAE (Mean Absolute Error) সব ভুলকে সমানভাবে দেখে। কিন্তু ট্যাক্সি ব্যবসায় যদি একটি রাইড ৫ মিনিটের বদলে ৭ মিনিট হয় (২ মিনিট ভুল), তা তেমন ক্ষতি করে না। কিন্তু যদি ১৫ মিনিটের রাইড ৪৫ মিনিট প্রেডিক্ট করে (৩০ মিনিট ভুল), তবে যাত্রী ট্রেন মিস করবেন বা ক্ষুব্ধ হবেন। স্কয়ারিংয়ের কারণে RMSE বড় ভুলগুলোকে কঠোরভাবে পেনাল্টি দেয়, যা প্রোডাকশন নির্ভরযোগ্যতার জন্য অত্যন্ত গুরুত্বপূর্ণ।

---

### ৬.৩ রেগুলারাইজেশন: কেন Lasso (L1) এবং Ridge (L2) প্রয়োজন?

যখন আমরা ১৩,০০০ ক্রস-ফিচার তৈরি করি, অনেক রুট হয়তো পুরো মাসে মাত্র ১ বার এসেছে। মডেল সেই একটি ট্রিপের নয়েজকে সত্য ভেবে ওভারফিট করে ফেলতে পারে।

```python
from sklearn.linear_model import Lasso

lr_lasso = Lasso(alpha=0.01)
lr_lasso.fit(X_train, y_train)

y_pred = lr_lasso.predict(X_val)
```

#### 🔍 Lasso (L1) বনাম Ridge (L2)-এর তুলনা:
1. **Lasso (L1 Regularization)**:
   $$\text{Loss} = MSE + \alpha \sum_{j=1}^{p} |w_j|$$
   - **বৈশিষ্ট্য**: L1 পেনাল্টির জ্যামিতিক সীমাবদ্ধতা হলো একটি ডায়মন্ড (বহুভুজ)। যখন কনট্যুর লাইন ডায়মন্ডের কোণায় স্পর্শ করে, তখন অপ্রয়োজনীয় বা নয়েজি ফিচারের ওয়েট সরাসরি **০.০০ (শূন্য)** হয়ে যায়!
   - **ইঞ্জিনিয়ারিং সুবিধা**: এটি স্পার্সিটি তৈরি করে এবং স্বয়ংক্রিয়ভাবে ফিচার সিলেকশন করে। ১৩,০০০ ফিচারের মধ্যে হয়তো মাত্র ১,২০০ ফিচারের মান অশূন্য থাকে। ফলে প্রোডাকশনে মডেলের সাইজ ছোট হয় এবং ইনফারেন্স দ্রুত হয়।
2. **Ridge (L2 Regularization)**:
   $$\text{Loss} = MSE + \alpha \sum_{j=1}^{p} w_j^2$$
   - **বৈশিষ্ট্য**: L2 পেনাল্টি ওয়েটগুলোকে শূন্যের কাছাকাছি সংকুচিত করে কিন্তু কোনো ওয়েট পুরোপুরি শূন্য করে না।

---

## অধ্যায় ৭: মডেল ডায়াগনস্টিকস ও রেসিডুয়াল বিশ্লেষণ

### ৭.১ এরর ডিস্ট্রিবিউশন প্লট (Prediction vs Actual)

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.distplot(y_pred, label='prediction')
sns.distplot(y_train, label='actual')
plt.title("Actual vs Predicted Duration Distribution")
plt.legend()
plt.show()
```

#### 🔍 কোড কেন লেখা হলো?
শুধু একটি সংখ্যা (RMSE = 7.8) দেখে মডেলের আসল চরিত্র বোঝা যায় না। প্রেডিকশন এবং আসল ডেটার কার্ভ পাশাপাশি প্লট করলে মডেলের ত্রুটি স্পষ্টভাবে ধরা পড়ে:

1. **পিক পজিশন (Peak Shift)**: আসল ট্রিপগুলোর পিক (মোস্ট ফ্রিকোয়েন্ট ডিউরেশন) হয়তো ৮-১০ মিনিটের মধ্যে, কিন্তু মডেলের প্রেডিকশন কার্ভ কি ঠিক একই জায়গায় পিক করছে?
2. **রাইট-টেইল আন্ডার-এস্টিমেশন (The Long Tail Problem)**:
   - ট্যাক্সি ডেটা একটি রাইট-স্কিউড (Right-skewed) ডিস্ট্রিবিউশন অনুসরণ করে (অধিকাংশ ট্রিপ ছোট, কিন্তু কিছু ট্রিপ ৪০-৬০ মিনিটের লম্বা)।
   - ডিস্ট্রিবিউশন প্লটে দেখা যায়, লিনিয়ার মডেল দীর্ঘ ট্রিপগুলোর ক্ষেত্রে প্রায়শই আন্ডার-এস্টিমেট করে (অর্থাৎ ৫০ মিনিটের ট্রিপকে ৩০-৩৫ মিনিট প্রেডিক্ট করে ফেলে)।
   - এই ভিজ্যুয়ালাইজেশন প্রমাণ করে যে শুধুমাত্র সাধারণ লিনিয়ার মডেল দিয়ে রিয়েল-ওয়ার্ল্ডের সমস্ত জটিলতা সমাধান করা সম্ভব নয়; পরবর্তী মডিউলগুলোতে Gradient Boosted Trees (XGBoost, LightGBM) ব্যবহার করার যৌক্তিকতা এখান থেকেই আসে।

---

## অধ্যায় ৮: মডেল সিরিয়ালাইজেশন ও প্রোডাকশন আর্টিফ্যাক্ট সেভিং

### ৮.১ কেন `pickle.dump((dv, lr), f)`-এ ভেক্টরাইজার ও মডেল একসাথে সেভ করা হলো?

মডেল ট্রেনিং শেষে আমরা ফাইল সেভ করি:

```python
import os
import pickle

os.makedirs('models', exist_ok=True)
with open('models/lin_reg.bin', 'wb') as f_out:
    pickle.dump((dv, lr), f_out)
```

#### 🔍 কোড কেন লেখা হলো? (সবচেয়ে মারাত্মক প্রোডাকশন বাগ প্রতিরোধ)
অনেক জুনিয়র ইঞ্জিনিয়ার শুধুমাত্র মডেলটি সেভ করেন: `pickle.dump(lr, f_out)`। এটি প্রোডাকশনে মারাত্মক বিপর্যয় ডেকে আনে!

#### কেন?
1. প্রোডাকশনে কোনো ডেটাফ্রেম থাকে না। ক্লায়েন্ট এপিআই-তে একটি র কাঁচা JSON পে-লোড পাঠায়:
   ```json
   {
     "PULocationID": 43,
     "DOLocationID": 100,
     "trip_distance": 3.5
   }
   ```
2. মডেল `lr` এই JSON সরাসরি বুঝতে পারে না। তার ইনপুট হিসেবে চাই একটি $1 \times 13,221$ সাইজের স্পার্স ভেক্টর।
3. যদি আপনার কাছে ট্রেনিংয়ের সময় তৈরি হওয়া নির্দিষ্ট `DictVectorizer` অবজেক্টটি (`dv`) সংরক্ষিত না থাকে, তবে আপনি কখনোই প্রোডাকশনের JSON-কে ট্রেইনিংয়ের মতো একই কলাম ইনডেক্সে রূপান্তর করতে পারবেন না।
4. তাই প্রি-প্রসেসর `dv` এবং এস্টিমেটর `lr`-কে একটি একক টাপল `(dv, lr)` আকারে সেভ করা হলো, যাতে ডিপ্লয়মেন্ট সার্ভার একটিমাত্র ফাইল লোড করেই সম্পূর্ণ এন্ড-টু-এন্ড প্রেডিকশন পাইপলাইন পেয়ে যায়।

---

## অধ্যায় ৯: জুপিটার নোটবুক থেকে মডুলার কোড পাইপলাইনে রূপান্তর

### ৯.১ জুপিটার নোটবুকের লুকানো বিপদ (Hidden State Bug)
- জুপিটার নোটবুকে সেলগুলো যে কোনো ক্রমে (যেমন: ৫ নম্বর সেলের পর ২ নম্বর সেল) রান করা যায়।
- মেমরিতে ভ্যারিয়েবলের মান কী আছে তা বাহ্যিক কোড দেখে বোঝা যায় না।
- নোটবুকের কোডে ইউনিট টেস্ট বা ইন্টিগ্রেশন টেস্ট চালানো যায় না।
- গিটহাবে নোটবুকের JSON মেটাডাটা ভার্সন কন্ট্রোল ও মার্জ কনফ্লিক্টের দুঃস্বপ্ন তৈরি করে।

### ৯.২ রিইউজেবল মডুলার পাইথন স্ক্রিপ্ট আর্কিটেকচার
প্রোডাকশনের প্রথম পদক্ষেপ হলো পুরো লজিককে ক্লাসিক্যাল ক্লিন ফাংশনে বিভক্ত করা:
1. `read_dataframe(filename)`: I/O এবং বেসিক ক্লিনিং।
2. `prepare_features(df)`: ফিচার ইঞ্জিনিয়ারিং ও ভেক্টরাইজেশন।
3. `train_model(X_train, y_train)`: মডেল ফিটিং।
4. `save_model(artifact, path)`: ডিস্কে সিরিয়ালাইজেশন।

![Notebook to Script Transition](images/06-course-overview-01-notebook.jpg)
![Training Pipeline Orchestration](images/06-course-overview-02-pipeline.jpg)
![Model Serving as a Service](images/06-course-overview-03-service.jpg)

---

## অধ্যায় ১০: MLOps ম্যাচিউরিটি মডেল (Level 0 থেকে Level 2)

গুগল ও মাইক্রোসফটের প্রস্তাবিত আর্কিটেকচার অনুযায়ী একটি প্রতিষ্ঠানের MLOps সক্ষমতাকে ৩টি প্রধান স্তরে ভাগ করা হয়:

| স্তর | পর্যায় | ডেটা প্রিপারেশন | মডেল ট্রেইনিং | ডিপ্লয়মেন্ট | মনিটরিং |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **Level 0** | **Manual Process** (ম্যানুয়াল) | জুপিটার নোটবুকে ডেটাসায়েন্টিস্ট হাতে হাতে ডেটা ডাউনলোড ও ক্লিন করেন। | লোকাল পিসিতে বা নোটবুকে ম্যানুয়ালি সেল রান করে মডেল ট্রেন হয়। | ইঞ্জিনিয়ারদের কাছে `.bin` বা `.pkl` ফাইল ড্রপবক্স/স্ল্যাকে পাঠানো হয়। ইঞ্জিনিয়াররা কোডে হার্ডকোড করেন। | কোনো সিস্টেম মনিটরিং নেই। ব্যবহারকারী কমপ্লেইন করলে বোঝা যায় মডেল ফেইল করেছে। |
| **Level 1** | **ML Pipeline Automation** (পাইপলাইন অটোমেশন) | প্রিফেক্ট/এয়ারফ্লো দিয়ে স্বয়ংক্রিয়ভাবে ডেটা ফেচ ও ভ্যালিডেট হয়। | নতুন ডেটা আসলে ক্লাউডে অটোমেটেড রি-ট্রেইনিং পাইপলাইন (Continuous Training - CT) ট্রিগার হয়। | মডেল স্বয়ংক্রিয়ভাবে মডেল রেজিস্ট্রিতে রেজিস্টার হয়, কিন্তু প্রোডাকশন রিলিজ আংশিক ম্যানুয়াল। | প্রেডিকশন ল্যাটেন্সি ও এরর কিছুটা ট্র্যাক করা হয়। |
| **Level 2** | **Full CI/CD & Production Orchestration** | সম্পূর্ণ টেস্টেড ফিচার স্টোর ও ডেটা পাইপলাইন। | হাইপারপ্যারামিটার টিউনিং ও ট্রেইনিং সম্পূর্ণ ডকারাইজড ও অর্কেস্ট্রেটেড। | কোড পুশ হলে স্বয়ংক্রিয় CI টেস্ট, ডকার বিল্ড এবং কিউবারনেটিস/ল্যাম্বডায় জিরো-ডাউনটাইম CD ডিপ্লয়মেন্ট। | রিয়েল-টাইম ডাটা ড্রিফট, কনসেপ্ট ড্রিফট ও পারফরম্যান্স ড্যাশবোর্ড (Evidently/Grafana) চালু থাকে। |

---

## অধ্যায় ১১: মডিউল ১ হোমওয়ার্কের পুঙ্খানুপুঙ্খ সমাধান ও গাণিতিক বিশ্লেষণ

মডিউল ১-এর হোমওয়ার্কটি NYC Yellow Taxi ডেটাসেটের ওপর ভিত্তি করে তৈরি। নিচে প্রতিটি প্রশ্নের সুনির্দিষ্ট সমাধান ও তার পেছনের কারণ তুলে ধরা হলো:

### প্রশ্ন ১: জানুয়ারি ২০২৩ ডেটাসেটে কতগুলো কলাম রয়েছে?
- **কমান্ড**:
  ```python
  import pandas as pd
  df = pd.read_parquet('yellow_tripdata_2023-01.parquet')
  print(len(df.columns))
  ```
- **উত্তর**: **১৯টি কলাম (19 columns)**।

### প্রশ্ন ২: জানুয়ারি ২০২৩-এর ট্রিপ ডিউরেশনের স্ট্যান্ডার্ড ডেভিয়েশন (Standard Deviation) কত?
- **হিসাব**:
  ```python
  df['duration'] = (df.tpep_dropoff_datetime - df.tpep_pickup_datetime).dt.total_seconds() / 60
  print(df.duration.std())
  ```
- **ফলাফল**: **৪২.৫৯ মিনিট (42.59 minutes)**।
- **ব্যাখ্যা**: স্ট্যান্ডার্ড ডেভিয়েশন এত বেশি হওয়ার কারণ হলো ডেটাতে কিছু তীব্র আউটলায়ার ছিল (কয়েক হাজার মিনিটের ট্রিপ), যা ডেটার ভ্যারিয়েন্সকে বিশাল করে তোলে।

### প্রশ্ন ৩: ১ থেকে ৬০ মিনিটের মধ্যে ফিল্টার করার পর কত শতাংশ ডেটা অবশিষ্ট থাকে?
- **হিসাব**:
  ```python
  initial_rows = len(df)
  df_filtered = df[(df.duration >= 1) & (df.duration <= 60)]
  fraction = len(df_filtered) / initial_rows
  print(f"{fraction * 100:.2f}%")
  ```
- **ফলাফল**: **৯৮% (98%)**।
- **উপসংহার**: মাত্র ২% অস্বাভাবিক ডেটা বাদ দিয়ে আমরা মডেলের ট্রেইনিংকে ৯৮% সুস্থ ও স্থিতিশীল ডেটার ওপর ফোকাস করতে সক্ষম হই।

### প্রশ্ন ৪: ওয়ান-হট এনকোডিংয়ের পর ফিচার ম্যাট্রিক্সের ডাইমেনশন (কলাম সংখ্যা) কত?
- **হিসাব**:
  ```python
  categorical = ['PULocationID', 'DOLocationID']
  df_filtered[categorical] = df_filtered[categorical].astype(str)
  train_dicts = df_filtered[categorical].to_dict(orient='records')
  dv = DictVectorizer()
  X_train = dv.fit_transform(train_dicts)
  print(X_train.shape[1])
  ```
- **ফলাফল**: **৫১৫টি কলাম (515 columns)**।
- **ব্যাখ্যা**: নিউ ইয়র্কের প্রায় ২৬০টি পিকআপ জোন এবং ২৬০টি ড্রপঅফ জোনের ইউনিক ক্যাটাগরিগুলো মিলে ৫১৫টি বাইনারি ওয়ান-হট কলাম তৈরি করে।

### প্রশ্ন ৫: ট্রেনিং সেটে লিনিয়ার রিগ্রেশন মডেলের RMSE কত?
- **হিসাব**:
  ```python
  lr = LinearRegression()
  lr.fit(X_train, y_train)
  y_pred = lr.predict(X_train)
  print(root_mean_squared_error(y_train, y_pred))
  ```
- **ফলাফল**: **৭.৬৪ মিনিট (7.64 minutes)**।

### প্রশ্ন ৬: ভ্যালিডেশন সেটে (ফেব্রুয়ারি ২০২৩) মডেলের RMSE কত?
- **হিসাব**:
  ```python
  # ফেব্রুয়ারি ডেটা ফিল্টারিং ও শুধুমাত্র transform কল করা
  val_dicts = df_val[categorical].to_dict(orient='records')
  X_val = dv.transform(val_dicts)
  y_pred_val = lr.predict(X_val)
  print(root_mean_squared_error(y_val, y_pred_val))
  ```
- **ফলাফল**: **৭.৮১ মিনিট (7.81 minutes)**।
- **বিশ্লেষণ**: ট্রেনিং এরর ৭.৬৪ এবং ভ্যালিডেশন এরর ৭.৮১—উভয়ের মান কাছাকাছি হওয়ায় প্রমাণিত হয় যে মডেলটি ওভারফিট করেনি, বরং একটি শক্তিশালী বেসলাইন তৈরি করেছে।

---

## অধ্যায় ১২: সম্পূর্ণ এক্সিকিউটেবল প্রোডাকশন পাইথন কোড

নিচে সম্পূর্ণ পাইপলাইন স্ক্রিপ্টটি তুলে ধরা হলো। এটি মডুলার, টাইপ-হিন্টেড এবং সরাসরি কমান্ড-লাইন থেকে এক্সিকিউটযোগ্য:

```python
"""
NYC Taxi Trip Duration Prediction Service
Module 1: Production-Ready Baseline Pipeline
Author: MLOps Zoomcamp
"""

import os
import sys
import pickle
import logging
from typing import Tuple, List
import pandas as pd
from scipy.sparse import csr_matrix
from sklearn.feature_extraction import DictVectorizer
from sklearn.linear_model import LinearRegression, Lasso
from sklearn.metrics import root_mean_squared_error

# লগিং কনফিগারেশন
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s [%(levelname)s] %(message)s',
    handlers=[logging.StreamHandler(sys.stdout)]
)
logger = logging.getLogger(__name__)


def read_and_clean_data(file_path: str) -> pd.DataFrame:
    """
    Parquet ফাইল থেকে ডেটা লোড করে, ডিউরেশন ক্যালকুলেট করে
    এবং অস্বাভাবিক আউটলায়ার ফিল্টার করে।
    """
    if not os.path.exists(file_path):
        raise FileNotFoundError(f"ফাইলটি খুঁজে পাওয়া যায়নি: {file_path}")

    logger.info(f"ডেটা ফাইল লোড করা হচ্ছে: {file_path}")
    df = pd.read_parquet(file_path)

    initial_count = len(df)
    
    # ১. ডিউরেশন মিনিট এককে হিসাব
    df['duration'] = (
        df['lpep_dropoff_datetime'] - df['lpep_pickup_datetime']
    ).dt.total_seconds() / 60

    # ২. আউটলায়ার ফিল্টারিং (১ থেকে ৬০ মিনিটের ট্রিপ)
    df = df[(df.duration >= 1) & (df.duration <= 60)].copy()
    filtered_count = len(df)
    logger.info(
        f"ফিল্টারিং সম্পন্ন: {initial_count} টি রো থেকে {filtered_count} টি রো রাখা হয়েছে "
        f"({(filtered_count / initial_count) * 100:.2f}% ডেটা অক্ষত)"
    )

    # ৩. ক্যাটাগরিক্যাল কাস্টিং (স্ট্রিংয়ে রূপান্তর)
    categorical_cols = ['PULocationID', 'DOLocationID']
    df[categorical_cols] = df[categorical_cols].astype(str)

    # ৪. ফিচার ক্রসিং (রুট তৈরি)
    df['PU_DO'] = df['PULocationID'] + '_' + df['DOLocationID']

    return df


def extract_features(
    df_train: pd.DataFrame, 
    df_val: pd.DataFrame, 
    categorical: List[str], 
    numerical: List[str]
) -> Tuple[csr_matrix, csr_matrix, DictVectorizer]:
    """
    DictVectorizer ব্যবহার করে ক্যাটাগরিক্যাল ও নিউমেরিক্যাল ফিচার ভেক্টরাইজ করে।
    Train সেটে fit_transform এবং Validation সেটে transform নিশ্চিত করে।
    """
    logger.info("ফিচার ভেক্টরাইজেশন শুরু হচ্ছে...")
    dv = DictVectorizer()

    # ট্রেনিং ডিকশনারি তৈরি ও ফিটিং
    train_dicts = df_train[categorical + numerical].to_dict(orient='records')
    X_train = dv.fit_transform(train_dicts)
    logger.info(f"X_train স্পার্স ম্যাট্রিক্স ডাইমেনশন: {X_train.shape}")

    # ভ্যালিডেশন ডিকশনারি তৈরি ও রূপান্তর (Fit ছাড়া)
    val_dicts = df_val[categorical + numerical].to_dict(orient='records')
    X_val = dv.transform(val_dicts)
    logger.info(f"X_val স্পার্স ম্যাট্রিক্স ডাইমেনশন: {X_val.shape}")

    return X_train, X_val, dv


def train_and_evaluate(
    X_train: csr_matrix, 
    y_train: pd.Series, 
    X_val: csr_matrix, 
    y_val: pd.Series
) -> Tuple[LinearRegression, Lasso]:
    """
    Linear Regression বেসলাইন এবং Lasso রিগ্রেশন ট্রেন ও ইভ্যালুয়েট করে।
    """
    # ১. লিনিয়ার রিগ্রেশন
    logger.info("--- Linear Regression ট্রেইনিং শুরু ---")
    lr = LinearRegression()
    lr.fit(X_train, y_train)

    train_pred_lr = lr.predict(X_train)
    val_pred_lr = lr.predict(X_val)

    train_rmse_lr = root_mean_squared_error(y_train, train_pred_lr)
    val_rmse_lr = root_mean_squared_error(y_val, val_pred_lr)
    logger.info(f"Linear Regression -> Train RMSE: {train_rmse_lr:.2f} min | Val RMSE: {val_rmse_lr:.2f} min")

    # ২. লাসো রিগ্রেশন (L1 Regularization)
    logger.info("--- Lasso Regression (alpha=0.01) ট্রেইনিং শুরু ---")
    lasso = Lasso(alpha=0.01)
    lasso.fit(X_train, y_train)

    val_pred_lasso = lasso.predict(X_val)
    val_rmse_lasso = root_mean_squared_error(y_val, val_pred_lasso)
    logger.info(f"Lasso Regression    -> Val RMSE: {val_rmse_lasso:.2f} min")

    return lr, lasso


def save_artifacts(dv: DictVectorizer, model: LinearRegression, output_path: str) -> None:
    """
    প্রিপ্রসেসর ভেক্টরাইজার এবং মডেল অবজেক্ট একটি টাপল আকারে ডিস্কে সেভ করে।
    """
    os.makedirs(os.path.dirname(output_path), exist_ok=True)
    with open(output_path, 'wb') as f_out:
        pickle.dump((dv, model), f_out)
    logger.info(f"আর্টিফ্যাক্ট সফলভাবে সেভ করা হয়েছে: {output_path} ✅")


def main():
    train_data_path = './data/green_tripdata_2021-01.parquet'
    val_data_path = './data/green_tripdata_2021-02.parquet'
    model_output_path = './models/lin_reg.bin'

    # ১. ডেটা রিড ও প্রিপারেশন
    df_train = read_and_clean_data(train_data_path)
    df_val = read_and_clean_data(val_data_path)

    # ২. ফিচার সিলেকশন
    categorical_features = ['PU_DO']
    numerical_features = ['trip_distance']

    # ৩. ভেক্টরাইজেশন
    X_train, X_val, dv = extract_features(
        df_train, df_val, categorical_features, numerical_features
    )

    y_train = df_train['duration'].values
    y_val = df_val['duration'].values

    # ৪. মডেল ট্রেইনিং ও মূল্যায়ন
    best_lr_model, _ = train_and_evaluate(X_train, y_train, X_val, y_val)

    # ৫. প্রোডাকশন সেভিং
    save_artifacts(dv, best_lr_model, model_output_path)


if __name__ == '__main__':
    main()
```
