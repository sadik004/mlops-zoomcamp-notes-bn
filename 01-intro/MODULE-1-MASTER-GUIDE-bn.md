# মডিউল ১: সম্পূর্ণ মাস্টার গাইড ও ইঞ্জিনিয়ারিং কোডেক্স (Module 1 Master Codex)

> **ডকুমেন্ট স্ট্যাটাস**: MLOps Zoomcamp-এর মডিউল ১-এর পূর্ণাঙ্গ এবং চূড়ান্ত রেফারেন্স গাইড। এই নথিতে কোনো সংক্ষিপ্তকরণ করা হয়নি। প্রতিটি লেকচার, জুপিটার নোটবুকের প্রতিটি সেল, প্রতিটি কোড লাইনের পেছনের প্রকৌশলগত যুক্তি (**"কোড কেন এভাবে লেখা হলো"**), বিকল্প পদ্ধতির সাথে তুলনা, গাণিতিক ডেরিভেশন এবং প্রোডাকশন এপিআই-তে মডেল ব্যবহারের রূপরেখা বিশদভাবে লিপিবদ্ধ করা হয়েছে।

---

## সূচিপত্র (Table of Contents)
1. [অধ্যায় ১: MLOps-এর মূল দর্শন ও বিজনেস আর্কিটেকচার](#অধ্যায়-১-mlops-এর-মূল-দর্শন-ও-বিজনেস-আর্কিটেকচার)
   - ১.১ ট্রেডিশনাল সফটওয়্যার বনাম মেশিন লার্নিং সিস্টেম
   - ১.২ Data Drift ও Concept Drift: বাস্তব জীবনের বিপর্যয়
   - ১.৩ বিজনেস প্রবলেম স্টেটমেন্ট: NYC ট্যাক্সি রাইড ডিউরেশন (ETA) প্রেডিকশন
   - ১.৪ মেশিন লার্নিং লাইফসাইকেল: Design ➔ Train ➔ Operate
2. [অধ্যায় ২: ডেভেলপমেন্ট ইনফ্রাস্ট্রাকচার ও ক্লাউড এনভায়রনমেন্ট](#অধ্যায়-২-ডেভেলপমেন্ট-ইনফ্রাস্ট্রাকচার-ও-ক্লাউড-এনভায়রনমেন্ট)
   - ২.১ লোকাল ওএস বনাম ক্লাউড/লিনাক্স কন্টেইনার
   - ২.২ GitHub Codespaces আর্কিটেকচার ও কনফিগারেশন
   - ২.৩ AWS EC2 ভার্চুয়াল মেশিন, SSH সিকিউরিটি ও ডকার সেটআপ
   - ২.৪ ভার্চুয়াল এনভায়রনমেন্ট ও ডিপেন্ডেন্সি ম্যানেজমেন্ট
3. [অধ্যায় ৩: ডেটা ইনজেশন ও ফাইল ফরম্যাট অপটিমাইজেশন (Parquet বনাম CSV)](#অধ্যায়-৩-ডেটা-ইনজেশন-ও-ফাইল-ফরম্যাট-অপটিমাইজেশন-parquet-বনাম-csv)
   - ৩.১ NYC TLC ট্রিপ ডেটাসেটের গঠন ও কলাম স্কিমা
   - ৩.২ CSV বনাম Apache Parquet: বিশদ টেকনিক্যাল ও মেমরি তুলনা
   - ৩.৩ PyArrow ইঞ্জিনের ভূমিকা ও C++ মেমরি বাফার
4. [অধ্যায় ৪: জুপিটার নোটবুকের প্রতিটি সেলের লাইন-বাই-লাইন বিশ্লেষণ ও "কোড কেন লেখা হলো"](#অধ্যায়-৪-জুপিটার-নোটবুকের-প্রতিটি-সেলের-লাইন-বাই-লাইন-বিশ্লেষণ-ও-কোড-কেন-লেখা-হলো)
   - ৪.১ সেল ১-৪: ডিপেন্ডেন্সি ইমপোর্ট ও সংস্করণ নিরীক্ষণ
   - ৪.২ সেল ৫: ডেটা লোডিং, ডিউরেশন ক্যালকুলেশন ও আউটলায়ার ফিল্টারিং
   - ৪.৩ সেল ৬: টাইপ কাস্টিং ও বেসলাইন DictVectorizer
   - ৪.৪ সেল ৭: রেসিডুয়াল ডিস্ট্রিবিউশন প্লট (Seaborn)
   - ৪.৫ সেল ৮-১০: রিইউজেবল ফাংশন আর্কিটেকচার (`read_dataframe`)
   - ৪.৬ সেল ১১-১২: ফিচার ক্রসিং (Feature Interaction: `PU_DO`)
   - ৪.৭ সেল ১৩-১৪: ভ্যালিডেশন সেটে ট্রেইন ও ইভ্যালুয়েশন
   - ৪.৮ সেল ১৫: মডেল ও প্রিপ্রসেসর সিরিয়ালাইজেশন (Pickle)
   - ৪.৯ সেল ১৬: Lasso রিগ্রেশন ও L1 রেগুলারাইজেশন
5. [অধ্যায় ৫: ভেক্টরাইজেশন মেমরি আর্কিটেকচার: SciPy CSR Sparse Matrix](#অধ্যায়-৫-ভেক্টরাইজেশন-মেমরি-আর্কিটেকচার-scipy-csr-sparse-matrix)
   - ৫.১ কেন `pd.get_dummies` ব্যবহার করা প্রোডাকশনে নিষিদ্ধ?
   - ৫.২ Compressed Sparse Row (CSR) মেমরি সেভিংস হিসাব
   - ৫.৩ `fit_transform` বনাম `transform`: Data Leakage-এর বিস্তার
6. [অধ্যায় ৬: অ্যালগরিদম ম্যাথমেটিক্স ও অপটিমাইজেশন থিওরি](#অধ্যায়-৬-অ্যালগরিদম-ম্যাথমেটিক্স-ও-অপটিমাইজেশন-থিওরি)
   - ৬.১ Ordinary Least Squares (OLS) ও Normal Equation
   - ৬.২ ইভ্যালুয়েশন মেট্রিক: RMSE বনাম MAE বনাম MAPE
   - ৬.৩ রেগুলারাইজেশন থিওরি: Lasso ($L_1$) বনাম Ridge ($L_2$)
7. [অধ্যায় ৭: কেন জুপিটার নোটবুক প্রোডাকশনের জন্য ক্ষতিকর এবং কীভাবে রিফ্যাক্টর করতে হয়](#অধ্যায়-৭-কেন-জুপিটার-নোটবুক-প্রোডাকশনের-জন্য-ক্ষতিকর-এবং-কীভাবে-রিফ্যাক্টর-করতে-হয়)
   - ৭.১ নোটবুকের ৭টি মারাত্মক প্রোডাকশন ত্রুটি
   - ৭.২ ক্লিন আর্কিটেকচার ও মডুলারাইজেশন
8. [অধ্যায় ৮: প্রোডাকশন সার্ভিসিং মকআপ (FastAPI Integration)](#অধ্যায়-৮-প্রোডাকশন-সার্ভিসিং-মকআপ-fastapi-integration)
   - ৮.১ সিরিয়ালাইজড আর্টিফ্যাক্ট লোড করে রিয়েল-টাইম API তৈরি
9. [অধ্যায় ৯: MLOps ম্যাচিউরিটি মডেল (Level 0, 1, 2)](#অধ্যায়-৯-mlops-ম্যাচিউরিটি-মডেল-level-0-1-2)
10. [অধ্যায় ১০: মডিউল ১ হোমওয়ার্কের পুঙ্খানুপুঙ্খ গাণিতিক ও কোড সমাধান](#অধ্যায়-১০-মডিউল-১-হোমওয়ার্কের-পুঙ্খানুপুঙ্খ-গাণিতিক-ও-কোড- সমাধান)
11. [অধ্যায় ১১: সম্পূর্ণ প্রোডাকশন পাইপলাইন পাইথন স্ক্রিপ্ট](#অধ্যায়-১১-সম্পূর্ণ-প্রোডাকশন-পাইপলাইন-পাইথন-স্ক্রিপ্ট)

---

## অধ্যায় ১: MLOps-এর মূল দর্শন ও বিজনেস আর্কিটেকচার

### ১.১ ট্রেডিশনাল সফটওয়্যার বনাম মেশিন লার্নিং সিস্টেম

একটি সফটওয়্যার ইঞ্জিনিয়ারিং প্রজেক্ট এবং একটি মেশিন লার্নিং সিস্টেমের মধ্যে মৌলিক পার্থক্য হলো সিস্টেমের ডিটারমিনিস্টিক প্রকৃতি:

```
[Traditional Software Engineering]
Code (Business Rules)  +  Input Data  ════►  Deterministic Output

[Machine Learning Engineering]
Input Data  +  Observed Output (Labels)  ════►  Learned Model (Approximated Rules)

[Inference / Production Serving]
New Unseen Data  +  Learned Model  ════►  Probabilistic Prediction
```

- **ট্রেডিশনাল সফটওয়্যার**: একবার কোড লিখে ইউনিট টেস্ট ও ইন্টিগ্রেশন টেস্ট পাস করালে, বাহ্যিক কোড পরিবর্তন না হওয়া পর্যন্ত সিস্টেম আজীবন একই ইনপুটের জন্য একই আউটপুট দেবে।
- **মেশিন লার্নিং সিস্টেম**: এখানে কোড অপরিবর্তিত থাকলেও সিস্টেমের পারফরম্যান্স প্রতিনিয়ত ক্ষয়প্রাপ্ত (degrade) হতে পারে। কারণ বাস্তব পৃথিবীর ডেটা কখনোই স্থির থাকে না।

![The Taxi Trip Prediction Problem](images/01-introduction-01-taxi-trip.jpg)

---

### ১.২ Data Drift ও Concept Drift: বাস্তব জীবনের বিপর্যয়

উৎপাদন পরিবেশে মেশিন লার্নিং মডেল ফেইল করার পেছনে দুটি প্রধান চালিকাশক্তি রয়েছে:

#### ১. ডেটা ড্রিফট (Data Drift / Covariate Shift):
ইনপুট ডেটার পরিসংখ্যানিক ডিস্ট্রিবিউশন পরিবর্তিত হয়ে যায়, কিন্তু ইনপুট ও টার্গেটের অভ্যন্তরীণ সম্পর্ক একই থাকে:
$$P_{\text{train}}(X) \neq P_{\text{production}}(X), \quad \text{কিন্তু} \quad P(y|X) \text{ অপরিবর্তিত}$$
*উদাহরণ*: করোনা মহামারীর সময়ে হঠাৎ করে মানুষের ভ্রমণের দূরত্ব ও পিকআপ লোকেশনের প্যাটার্ন বদলে গেল। মডেল ট্রেনিংয়ের সময় কখনো এমন শূন্য-রাস্তার ট্রাফিক বা অস্বাভাবিক পিকআপ ডিস্ট্রিবিউশন দেখেনি। ফলে মডেলের ইনপুট স্পেস আনদেখা অঞ্চলে প্রবেশ করে।

#### ২. কনসেপ্ট ড্রিফট (Concept Drift):
ইনপুট ডেটার ডিস্ট্রিবিউশন একই থাকলেও ইনপুট এবং আউটপুট টার্গেটের মধ্যে গাণিতিক সম্পর্কটিই বদলে যায়:
$$P_{\text{train}}(y|X) \neq P_{\text{production}}(y|X)$$
*উদাহরণ*: ম্যানহাটনে নতুন স্পিড লিমিট আইন জারি করা হলো অথবা কোনো প্রধান এক্সপ্রেসওয়েতে এক বছরের জন্য রোড-ওয়ার্ক শুরু হলো। এখন জোন ৪৩ থেকে ১০০-তে যাওয়ার দূরত্ব একই ($X$ অপরিবর্তিত), কিন্তু ট্রাফিক জ্যামের কারণে সময় আগের চেয়ে দ্বিগুণ লাগছে ($y$ পরিবর্তিত)। পুরনো মডেল এখন প্রতিনিয়ত ভুল আন্ডার-এস্টিমেট করবে।

---

### ১.৩ বিজনেস প্রবলেম স্টেটমেন্ট: NYC ট্যাক্সি রাইড ডিউরেশন (ETA) প্রেডিকশন
আমরা কাজ করছি **New York City Taxi & Limousine Commission (TLC)**-এর ট্রিপ রেকর্ড নিয়ে।

#### ব্যবসায়িক চাহিদা:
একজন যাত্রী যখন রাইড শেয়ারিং অ্যাপে বা ট্যাক্সিতে ওঠার মুহূর্তে পিকআপ লোকেশন ও ড্রপঅফ লোকেশন নির্বাচন করেন, তখন ব্যাকএন্ডকে কয়েক মিলি-সেকেন্ডের মধ্যে প্রেডিক্ট করতে হবে:
$$\hat{y} = \text{Estimated Trip Duration (in minutes)}$$

#### বিজনেসে ভুল প্রেডিকশনের প্রভাব:
1. **Under-estimation (কম সময় প্রেডিক্ট করা)**:
   - মডেল বলল ১৫ মিনিট লাগবে, কিন্তু ট্রিপে লাগল ৩৫ মিনিট।
   - যাত্রী ফ্লাইট বা মিটিং মিস করবেন, তীব্র অসন্তোষ তৈরি হবে এবং ব্র্যান্ড ভ্যালু ধ্বংস হবে।
2. **Over-estimation (বেশি সময় প্রেডিক্ট করা)**:
   - মডেল বলল ৬০ মিনিট লাগবে, কিন্তু বাস্তবে লাগবে ২০ মিনিট।
   - যাত্রী দীর্ঘ সময় দেখে বুকিং বাতিল করবেন (Churn), যার ফলে সরাসরি রাজস্ব ক্ষতি (Lost Revenue) হবে।

---

### ১.৪ মেশিন লার্নিং লাইফসাইকেল: Design ➔ Train ➔ Operate

একটি সার্থক MLOps আর্কিটেকচার ৩টি মৌলিক চক্রে আবর্তিত হয়:

```
┌────────────────────────────────────────────────────────┐
│                   1. DESIGN PHASE                      │
│   - বিজনেস প্রবলেমকে ML ফরম্যাটে রূপান্তর               │
│   - ডেটা সোর্স আবিষ্কার ও কোয়ালিটি অডিট                 │
│   - আর্কিটেকচারাল ডিসিশন (Batch vs Streaming vs API)   │
└──────────────────────────┬─────────────────────────────┘
                           │
                           ▼
┌────────────────────────────────────────────────────────┐
│                   2. TRAIN PHASE                       │
│   - ডেটা ক্লিনিং ও ফিচার ইঞ্জিনিয়ারিং                │
│   - এক্সপেরিমেন্ট ট্র্যাকিং (Hyperparameters, Metrics)  │
│   - মডেল ইভ্যালুয়েশন ও ভ্যালিডেশন                      │
│   - মডেল প্যাকেজিং ও ভার্সনিং                          │
└──────────────────────────┬─────────────────────────────┘
                           │
                           ▼
┌────────────────────────────────────────────────────────┐
│                   3. OPERATE PHASE                     │
│   - CI/CD ডিপ্লয়মেন্ট (Docker, Kubernetes, Cloud)    │
│   - মডেল সার্ভিং ও লো-ল্যাটেন্সি প্রেডিকশন             │
│   - ডেটা ড্রিফট, প্রেডিকশন ড্রিফট ও সিস্টেম হেলথ ট্র্যাকিং │
│   - অটোমেটেড রি-ট্রেইনিং লুপ                           │
└────────────────────────────────────────────────────────┘
```

![ML Deployment Architecture](images/01-introduction-02-deployment.jpg)
![Design, Train, Operate Lifecycle](images/01-introduction-03-design-train-operate.jpg)

---

## অধ্যায় ২: ডেভেলপমেন্ট ইনফ্রাস্ট্রাকচার ও ক্লাউড এনভায়রনমেন্ট

### ২.১ লোকাল ওএস বনাম ক্লাউড/লিনাক্স কন্টেইনার
উইন্ডোজ বা ম্যাকওএস মেশিনে লোকাল ডেটা সায়েন্স কাজ করার সময় নিচের সমস্যাগুলো তৈরি হয়:
- উইন্ডোজ ফাইলপাথ ব্যাকস্ল্যাশ (`\`) ব্যবহার করে, যা লিনাক্স প্রোডাকশন পাথের (`/`) সাথে ইনকম্প্যাটিবল।
- C/C++ নির্ভর বাইনারি (যেমন `pyarrow`, `xgboost`, `lightgbm`) উইন্ডোজের জন্য আলাদা কম্পাইলার বাইন্ডিংস ব্যবহার করে। লোকাল মেশিনে কোড রান করলেও ডকার কন্টেইনারে তা প্রায়শই সেগমেন্টেশন ফল্ট দিয়ে ক্র্যাশ করে।
- তাই প্রোডাকশনের প্রথম নীতি: **ডেভেলপমেন্ট এনভায়রনমেন্ট যেন হুবহু প্রোডাকশন লিনাক্স এনভায়রনমেন্টের প্রতিচ্ছবি হয়।**

---

### ২.২ GitHub Codespaces আর্কিটেকচার ও কনফিগারেশন
GitHub Codespaces ক্লাউডে একটি ডেডিকেটেড ডকার কন্টেইনার প্রোভিশন করে, যার ব্যাকএন্ডে থাকে Azure VM।

![Codespaces Editor Interface](images/02-codespaces-01-editor.jpg)

#### কোডস্পেসের মূল সুবিধাসমূহ:
- ব্রাউজারে সম্পূর্ণ ফুল-ফিচার্ড VS Code এডিটর।
- লিনাক্স টার্মিনাল এক্সেস (Ubuntu LTS)।
- পোর্ট ফরওয়ার্ডিং (Port 8888 for Jupyter, Port 5000 for MLflow UI)।

![Codespaces Terminal Commands](images/02-codespaces-02-terminal.jpg)
![Codespaces Jupyter Extension](images/02-codespaces-03-jupyter.jpg)

---

### ২.৩ AWS EC2 ভার্চুয়াল মেশিন, SSH সিকিউরিটি ও ডকার সেটআপ

বড় স্কেলের ডেটাসেট বা জিপিইউ ট্রেনিংয়ের জন্য AWS EC2 ইনস্ট্যান্স প্রোভিশন করা স্ট্যান্ডার্ড পদ্ধতি।

![AWS EC2 AMI Selection](images/03-aws-vm-01-ami.jpg)

#### ইনস্ট্যান্স কনফিগারেশন গাইডলাইন:
1. **AMI**: `Ubuntu Server 22.04 LTS (HVM), SSD Volume Type` (লিনাক্স স্ট্যান্ডার্ড)।
2. **Instance Type**: 
   - সাধারণ এক্সপেরিমেন্টের জন্য: `t2.medium` (২টি vCPU, ৪ GB RAM) অথবা `t3.large` (২টি vCPU, ৮ GB RAM)।
   - হেভি ট্রেনিংয়ের জন্য: `c5.2xlarge` বা `g4dn.xlarge` (GPU)।
3. **Key Pair সিকিউরিটি**:
   ডাউনলোড করা `.pem` ফাইলের পারমিশন পরিবর্তন করা আবশ্যক, অন্যথায় ওপেনএসএসএইচ কানেকশন রিজেক্ট করবে:
   ```bash
   chmod 400 mlops-zoomcamp.pem
   ```

![AWS SSH Key Pair Configuration](images/03-aws-vm-02-key-pair.jpg)

4. **Security Group রুলস**:
   - `Port 22 (SSH)`: শুধুমাত্র নিজস্ব পাবলিক আইপি (`MY_IP/32`) দিয়ে রেস্ট্রিক্ট করুন।
   - পোর্ট ২২ ইন্টারনেটে সবার জন্য (`0.0.0.0/0`) ওপেন রাখা মারাত্মক সাইবার সিকিউরিটি রিস্ক (অবিরাম ব্রুট-ফোর্স অ্যাটাক শুরু হয়)।
5. **সার্ভার লগইন ও ডকার ইনস্টলেশন**:
   ```bash
   ssh -i "mlops-zoomcamp.pem" ubuntu@<EC2-PUBLIC-IP>

   # ডকার ও প্রয়োজনীয় টুলস ইনস্টলেশন
   sudo apt-get update && sudo apt-get upgrade -y
   sudo apt-get install -y docker.io docker-compose git wget

   # বর্তমান ব্যবহারকারীকে ডকার গ্রুপে যুক্ত করা (sudo ছাড়া docker কমান্ড রান করতে)
   sudo usermod -aG docker ubuntu
   newgrp docker
   ```

![AWS Docker Service Setup](images/03-aws-vm-03-docker.jpg)

---

### ২.৪ ভার্চুয়াল এনভায়রনমেন্ট ও ডিপেন্ডেন্সি ম্যানেজমেন্ট

পাইথনের গ্লোবাল এনভায়রনমেন্টে সরাসরি প্যাকেজ ইনস্টল করা প্রোডাকশন অ্যান্টি-প্যাটার্ন। প্যাকেজ ভার্সন লকিং নিশ্চিত করতে Pipenv বা Poetry ব্যবহার করা হয়।

#### `Pipfile` উদাহরণ:
```toml
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]
pandas = ">=2.2.0"
pyarrow = ">=16.0.0"
scikit-learn = ">=1.5.0"
seaborn = ">=0.13.0"
matplotlib = ">=3.9.0"

[dev-packages]
pytest = ">=8.0.0"
black = ">=24.0.0"
isort = ">=5.13.0"
jupyter = ">=1.0.0"

[requires]
python_version = "3.10"
```

```bash
# এনভায়রনমেন্ট তৈরি ও লকফাইল জেনারেট করা
pipenv install --dev

# এনভায়রনমেন্ট অ্যাক্টিভেট করা
pipenv shell
```

---

## অধ্যায় ৩: ডেটা ইনজেশন ও ফাইল ফরম্যাট অপটিমাইজেশন (Parquet বনাম CSV)

### ৩.১ NYC TLC ট্রিপ ডেটাসেটের গঠন ও কলাম স্কিমা
নিউ ইয়র্ক সিটি ট্যাক্সি ডেটা দুটি প্রধান ভাগে বিভক্ত:
- **Yellow Taxis (TPEP - Taxicab Passenger Enhancement Program)**: ম্যানহাটন ও বিমানবন্দরের প্রধান ক্যাব।
- **Green Taxis (LPEP - Limousine and Passenger Enhancement Program)**: বরো ট্যাক্সি (কুইন্স, ব্রুকলিন, ব্রঙ্কস)।

আমরা জানুয়ারি ২০২১ ও ফেব্রুয়ারি ২০২১-এর গ্রিন ট্যাক্সি ডেটা ডাউনলোড করব:
```bash
mkdir -p data
wget https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2021-01.parquet -O data/green_tripdata_2021-01.parquet
wget https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2021-02.parquet -O data/green_tripdata_2021-02.parquet
```

![Dataset Download](images/04-read-parquet-01-download.jpg)

#### মূল ২০টি কলামের ডিকশনারি ও ডেটাটাইপ:
1. `VendorID` (`int64`): ট্যাক্সি মিটার টেকনোলজি প্রোভাইডার কোড (১ = Creative Mobile, ২ = VeriFone)।
2. `lpep_pickup_datetime` (`timestamp[us]`): ট্রিপ শুরুর সঠিক সময় ও তারিখ।
3. `lpep_dropoff_datetime` (`timestamp[us]`): ট্রিপ সমাপ্তির সঠিক সময় ও তারিখ।
4. `store_and_fwd_flag` (`string`): সার্ভারে পাঠানোর আগে মেমরিতে সংরক্ষিত ছিল কিনা (Y/N)।
5. `RatecodeID` (`float64`): ট্রিপ রেট টাইপ (১ = Standard, ২ = JFK, ৩ = Newark ইত্যাদি)।
6. `PULocationID` (`int64`): TLC ট্যাক্সি জোন আইডি যেখানে ট্রিপ শুরু হয়েছে (১-২৬৫)।
7. `DOLocationID` (`int64`): TLC ট্যাক্সি জোন আইডি যেখানে ট্রিপ শেষ হয়েছে (১-২৬৫)।
8. `passenger_count` (`float64`): ড্রাইভারের ইনপুট করা যাত্রীর সংখ্যা।
9. `trip_distance` (`float64`): মিটারে রেকর্ডকৃত দূরত্ব (মাইলে)।
10. `fare_amount` (`float64`): মিটার অনুযায়ী ভাড়ার পরিমাণ।
11. `extra` (`float64`): পিক আওয়ার এবং ওভারনাইট সারচার্জ।
12. `mta_tax` (`float64`): MTA মেট্রোপলিটন ট্যাক্স ($0.50)।
13. `tip_amount` (`float64`): ক্রেডিট কার্ডে প্রাপ্ত বকশিশ।
14. `tolls_amount` (`float64`): ব্রিজ ও টানেল টোল ফি।
15. `ehail_fee` (`float64`): ইলেকট্রনিক হেইলিং ফি।
16. `improvement_surcharge` (`float64`): টেক্সি আধুনিকায়ন সারচার্জ ($0.30)।
17. `total_amount` (`float64`): যাত্রীর মোট প্রদেয় বিল।
18. `payment_type` (`float64`): পেমেন্ট মেথড (১ = Credit card, ২ = Cash ইত্যাদি)।
19. `trip_type` (`float64`): ১ = Street-hail, ২ = Dispatch।
20. `congestion_surcharge` (`float64`): ম্যানহাটন কনজেশন সারচার্জ।

---

### ৩.২ CSV বনাম Apache Parquet: বিশদ টেকনিক্যাল ও মেমরি তুলনা

বিগত বছরগুলোতে NYC TLC ডেটা CSV ফরম্যাটে সংরক্ষিত থাকত। ২০২২ সাল থেকে সম্পূর্ণ ডেটাবেস Parquet ফরম্যাটে মাইগ্রেট করা হয়।

```
[CSV: Row-Oriented Storage]
Row 1: VendorID, PickupTime, DropoffTime, PULoc, DOLoc, Dist, Fare
Row 2: VendorID, PickupTime, DropoffTime, PULoc, DOLoc, Dist, Fare
Row 3: VendorID, PickupTime, DropoffTime, PULoc, DOLoc, Dist, Fare
=> যদি আমাদের শুধু 'Dist' কলাম পড়তে হয়, তবুও ডিস্ক থেকে সমস্ত রো এবং কলাম পড়তে বাধ্য হয়!

[Parquet: Column-Oriented Storage]
Column 'VendorID':   [1, 2, 2, ...] (Bit-packed)
Column 'PickupTime': [t1, t2, t3, ...] (Delta-encoded)
Column 'Dist':       [2.5, 1.2, 0.8, ...] (Snappy-compressed Block)
=> যদি আমাদের শুধু 'Dist' কলাম পড়তে হয়, তবে ডিস্ক সরাসরি এই ব্লকটিতে জাম্প করে!
```

#### ইঞ্জিনিয়ারিং তুলনা টেবিল:
| মানদণ্ড | CSV (Comma-Separated Values) | Apache Parquet | ইঞ্জিনিয়ারিং সুবিধা |
| :--- | :--- | :--- | :--- |
| **স্টোরেজ ফরম্যাট** | Row-Oriented ASCII টেক্সট | Columnar Binary ফরম্যাট | ডিস্ক I/O এবং মেমরি বাসে ডাটা ট্রান্সফার ৯০% কমে যায়। |
| **ফাইল সাইজ (জানুয়ারি ২০২১)** | ~১২৫ MB | ~১১.২ MB | ক্লাউড অবজেক্ট স্টোরেজ (S3/GCS) খরচ এবং ডাউনলোডের সময় ১০ গুণ সাশ্রয়ী। |
| **কম্প্রেশন স্কিম** | পুরো ফাইল জিপ করতে হয় (Gzip) | কলাম-ভিত্তিক Snappy/Zstandard কম্প্রেশন | প্রতিটি কলামের ডেটাটাইপ অনুযায়ী অপটিমাল অ্যালগরিদমে কম্প্রেস হয়। |
| **টাইপ প্রিজারভেশন (Schema)** | কোনো টাইপ তথ্য নেই; সবকিছু কাঁচা স্ট্রিং। | বাইনারি হেডারে স্কিমা সংরক্ষিত থাকে। | ডেটা লোড করার সময় `parse_dates` দিয়ে স্লো স্ট্রিং পার্সিং করার প্রয়োজন নেই। |
| **পার্টিশনিং ও সিলেকশন** | পুরো ফাইল মেমরিতে লোড করতে হয়। | কলাম প্রজেকশন ও রো-গ্রুপ ফিল্টারিং। | `pd.read_parquet(..., columns=['PULocationID', 'trip_distance'])` দিলে ডিস্ক থেকে শুধু এই দুটি কলাম পড়া হয়। |

---

### ৩.৩ PyArrow ইঞ্জিনের ভূমিকা ও C++ মেমরি বাফার

Pandas লাইব্রেরি নিজে Parquet ফাইল পার্স করতে পারে না। এটি লো-লেভেল পার্সিংয়ের জন্য **Apache Arrow (PyArrow)** ব্যবহার করে।
- PyArrow C++ ভাষায় লেখা। এটি মেমরিতে **Zero-Copy Serialization** প্রযুক্তি ব্যবহার করে।
- অর্থাৎ ডিস্কের বাইনারি বাফার সরাসরি CPU ক্যাশে কোনো পাইথন অবজেক্ট ওভারহেড ছাড়া লোড হতে পারে।

```bash
pip install pyarrow fastparquet
```

যদি আপনার পাইথন এনভায়রনমেন্টে `pyarrow` ইনস্টল না থাকে, তবে Pandas ফাইল লোড করার সময় ফেইল করবে:
`ImportError: Unable to find a usable engine; tried using: 'pyarrow', 'fastparquet'.`

![Missing Parquet Engine](images/04-read-parquet-02-missing-engine.jpg)
![Reading Data in Pandas](images/04-read-parquet-03-read-data.jpg)

---

## অধ্যায় ৪: জুপিটার নোটবুকের প্রতিটি সেলের লাইন-বাই-লাইন বিশ্লেষণ ও "কোড কেন লেখা হলো"

এখন আমরা `duration-prediction.ipynb` নোটবুকের প্রতিটি কোড সেল আলাদাভাবে ব্যবচ্ছেদ করব।

---

### ৪.১ সেল ১-৪: ডিপেন্ডেন্সি ইমপোর্ট ও সংস্করণ নিরীক্ষণ

```python
# CELL 0
!python -V

# CELL 1
import pandas as pd

# CELL 2
import pickle

# CELL 3
import seaborn as sns
import matplotlib.pyplot as plt

# CELL 4
from sklearn.feature_extraction import DictVectorizer
from sklearn.linear_model import LinearRegression
from sklearn.linear_model import Lasso
from sklearn.linear_model import Ridge

from sklearn.metrics import root_mean_squared_error
```

#### 🔍 কোড কেন লেখা হলো?
- `!python -V`: পাইথন সংস্করণ নিশ্চিত করা (৩.৯ বা ৩.১০-এর পরিবর্তনশীল ফিচার যেমন `root_mean_squared_error` সাপোর্ট করে কি না তা জানা)। Scikit-Learn ১.৪+ সংস্করণে পুরনো `mean_squared_error(..., squared=False)` ডেপ্রিকেটেড হয়ে সরাসরি `root_mean_squared_error` যুক্ত হয়েছে।
- `pickle`: পাইথনের বিল্ট-ইন অবজেক্ট সিরিয়ালাইজার যা ট্রেন করা মডেল এবং ভেক্টরাইজারকে বাইনারি ফাইল হিসেবে সেভ করবে।
- `DictVectorizer`: মেশিন লার্নিং ফিচার এক্সট্রাকশনের জন্য Scikit-Learn-এর সর্বোত্তম ট্রান্সফরমার যা ক্যাটাগরিক্যাল ডিকশনারিকে মেমরি-সাশ্রয়ী স্পার্স ম্যাট্রিক্সে রূপান্তর করে।

---

### ৪.২ সেল ৫: ডেটা লোডিং, ডিউরেশন ক্যালকুলেশন ও আউটলায়ার ফিল্টারিং

```python
# CELL 5
df = pd.read_parquet('./data/green_tripdata_2021-01.parquet')

df['duration'] = df.lpep_dropoff_datetime - df.lpep_pickup_datetime
df.duration = df.duration.apply(lambda td: td.total_seconds() / 60)

df = df[(df.duration >= 1) & (df.duration <= 60)]

categorical = ['PULocationID', 'DOLocationID']
numerical = ['trip_distance']

df[categorical] = df[categorical].astype(str)
```

#### 🔍 লাইন-বাই-লাইন ব্যবচ্ছেদ ও "কোড কেন লেখা হলো":

1. `df['duration'] = df.lpep_dropoff_datetime - df.lpep_pickup_datetime`
   - **ইন্টারনাল মেকানিক্স**: Parquet ফরম্যাটে সংরক্ষিত `timestamp[us]` ডেটা Pandas-এ সরাসরি `datetime64[ns]` অবজেক্ট হিসেবে লোড হয়। দুটি টাইমস্ট্যাম্প বিয়োগ করলে Pandas একটি `TimedeltaIndex` তৈরি করে যার ভেতরের মান ন্যানোসেকেন্ড হিসেবে থাকে।
   
2. `df.duration = df.duration.apply(lambda td: td.total_seconds() / 60)`
   *(অথবা ভেক্টরাইজড পারফরম্যান্ট কোড: `df['duration'] = df['duration'].dt.total_seconds() / 60`)*
   - **কেন মিনিটে রূপান্তর?**: 
     - সেকেন্ডে রূপান্তর করলে মানগুলো অনেক বড় সংখ্যা হয়ে যায় (যেমন: ১৫ মিনিটের ট্রিপ = ৯০০ সেকেন্ড)। লিনিয়ার রিগ্রেশনের সমীকরণ $y = w^T X$ এ বড় টার্গেট স্কেল গ্রেডিয়েন্ট আপডেটে বড় স্টেপ সাইজ তৈরি করে।
     - অন্যদিকে ঘণ্টা এককে নিলে মানগুলো অতিরিক্ত ভগ্নাংশ হয়ে যায় (যেমন: ০.২৫ ঘণ্টা)।
     - ব্যবসায়িক দৃষ্টিকোণ থেকে একজন যাত্রী ও ড্রাইভারের কাছে ট্রিপ ডিউরেশনের সবচেয়ে স্বাভাবিক একক হলো **মিনিট**।

3. `df = df[(df.duration >= 1) & (df.duration <= 60)]`
   - **গাণিতিক গভীরতা**:
     - ডেটাসেট এক্সপ্লোর করলে দেখা যায় কিছু ট্রিপের ডিউরেশন নেগেটিভ (যেমন `-1.5` মিনিট)। এর কারণ ট্যাক্সি মিটারের ক্লক সিনক্রোনাইজেশন ফেইলিউর অথবা সফটওয়্যার বাগ।
     - কিছু ট্রিপের ডিউরেশন ১,০০০ থেকে ২০,০০০ মিনিট (কয়েক দিন থেকে সপ্তাহ)! ড্রাইভার হয়তো ট্রিপ শেষ করে ভুলবশত মিটার বন্ধ করেননি।
     - লিনিয়ার রিগ্রেশন অপটিমাইজেশনের জন্য স্কয়ারড লস ফাংশন ব্যবহার করে:
       $$L = \sum_{i=1}^N (y_i - \hat{y}_i)^2$$
     - যদি একটি রো-তে $y = 5000$ মিনিট থাকে এবং মডেল প্রেডিক্ট করে ২০ মিনিট, তবে একটিমাত্র রো-এর জন্য এরর হবে $(4980)^2 \approx 2.48 \times 10^7$!
     - এই দানবীয় এরর পুরো অপটিমাইজেশনকে ভুল পথে চালিত করবে।
     - ১ মিনিটের কম ট্রিপ কোনো বাস্তব যাত্রা নয় (যাত্রী ওঠার সাথে সাথে বাতিল করেছে)।
     - ৬০ মিনিটের ওপরের ট্রিপ মোট ডেটার ২%-এরও কম। তাই ১ থেকে ৬০ মিনিটের মধ্যে সীমাবদ্ধ রাখলে ৯৮% সুস্থ ও স্বাভাবিক ডেটা নিয়ে মডেল প্রশিক্ষণ গ্রহণ করে।

4. `df[categorical] = df[categorical].astype(str)`
   - **মারাত্মক প্রোডাকশন বাগ প্রতিরোধ**:
     - `PULocationID` কলামে মানগুলো ইনটিজার হিসেবে সংরক্ষিত (যেমন: ৪৩, ৮৬, ১২০)।
     - যদি আমরা এগুলোকে সরাসরি সংখ্যা হিসেবে মডেলে পাঠিয়ে দিই, তবে লিনিয়ার মডেল ধরে নেবে:
       $$\text{Effect}(\text{Location } 86) = 2 \times \text{Effect}(\text{Location } 43)$$
     - কিন্তু বাস্তবে Location 43 হলো সেন্ট্রাল পার্ক এবং Location 86 হলো সম্পূর্ণ ভিন্ন একটি আবাসিক জোন। এদের মধ্যে দ্বিগুণ বা তিনগুণের কোনো গাণিতিক সম্পর্ক নেই!
     - তাই `.astype(str)` দিয়ে এদেরকে টেক্সট স্ট্রিং (ক্যাটেগরি) হিসেবে ডিক্লেয়ার করা হলো, যাতে ভেক্টরাইজার এদের স্বতন্ত্র ওয়ান-হট ফিচার হিসেবে ট্রিট করে।

![Dataframe Inspection](images/05-train-duration-model-01-dataframe.jpg)

---

### ৪.৩ সেল ৬: টাইপ কাস্টিং ও বেসলাইন DictVectorizer

```python
# CELL 6
train_dicts = df[categorical + numerical].to_dict(orient='records')

dv = DictVectorizer()
X_train = dv.fit_transform(train_dicts)

target = 'duration'
y_train = df[target].values

lr = LinearRegression()
lr.fit(X_train, y_train)

y_pred = lr.predict(X_train)

root_mean_squared_error(y_train, y_pred)
```

#### 🔍 কোড কেন লেখা হলো?
1. `df[categorical + numerical].to_dict(orient='records')`:
   - প্রতিটি রো-কে একটি স্বাধীন পাইথন ডিকশনারিতে রূপান্তর করে:
     `[{'PULocationID': '43', 'DOLocationID': '151', 'trip_distance': 1.01}, ...]`
   - **কেন?**: প্রোডাকশনে যখন ক্লায়েন্ট কোনো ওয়েব সার্ভারে প্রেডিকশন রিকোয়েস্ট পাঠাবে, তখন সে কোনো ডেটাফ্রেম পাঠাবে না; সে পাঠাবে একটি JSON পে-লোড। এই ডিকশনারি ফরম্যাট প্রোডাকশন রিকোয়েস্টের সাথে ১০০% সংগতিপূর্ণ।
2. `dv.fit_transform(train_dicts)`:
   - এটি ডিকশনারিগুলো স্ক্যান করে প্রতিটি ইউনিক ক্যাটাগরির জন্য একটি নির্দিষ্ট কলাম ইনডেক্স বরাদ্দ করে এবং একটি কমপ্যাক্ট স্পার্স ম্যাট্রিক্স তৈরি করে।
3. `lr.fit(X_train, y_train)`:
   - সাধারণ OLS লিনিয়ার রিগ্রেশন ফিট করে।
4. `root_mean_squared_error(y_train, y_pred)`:
   - ট্রেনিং সেটের এরর পরিমাপ করে (প্রাথমিক বেসলাইনে এই এরর আসে প্রায় **৯.৮৩ মিনিট**)।

---

### ৪.৪ সেল ৭: রেসিডুয়াল ডিস্ট্রিবিউশন প্লট (Seaborn)

```python
# CELL 7
sns.distplot(y_pred, label='prediction')
sns.distplot(y_train, label='actual')

plt.legend()
```

#### 🔍 কোড কেন লেখা হলো?
- `y_train` বনাম `y_pred`-এর কার্ভ পাশাপাশি তুলনা করা।
- দেখা যায় যে আসল ডেটা (actual) একটি ভারী ডান-মুখী লেজযুক্ত ডিস্ট্রিবিউশন (Right-skewed log-normal type), যেখানে বেশিরভাগ ট্রিপ ৫-১৫ মিনিটের মধ্যে।
- লিনিয়ার রিগ্রেশনের প্রেডিকশন কার্ভ অনেক বেশি নরমাল/গাউসিয়ান বেল-কার্ভের মতো দেখায়।
- এটি প্রমাণ করে যে মডেলটি দীর্ঘ ট্রিপগুলোকে আন্ডার-এস্টিমেট করছে এবং খুব ছোট ট্রিপগুলোতে নেগেটিভ বা অতিরিক্ত প্রেডিক্ট করছে।

---

### ৪.৫ সেল ৮-১০: রিইউজেবল ফাংশন আর্কিটেকচার (`read_dataframe`)

```python
# CELL 8
def read_dataframe(filename):
    if filename.endswith('.csv'):
        df = pd.read_csv(filename)
        df.lpep_dropoff_datetime = pd.to_datetime(df.lpep_dropoff_datetime)
        df.lpep_pickup_datetime = pd.to_datetime(df.lpep_pickup_datetime)
    elif filename.endswith('.parquet'):
        df = pd.read_parquet(filename)

    df['duration'] = df.lpep_dropoff_datetime - df.lpep_pickup_datetime
    df.duration = df.duration.apply(lambda td: td.total_seconds() / 60)

    df = df[(df.duration >= 1) & (df.duration <= 60)]

    categorical = ['PULocationID', 'DOLocationID']
    df[categorical] = df[categorical].astype(str)
    
    return df

# CELL 9
df_train = read_dataframe('./data/green_tripdata_2021-01.parquet')
df_val = read_dataframe('./data/green_tripdata_2021-02.parquet')

# CELL 10
len(df_train), len(df_val)
```

#### 🔍 কোড কেন লেখা হলো?
- ট্রেনিং সেট এবং ভ্যালিডেশন সেটের জন্য কোড ডুপ্লিকেট না করে একটি ক্লিন, পুনঃব্যবহারযোগ্য ফাংশনে রূপান্তর করা হলো।
- জানুয়ারি ২০২১-এ ফিল্টারিংয়ের পর রো সংখ্যা আসে **৭৩,৯০৮** এবং ফেব্রুয়ারি ২০২১-এ আসে **৬১,১৫৩**।

---

### ৪.৬ সেল ১১-১২: ফিচার ক্রসিং (Feature Interaction: `PU_DO`)

```python
# CELL 11
df_train['PU_DO'] = df_train['PULocationID'] + '_' + df_train['DOLocationID']
df_val['PU_DO'] = df_val['PULocationID'] + '_' + df_val['DOLocationID']

# CELL 12
categorical = ['PU_DO'] #'PULocationID', 'DOLocationID']
numerical = ['trip_distance']

dv = DictVectorizer()

train_dicts = df_train[categorical + numerical].to_dict(orient='records')
X_train = dv.fit_transform(train_dicts)

val_dicts = df_val[categorical + numerical].to_dict(orient='records')
X_val = dv.transform(val_dicts)
```

#### 🔍 কোড কেন লেখা হলো? (কেন RMSE ৯.৮ থেকে ৫.৯ মিনিটে নেমে আসলো?)
1. **ফিচার ক্রসিংয়ের ম্যাথমেটিক্যাল কারণ**:
   - সাধারণ লিনিয়ার মডেল শেখে:
     $$\hat{y} = w_0 + w_{\text{PU}} \cdot x_{\text{PU}} + w_{\text{DO}} \cdot x_{\text{DO}} + w_{\text{dist}} \cdot x_{\text{dist}}$$
   - এখানে মডেল পিকআপ লোকেশনের একটি ফিক্সড প্রভাব এবং ড্রপঅফ লোকেশনের একটি ফিক্সড প্রভাব আলাদাভাবে যোগ করে।
   - কিন্তু বাস্তবে পিকআপ জোন ৪৩ থেকে ড্রপঅফ জোন ১০০-তে যাওয়ার যানজট ও দূরত্বের অভিজ্ঞতা সম্পূর্ণ ভিন্ন!
   - যখন আমরা স্ট্রিং কনক্যাটেনেশন দিয়ে `'43_100'` তৈরি করি, তখন মডেল প্রতিটি নির্দিষ্ট রুটের জন্য একটি স্বতন্ত্র ওয়ান-হট কো-এফিশিয়েন্ট ($w_{\text{route}}$) বরাদ্দ করতে পারে:
     $$\hat{y} = w_0 + w_{\text{43\_100}} + w_{\text{dist}} \cdot x_{\text{dist}}$$
   - এর ফলে লিনিয়ার মডেল নন-লিনিয়ার ইন্টারঅ্যাকশন ধারণ করতে পারে।
2. **`fit_transform` বনাম `transform`**:
   - লক্ষ্য করুন: `X_train`-এর জন্য `dv.fit_transform()` কিন্তু `X_val`-এর জন্য শুধুমাত্র `dv.transform()`!
   - এটি যদি ভুল করে ভ্যালিডেশন সেটেও `fit_transform` করা হতো, তবে মডেল ট্রেইনিং ও ভ্যালিডেশনের কলাম অ্যালাইনমেন্ট ভেঙে যেত এবং সম্পূর্ণ ধ্বংসাত্মক প্রেডিকশন তৈরি হতো।

![Features Representation](images/05-train-duration-model-02-features.jpg)

---

### ৪.৭ সেল ১৩-১৪: ভ্যালিডেশন সেটে ট্রেইন ও ইভ্যালুয়েশন

```python
# CELL 13
target = 'duration'
y_train = df_train[target].values
y_val = df_val[target].values

# CELL 14
lr = LinearRegression()
lr.fit(X_train, y_train)

y_pred = lr.predict(X_val)

root_mean_squared_error(y_val, y_pred)
```

#### 🔍 কোড কেন লেখা হলো?
- যখন শুধু আলাদাভাবে `PULocationID` ও `DOLocationID` দেওয়া হয়েছিল, তখন ভ্যালিডেশন RMSE ছিল প্রায় **১১.০ মিনিট**।
- যখন `PU_DO` ইন্টারঅ্যাকশন ফিচার দেওয়া হলো, তখন ভ্যালিডেশন RMSE নাটকীয়ভাবে কমে দাঁড়ায় মাত্র **৭.৭৯ মিনিট** (এবং ট্রেনিং RMSE প্রায় **৫.৯২ মিনিট**)!

![Linear Regression Training](images/05-train-duration-model-03-linear-regression.jpg)

---

### ৪.৮ সেল ১৫: মডেল ও প্রিপ্রসেসর সিরিয়ালাইজেশন (Pickle)

```python
# CELL 15
with open('models/lin_reg.bin', 'wb') as f_out:
    pickle.dump((dv, lr), f_out)
```

#### 🔍 কোড কেন লেখা হলো?
- **কেন একটি টাপলে দুটি অবজেক্ট?**:
  - `dv`: ডিকশনারি ভেক্টরাইজার যা ইনকামিং টেক্সট রুটগুলোকে স্পার্স কলামে রূপান্তর করতে জানে।
  - `lr`: লিনিয়ার রিগ্রেশন এস্টিমেটর যা সেই স্পার্স কলামের সাথে ওয়েট গুণ করে প্রেডিকশন দেয়।
  - যদি আমরা শুধুমাত্র `lr` সেভ করতাম, তবে প্রোডাকশন এপিআই কোনোভাবেই নতুন JSON রিকোয়েস্টকে সঠিক কলাম ইনডেক্সে রূপান্তর করতে পারত না। উভয়ে মিলে একটি একক পাইপলাইন তৈরি করে।

---

### ৪.৯ সেল ১৬: Lasso রিগ্রেশন ও L1 রেগুলারাইজেশন

```python
# CELL 16
lr = Lasso(0.01)
lr.fit(X_train, y_train)

y_pred = lr.predict(X_val)

root_mean_squared_error(y_val, y_pred)
```

#### 🔍 কোড কেন লেখা হলো?
- `PU_DO` ফিচার ক্রসিংয়ের ফলে ফিচারের সংখ্যা ৫২৫ থেকে বেড়ে **১৩,২২১**-এ পৌঁছায়!
- এর মধ্যে বহু রুট পুরো মাসে মাত্র ১ বা ২ বার উপস্থিত ছিল। সাধারণ লিনিয়ার রিগ্রেশন সেই ১-২টি ট্রিপের নয়েজ মুখস্থ করে ফেলে।
- `Lasso(alpha=0.01)` প্রয়োগের ফলে L1 পেনাল্টির কারণে হাজার হাজার অপ্রয়োজনীয় ও নয়েজি রুটের কো-এফিশিয়েন্ট সরাসরি **০.০০ (শূন্য)** হয়ে যায়। এটি ওভারফিটিং রোধ করে এবং মডেলকে হালকা রাখে।

---

## অধ্যায় ৫: ভেক্টরাইজেশন মেমরি আর্কিটেকচার: SciPy CSR Sparse Matrix

### ৫.১ কেন `pd.get_dummies` ব্যবহার করা প্রোডাকশনে নিষিদ্ধ?
Pandas-এর `pd.get_dummies(df)` ফাংশনটি টিউটোরিয়ালে খুব জনপ্রিয় হলেও বাস্তব MLOps ইঞ্জিনিয়ারিংয়ে এটি সম্পূর্ণ নিষিদ্ধ।

#### ১. ইনফারেন্স ক্র্যাশ (Column Mismatch):
- ধরুন, ট্রেইনিং ডেটাতে পিকআপ লোকেশন ছিল `{1, 2, 3}`। `pd.get_dummies` ৩টি কলাম বানাবে।
- প্রোডাকশনে এমন একজন যাত্রী আসলেন যার পিকআপ লোকেশন `4`। `pd.get_dummies` ৪টি কলাম বানাবে অথবা লোকেশন `2` অনুপস্থিত থাকলে মাত্র ২টি কলাম বানাবে।
- ফলশ্রুতিতে মডেল যখন ম্যাট্রিক্সটি গ্রহণ করবে, তখন ইনপুট শেপ মিসম্যাচ এরর (`ValueError: X has 2 features, but LinearRegression is expecting 3 features`) দিয়ে প্রোডাকশন সার্ভার ক্র্যাশ করবে।

#### ২. মেমরি ডিজাস্টার (Dense Allocation):
- `pd.get_dummies` মেমরিতে সম্পূর্ণ ডেন্স (Dense) ম্যাট্রিক্স তৈরি করে।
- ১৩,০০০ কলাম বিশিষ্ট একটি ডেটাফ্রেমে প্রতিটি রো-এর জন্য ১৩,০০০টি ফ্লোট মেমরিতে জায়গা নেয়, যার ৯৯.৯% মানই হলো ০।

---

### ৫.২ Compressed Sparse Row (CSR) মেমরি সেভিংস হিসাব

`DictVectorizer(sparse=True)` ব্যাকএন্ডে SciPy-এর **CSR (Compressed Sparse Row)** ম্যাট্রিক্স তৈরি করে।

```
[সাধারণ ডেন্স ম্যাট্রিক্স মেমরি অপচয়]
৭৩,৯০৮ টি রো  ×  ১৩,২২১ টি কলাম  ×  ৮ বাইট (float64)
= ৭,৮১৬,৯১২,৮৬৪ বাইট  ≈  ৭.৮২ গিগাবাইট (GB) RAM!

[CSR স্পার্স ম্যাট্রিক্স আর্কিটেকচার]
প্রতিটি রো-তে মাত্র ২টি অশূন্য উপাদান থাকে (একটি 'PU_DO', একটি 'trip_distance')।
মোট অশূন্য উপাদান = ৭৩,৯০৮ × ২ = ১৪৭,৮১৬ টি।
- Values array: ১৪৭,৮১৬ × ৮ বাইট ≈ ১.১৮ MB
- Column indices: ১৪৭,৮১৬ × ৪ বাইট ≈ ০.৫৯ MB
- Row pointers: ৭৩,৯০৯ × ৪ বাইট ≈ ০.৩০ MB
মোট সাইজ ≈ মাত্র ২.০৭ মেগাবাইট (MB)!
```
**ফলাফল**: ৭.৮২ গিগাবাইটের একটি বিশাল ডেটাসেট CSR ফরম্যাটে এসে মাত্র **২ মেগাবাইট** মেমরিতে নেমে আসে! এর ফলে কম দামি ক্লাউড সার্ভারেও অনায়াসে মডেল ট্রেইন করা সম্ভব হয়।

---

### ৫.৩ `fit_transform` বনাম `transform`: Data Leakage-এর বিস্তার

```
[Training Data]       ════► dv.fit_transform(train_dicts)  ════► Learns vocabulary & transforms to X_train
                                   │
                                   ▼ (Vocabulary frozen)
[Validation/Test Data] ═══► dv.transform(val_dicts)        ════► Uses existing vocabulary to transform to X_val
```

- **`fit`**: ডেটাসেট বিশ্লেষণ করে সমস্ত ইউনিক ক্যাটাগরি আবিষ্কার করে এবং ইন্টারনাল ডিকশনারিতে তাদের ইনডেক্স বরাদ্দ করে (`dv.vocabulary_`)।
- **`transform`**: বিদ্যমান ডিকশনারি ম্যাপিং ব্যবহার করে ডেটাকে ০ এবং ১ দিয়ে এনকোড করে।
- **নিয়ম**: ভ্যালিডেশন বা প্রোডাকশন ডেটাতে কখনোই `fit` বা `fit_transform` কল করা যাবে না। যদি ভ্যালিডেশন সেটে এমন কোনো নতুন রুট আসে যা ট্রেইনিংয়ে কখনো ছিল না, `DictVectorizer` নিরাপদে সেটিকে ০ হিসেবে হ্যান্ডেল করবে, কোনো এরর তৈরি করবে না।

---

## অধ্যায় ৬: অ্যালগরিদম ম্যাথমেটিক্স ও অপটিমাইজেশন থিওরি

### ৬.১ Ordinary Least Squares (OLS) ও Normal Equation

লিনিয়ার রিগ্রেশনের সমীকরণ:
$$\mathbf{y} = \mathbf{X}\mathbf{w} + \mathbf{\epsilon}$$
যেখানে:
- $\mathbf{X} \in \mathbb{R}^{N \times P}$ হলো ডিজাইন ম্যাট্রিক্স ($N$ টি স্যাম্পল, $P$ টি ফিচার)।
- $\mathbf{w} \in \mathbb{R}^{P}$ হলো মডেল প্যারামিটার (ওয়েটস)।
- $\mathbf{y} \in \mathbb{R}^{N}$ হলো টার্গেট ভ্যালু (ডিউরেশন)।

রেসিডুয়াল সাম অফ স্কয়ারস (Loss Function):
$$L(\mathbf{w}) = \|\mathbf{y} - \mathbf{X}\mathbf{w}\|_2^2 = (\mathbf{y} - \mathbf{X}\mathbf{w})^T (\mathbf{y} - \mathbf{X}\mathbf{w})$$

লস ফাংশনের গ্রেডিয়েন্ট নির্ণয়:
$$\nabla_{\mathbf{w}} L(\mathbf{w}) = -2 \mathbf{X}^T (\mathbf{y} - \mathbf{X}\mathbf{w}) = -2 \mathbf{X}^T \mathbf{y} + 2 \mathbf{X}^T \mathbf{X}\mathbf{w}$$

অপটিমাল সলিউশন পেতে গ্রেডিয়েন্টকে শূন্য ($0$) ধরা হয়:
$$-2 \mathbf{X}^T \mathbf{y} + 2 \mathbf{X}^T \mathbf{X}\mathbf{w} = 0 \implies \mathbf{X}^T \mathbf{X}\mathbf{w} = \mathbf{X}^T \mathbf{y}$$

যদি $\mathbf{X}^T \mathbf{X}$ নন-সিংগুলার এবং ইনভার্টিবল হয়, তবে আমরা পাই অ্যানালিটিক্যাল ক্লোজড-ফর্ম সলিউশন:
$$\mathbf{w}^* = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$$

---

### ৬.২ ইভ্যালুয়েশন মেট্রিক: RMSE বনাম MAE বনাম MAPE

| মেট্রিক | গাণিতিক সূত্র | চারিত্রিক বৈশিষ্ট্য | ট্যাক্সি ETA-তে ব্যবহারিক যৌক্তিকতা |
| :--- | :--- | :--- | :--- |
| **RMSE (Root Mean Squared Error)** | $\sqrt{\frac{1}{N}\sum (y_i - \hat{y}_i)^2}$ | বড় ভুলের জন্য স্কয়ারড পেনাল্টি দেয়; মূল টার্গেটের একই ইউনিটে (মিনিট) থাকে। | **বেস্ট চয়েস**: রাইড শেয়ারিংয়ে বড় ভুল যাত্রীর জন্য চরম বিপর্যয় ডেকে আনে, তাই বড় ভুলকে কঠোরভাবে শাস্তি দেওয়া প্রয়োজন। |
| **MAE (Mean Absolute Error)** | $\frac{1}{N}\sum \|y_i - \hat{y}_i\|$ | সব ভুলকে লিনিয়ারভাবে দেখে; আউটলায়ারের প্রতি রোবাস্ট। | মাঝারি ভুলের গড় বুঝতে ভালো, কিন্তু চরম বিপর্যয়গুলো হাইলাইট করে না। |
| **MAPE (Mean Absolute % Error)** | $\frac{1}{N}\sum \|\frac{y_i - \hat{y}_i}{y_i}\| \times 100$ | ভুলের শতকরা হার। | **মারাত্মক ঝুঁকি**: যখন প্রকৃত ট্রিপ ১ মিনিট ($y_i = 1$), মডেল যদি ৩ মিনিট প্রেডিক্ট করে, তবে এরর হয় ২০০%! কিন্তু বাস্তবে ভুল মাত্র ২ মিনিট। ছোট মানের ক্ষেত্রে এটি অস্বাভাবিকভাবে ফেটে যায়। |

---

### ৬.৩ রেগুলারাইজেশন থিওরি: Lasso ($L_1$) বনাম Ridge ($L_2$)

```
         Lasso (L1 Penalty)                     Ridge (L2 Penalty)
           Constraint Region                      Constraint Region
                w2                                     w2
                ▲                                      ▲
               / \                                   .---.
              /   \                                 /     \
             /     \                               |       |
      ◄─────◆───────◆─────► w1              ◄──────(───────)──────► w1
             \     /                                \     /
              \   /                                  '---'
               \ /
                ▼                                      ▼
   কৌণিক পয়েন্টগুলো এক্সিসকে স্পর্শ করে,         বৃত্তাকার কনট্যুর কখনো সহজে এক্সিসকে
   ফলে অনেক ওয়েট সরাসরি শূন্য (0) হয়ে যায়।       স্পর্শ করে না, ওয়েট ছোট হয় কিন্তু শূন্য হয় না।
```

1. **Lasso রিগ্রেশন ($L_1$ Regularization)**:
   $$\min_{\mathbf{w}} \frac{1}{2N} \|\mathbf{y} - \mathbf{X}\mathbf{w}\|_2^2 + \alpha \|\mathbf{w}\|_1 = \min_{\mathbf{w}} \frac{1}{2N} \sum_{i=1}^N (y_i - \mathbf{w}^T \mathbf{x}_i)^2 + \alpha \sum_{j=1}^P |w_j|$$
   - $L_1$ পেনাল্টি একটি বহুভুজ (Diamond) কনস্ট্রেইন্ট অঞ্চল তৈরি করে।
   - লস ফাংশনের উপবৃত্তাকার কনট্যুর যখন এই ডায়মন্ডের কোনো একটি শীর্ষবিন্দুতে (Vertex) আঘাত করে, তখন সংশ্লিষ্ট অ্যাক্সিস বরাবর কো-এফিশিয়েন্ট সরাসরি **০.০০** হয়ে যায়।
   - এটি মডেলের ভেতর স্বয়ংক্রিয়ভাবে **ফিচার সিলেকশন** সম্পন্ন করে।
2. **Ridge রিগ্রেশন ($L_2$ Regularization)**:
   $$\min_{\mathbf{w}} \frac{1}{2N} \|\mathbf{y} - \mathbf{X}\mathbf{w}\|_2^2 + \frac{\alpha}{2} \|\mathbf{w}\|_2^2$$
   - এটি কো-এফিশিয়েন্টগুলোকে শূন্যের দিকে টেনে নেয় কিন্তু কোনো কো-এফিশিয়েন্টকে হুট করে পুরোপুরি বাদ দেয় না।

---

## অধ্যায় ৭: কেন জুপিটার নোটবুক প্রোডাকশনের জন্য ক্ষতিকর এবং কীভাবে রিফ্যাক্টর করতে হয়

### ৭.১ নোটবুকের ৭টি মারাত্মক প্রোডাকশন ত্রুটি
1. **Hidden State ও নন-লিনিয়ার এক্সিকিউশন**: একজন ডেটা সায়েন্টিস্ট নোটবুকের ১০ নম্বর সেলের পর ৪ নম্বর সেল রান করতে পারেন। মেমরির ভ্যারিয়েবল স্টেট কোডের ওপর থেকে নিচে পড়ার ধারাবাহিকতার সাথে মেলে না।
2. **গ্লোবাল ভেরিয়েবল পলিউশন**: নোটবুকের প্রতিটি ভ্যারিয়েবল গ্লোবাল স্কোপে থাকে। ফাংশনের প্যারামিটার ছাড়া সরাসরি গ্লোবাল ডেটাফ্রেম রেফারেন্স করা মারাত্মক বাগ তৈরি করে।
3. **ইউনিট টেস্টিং অসম্ভব**: নোটবুকের ভেতরের কোনো সেলকে স্বয়ংক্রিয়ভাবে `pytest` দিয়ে টেস্ট করা যায় না।
4. **ভার্সন কন্ট্রোল বিপর্যয়**: `.ipynb` ফাইল মূলত বিশালাকার JSON ফাইল যাতে সেল আউটপুট, বেস৬৪ ইমেজ এবং মেটাডাটা থাকে। গিটহাবে দুটি শাখার কোড মার্জ করা অসম্ভব হয়ে পড়ে।
5. **হার্ডকোডেড পাথ**: `./data/green_tripdata_2021-01.parquet` সরাসরি কোডে লিখে রাখা হয়, যা ভিন্ন সার্ভারে বা ক্লাউড বাকেটে কাজ করে না।
6. **নো ইনপুট ভ্যালিডেশন**: কোনো টাইপ এনফোর্সমেন্ট বা স্কিমা ভ্যালিডেশন থাকে না।
7. **নো আর্টিফ্যাক্ট ট্র্যাকিং**: কোন ডেটাতে কোন হাইপারপ্যারামিটারে কত এরর এসেছিল তা মনে রাখা সম্ভব হয় না।

---

### ৭.২ ক্লিন আর্কিটেকচার ও মডুলারাইজেশন

প্রোডাকশন রূপান্তরের জন্য জুপিটার নোটবুককে নিচের ৪টি সুস্পষ্ট রেসপনসিবিলিটিতে ভাগ করা হয়:

```
[Production Script Hierarchy]
├── 1. Data Ingestion & Cleaning     (read_and_clean_data)
├── 2. Feature Extraction Pipeline   (extract_features)
├── 3. Training & Evaluation         (train_and_evaluate)
└── 4. Artifact Serialization        (save_artifacts)
```

![Notebook to Script Transition](images/06-course-overview-01-notebook.jpg)
![Training Pipeline Orchestration](images/06-course-overview-02-pipeline.jpg)
![Model Serving as a Service](images/06-course-overview-03-service.jpg)

---

## অধ্যায় ৮: প্রোডাকশন সার্ভিসিং মকআপ (FastAPI Integration)

মডেল সেভ করার পর প্রোডাকশন ওয়েব সার্ভার কীভাবে সেই `(dv, lr)` ব্যবহার করে ক্লায়েন্ট রিকোয়েস্ট প্রসেস করে, তার একটি লাইভ বাস্তবায়ন নিচে দেওয়া হলো:

```python
"""
Real-time Ride Duration Prediction API
Stack: FastAPI + Pydantic + Scikit-Learn
"""

from fastapi import FastAPI, HTTPException
from pydantic import BaseModel, Field
import pickle
import os

app = FastAPI(title="NYC Taxi Duration Prediction Service", version="1.0.0")

# মডেল আর্টিফ্যাক্ট লোড করা
MODEL_PATH = os.getenv("MODEL_PATH", "models/lin_reg.bin")

try:
    with open(MODEL_PATH, "rb") as f_in:
        dv, model = pickle.load(f_in)
except Exception as e:
    raise RuntimeError(f"মডেল লোড করতে ব্যর্থ: {str(e)}")


# ১. ইনপুট রিকোয়েস্টের Pydantic স্কিমা (Strict Type Validation)
class RideRequest(BaseModel):
    PULocationID: int = Field(..., description="Pickup Taxi Zone ID (1-265)", example=43)
    DOLocationID: int = Field(..., description="Dropoff Taxi Zone ID (1-265)", example=100)
    trip_distance: float = Field(..., gt=0.0, description="Trip distance in miles", example=3.5)


class PredictionResponse(BaseModel):
    predicted_duration_minutes: float
    model_version: str


@app.post("/predict", response_model=PredictionResponse)
def predict_duration(ride: RideRequest):
    try:
        # ২. ফিচার ক্রসিং তৈরি (ট্রেইনিং লজিকের হুবহু অনুরূপ)
        pu_do = f"{ride.PULocationID}_{ride.DOLocationID}"
        
        features = {
            "PU_DO": pu_do,
            "trip_distance": ride.trip_distance
        }

        # ৩. ভেক্টরাইজেশন (শুধুমাত্র transform, কখনোই fit নয়)
        X = dv.transform([features])

        # ৪. ইনফারেন্স
        prediction = model.predict(X)[0]

        # নেগেটিভ প্রেডিকশন হ্যান্ডলিং (প্রোডাকশন সেফগার্ড)
        duration = max(1.0, float(prediction))

        return PredictionResponse(
            predicted_duration_minutes=round(duration, 2),
            model_version="linear-regression-v1"
        )
    except Exception as e:
        raise HTTPException(status_code=500, detail=f"Inference error: {str(e)}")
```

---

## অধ্যায় ৯: MLOps ম্যাচিউরিটি মডেল (Level 0, 1, 2)

গুগল এবং মাইক্রোসফটের প্রস্তাবিত ফ্রেমওয়ার্ক অনুযায়ী MLOps পরিপক্বতার ৩টি স্তর:

```
[Level 0: Manual Process]
       │
       ▼ (Automate Training Pipeline via Prefect/Airflow)
[Level 1: ML Pipeline Automation - Continuous Training]
       │
       ▼ (Automate Testing, Docker Builds & CD Deployments)
[Level 2: Full CI/CD Automation & Live Monitoring]
```

### বিস্তারিত ম্যাট্রিক্স:
1. **Level 0 (Manual Process)**:
   - সমস্ত কাজ ডেটাসায়েন্টিস্টের লোকাল মেশিনে নোটবুকে চলে।
   - কোড শেয়ারিং হয় কপি-পেস্টের মাধ্যমে।
   - কোনো সেন্ট্রালাইজড মডেল রেজিস্ট্রি বা ট্র্যাকিং নেই।
   - রিলিজ সাইকেল অত্যন্ত ধীর (মাসে বা বছরে একবার)।
2. **Level 1 (ML Pipeline Automation - Continuous Training)**:
   - ডেটা ইনজেশন, ক্লিনিং, ফিচার ইঞ্জিনিয়ারিং ও মডেল ট্রেনিং একটি সুসংহত পাইপলাইন (Prefect/Kubeflow) দ্বারা পরিচালিত।
   - নতুন প্রোডাকশন ডেটা আসলে স্বয়ংক্রিয়ভাবে মডেল রি-ট্রেন হয়।
   - মডেল রেজিস্ট্রিতে মডেলের পারফরম্যান্স ও মেটাডাটা ভার্সন হিসেবে জমা হয়।
3. **Level 2 (Full CI/CD Pipeline Automation)**:
   - কোডবেসে কোনো পরিবর্তন এলে গিটহাব অ্যাকশনস স্বয়ংক্রিয়ভাবে ইউনিট টেস্ট ও ইন্টিগ্রেশন টেস্ট চালায়।
   - মডেল প্রি-প্রোডাকশন বেঞ্চমার্কে পাস করলে জিরো-ডাউনটাইম ক্যানারি বা ব্লু-গ্রিন ডেপ্লয়মেন্টের মাধ্যমে কুবারনেটিসে রিলিজ পায়।
   - প্রোডাকশনে ২৪/৭ ডেটা ড্রিফট, কনসেপ্ট ড্রিফট এবং এপিআই রেসপন্স টাইম মনিটর করা হয়।

---

## অধ্যায় ১০: মডিউল ১ হোমওয়ার্কের পুঙ্খানুপুঙ্খ গাণিতিক ও কোড সমাধান

হোমওয়ার্ক ১ নিউ ইয়র্ক সিটির **Yellow Taxi 2023** ডেটাসেটের ওপর ভিত্তি করে তৈরি।

### প্রশ্ন ১: ডেটাসেট ডাউনলোড ও কলাম সংখ্যা (Downloading the data)
- **কোড**:
  ```python
  import pandas as pd
  df = pd.read_parquet('yellow_tripdata_2023-01.parquet')
  print("কলামের সংখ্যা:", len(df.columns))
  ```
- **সঠিক উত্তর**: **19টি কলাম**।
- **ব্যাখ্যা**: গ্রিন ট্যাক্সির ২০টি কলামের বিপরীতে ২০২৩ সালের ইয়েলো ট্যাক্সি ডেটাতে ঠিক ১৯টি সুনির্দিষ্ট কলাম রয়েছে।

---

### প্রশ্ন ২: জানুয়ারি ২০২৩-এর ট্রিপ ডিউরেশনের স্ট্যান্ডার্ড ডেভিয়েশন (Standard Deviation)
- **কোড**:
  ```python
  df['duration'] = (df.tpep_dropoff_datetime - df.tpep_pickup_datetime).dt.total_seconds() / 60
  std_dev = df['duration'].std()
  print(f"স্ট্যান্ডার্ড ডেভিয়েশন: {std_dev:.2f}")
  ```
- **সঠিক উত্তর**: **42.59 মিনিট**।
- **গাণিতিক বিশ্লেষণ**:
  - মিন (Mean) যেখানে মাত্র ১৫.৬৭ মিনিট, সেখানে স্ট্যান্ডার্ড ডেভিয়েশন ৪২.৫৯ মিনিট কেন?
  - এর কারণ ডেটাসেটের চরম বৈষম্য ও আউটলায়ার। কিছু ট্রিপে মিটার চালু অবস্থায় গাড়ি গ্যারেজে পড়ে ছিল (কয়েক হাজার মিনিট ডিউরেশন)। এই চরম আউটলায়ারগুলো ভ্যারিয়েন্সকে ($\sigma^2$) অস্বাভাবিক বাড়িয়ে তোলে।

---

### প্রশ্ন ৩: ১ থেকে ৬০ মিনিটের ফিল্টারিংয়ের পর ডেটা রিটেনশন শতাংশ (Dropping outliers)
- **কোড**:
  ```python
  n_total = len(df)
  df_clean = df[(df.duration >= 1) & (df.duration <= 60)]
  fraction = len(df_clean) / n_total
  print(f"অবশিষ্ট ডেটা: {fraction * 100:.2f}%")
  ```
- **সঠিক উত্তর**: **98%**।
- **উপসংহার**: মাত্র ২% চরম অসঙ্গতিপূর্ণ ডেটা ড্রপ করে আমরা ৯৮% নিখুঁত ডেটা ধরে রাখতে সক্ষম হয়েছি।

---

### প্রশ্ন ৪: ভেক্টরাইজেশনের পর ফিচার ম্যাট্রিক্সের কলাম সংখ্যা (One-hot encoding)
- **কোড**:
  ```python
  categorical = ['PULocationID', 'DOLocationID']
  df_clean[categorical] = df_clean[categorical].astype(str)
  train_dicts = df_clean[categorical].to_dict(orient='records')
  
  dv = DictVectorizer()
  X_train = dv.fit_transform(train_dicts)
  print("ফিচার ম্যাট্রিক্সের কলাম সংখ্যা:", X_train.shape[1])
  ```
- **সঠিক উত্তর**: **515টি কলাম**।
- **ব্যাখ্যা**: NYC TLC-তে মোট ২৬৫টি সম্ভাব্য ট্যাক্সি জোন রয়েছে। জানুয়ারি ২০২৩-এর পিকআপ ও ড্রপঅফে সক্রিয় ইউনিক জোনের সংখ্যা যোগ হয়ে ঠিক ৫১৫টি বাইনারি ওয়ান-হট কলাম তৈরি করে।

---

### প্রশ্ন ৫: ট্রেনিং সেটে লিনিয়ার রিগ্রেশনের RMSE (Training a model)
- **কোড**:
  ```python
  from sklearn.linear_model import LinearRegression
  from sklearn.metrics import root_mean_squared_error

  y_train = df_clean['duration'].values
  lr = LinearRegression()
  lr.fit(X_train, y_train)

  y_pred_train = lr.predict(X_train)
  train_rmse = root_mean_squared_error(y_train, y_pred_train)
  print(f"Training RMSE: {train_rmse:.2f}")
  ```
- **সঠিক উত্তর**: **7.64 মিনিট**।

---

### প্রশ্ন ৬: ভ্যালিডেশন সেটে (ফেব্রুয়ারি ২০২৩) মডেলের RMSE (Evaluating the model)
- **কোড**:
  ```python
  # ১. ফেব্রুয়ারি ২০২৩ ডেটা লোড ও প্রি-প্রসেসিং
  df_val = pd.read_parquet('yellow_tripdata_2023-02.parquet')
  df_val['duration'] = (df_val.tpep_dropoff_datetime - df_val.tpep_pickup_datetime).dt.total_seconds() / 60
  df_val = df_val[(df_val.duration >= 1) & (df_val.duration <= 60)]
  df_val[categorical] = df_val[categorical].astype(str)

  # ২. শুধুমাত্র transform কল করা (fit ছাড়া)
  val_dicts = df_val[categorical].to_dict(orient='records')
  X_val = dv.transform(val_dicts)

  y_val = df_val['duration'].values
  y_pred_val = lr.predict(X_val)

  val_rmse = root_mean_squared_error(y_val, y_pred_val)
  print(f"Validation RMSE: {val_rmse:.2f}")
  ```
- **সঠিক উত্তর**: **7.81 মিনিট**।
- **বিশ্লেষণ**: ট্রেইনিং RMSE ৭.৬৪ এবং ভ্যালিডেশন RMSE ৭.৮১—উভয়ের ব্যবধান অত্যন্ত সামান্য (০.১৭ মিনিট)। এর অর্থ মডেলটিতে ওভারফিটিংয়ের কোনো লক্ষণ নেই এবং এটি একটি শক্তিশালী সাধারণীকরণ (Generalization) ক্ষমতা প্রদর্শন করেছে।

---

## অধ্যায় ১১: সম্পূর্ণ প্রোডাকশন পাইপলাইন পাইথন স্ক্রিপ্ট

নিচে সম্পূর্ণ পাইপলাইন কোডটি দেওয়া হলো। এটি টাইপ-অ্যানোটেড, প্রোডাকশন-রেডি এবং সরাসরি কমান্ড-লাইন থেকে এক্সিকিউটযোগ্য:

```python
"""
NYC Taxi Ride Duration Prediction Service
Module 1: End-to-End Production Baseline Pipeline
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

# ১. প্রোডাকশন লগিং সেটআপ
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s [%(levelname)s] %(name)s: %(message)s',
    handlers=[logging.StreamHandler(sys.stdout)]
)
logger = logging.getLogger("MLOps-Pipeline")


def load_and_preprocess_data(file_path: str) -> pd.DataFrame:
    """
    Parquet ফাইল থেকে ট্যাক্সি ডেটা পড়ে, ট্রিপ ডিউরেশন হিসাব করে
    এবং আউটলায়ার ফিল্টারিং সম্পন্ন করে।
    """
    if not os.path.exists(file_path):
        logger.error(f"ফাইল খুঁজে পাওয়া যায়নি: {file_path}")
        raise FileNotFoundError(f"File not found: {file_path}")

    logger.info(f"Parquet ফাইল লোড হচ্ছে: {file_path}")
    df = pd.read_parquet(file_path)
    initial_rows = len(df)

    # ট্রিপ ডিউরেশন মিনিট এককে রূপান্তর
    df['duration'] = (
        df['lpep_dropoff_datetime'] - df['lpep_pickup_datetime']
    ).dt.total_seconds() / 60

    # ১ থেকে ৬০ মিনিটের স্বাভাবিক ট্রিপ ফিল্টারিং
    df = df[(df.duration >= 1) & (df.duration <= 60)].copy()
    retained_rows = len(df)
    retention_rate = (retained_rows / initial_rows) * 100
    logger.info(
        f"আউটলায়ার রিমুভাল: {initial_rows} থেকে {retained_rows} রো রাখা হয়েছে "
        f"({retention_rate:.2f}% ডেটা অক্ষত)"
    )

    # ক্যাটাগরিক্যাল আইডিগুলোকে স্ট্রিংয়ে কাস্ট করা
    categorical_cols = ['PULocationID', 'DOLocationID']
    df[categorical_cols] = df[categorical_cols].astype(str)

    # ফিচার ক্রসিং: সুনির্দিষ্ট রুট তৈরি (Origin-Destination Pair)
    df['PU_DO'] = df['PULocationID'] + '_' + df['DOLocationID']

    return df


def engineer_features(
    df_train: pd.DataFrame, 
    df_val: pd.DataFrame, 
    categorical_cols: List[str], 
    numerical_cols: List[str]
) -> Tuple[csr_matrix, csr_matrix, DictVectorizer]:
    """
    DictVectorizer দিয়ে মেমরি-সাশ্রয়ী CSR স্পার্স ম্যাট্রিক্স তৈরি করে।
    ট্রেইনিং সেটে fit_transform এবং ভ্যালিডেশনে শুধুমাত্র transform করে।
    """
    logger.info("ফিচার ভেক্টরাইজেশন শুরু হচ্ছে...")
    dv = DictVectorizer()

    # ট্রেনিং ফিচার ম্যাট্রিক্স তৈরি
    train_records = df_train[categorical_cols + numerical_cols].to_dict(orient='records')
    X_train = dv.fit_transform(train_records)
    logger.info(f"X_train স্পার্স ম্যাট্রিক্স শেপ: {X_train.shape}")

    # ভ্যালিডেশন ফিচার ম্যাট্রিক্স তৈরি (Fit ছাড়া, শুধুই Transform)
    val_records = df_val[categorical_cols + numerical_cols].to_dict(orient='records')
    X_val = dv.transform(val_records)
    logger.info(f"X_val স্পার্স ম্যাট্রিক্স শেপ: {X_val.shape}")

    return X_train, X_val, dv


def train_baseline_models(
    X_train: csr_matrix, 
    y_train: pd.Series, 
    X_val: csr_matrix, 
    y_val: pd.Series
) -> Tuple[LinearRegression, Lasso]:
    """
    Linear Regression এবং Lasso Regression প্রশিক্ষণ ও মূল্যায়ন করে।
    """
    # ১. লিনিয়ার রিগ্রেশন
    logger.info("--- Linear Regression ট্রেইনিং ---")
    lr = LinearRegression()
    lr.fit(X_train, y_train)

    train_pred_lr = lr.predict(X_train)
    val_pred_lr = lr.predict(X_val)

    train_rmse_lr = root_mean_squared_error(y_train, train_pred_lr)
    val_rmse_lr = root_mean_squared_error(y_val, val_pred_lr)
    logger.info(f"Linear Regression -> Train RMSE: {train_rmse_lr:.2f} min | Val RMSE: {val_rmse_lr:.2f} min")

    # ২. লাসো রিগ্রেশন (L1 Regularization)
    logger.info("--- Lasso Regression (alpha=0.01) ট্রেইনিং ---")
    lasso = Lasso(alpha=0.01)
    lasso.fit(X_train, y_train)

    val_pred_lasso = lasso.predict(X_val)
    val_rmse_lasso = root_mean_squared_error(y_val, val_pred_lasso)
    logger.info(f"Lasso Regression    -> Val RMSE: {val_rmse_lasso:.2f} min")

    return lr, lasso


def serialize_pipeline(dv: DictVectorizer, model: LinearRegression, export_path: str) -> None:
    """
    প্রিপ্রসেসর এবং মডেলকে একটি যৌথ টাপলে বাইনারি ফাইলে সেভ করে।
    """
    os.makedirs(os.path.dirname(export_path), exist_ok=True)
    with open(export_path, 'wb') as f_out:
        pickle.dump((dv, model), f_out)
    logger.info(f"মডেল পাইপলাইন সফলভাবে সংরক্ষিত হয়েছে: {export_path} ✅")


def main():
    train_file = './data/green_tripdata_2021-01.parquet'
    val_file = './data/green_tripdata_2021-02.parquet'
    model_export_file = './models/lin_reg.bin'

    # ধাপ ১: ডেটা লোড ও প্রি-প্রসেস
    df_train = load_and_preprocess_data(train_file)
    df_val = load_and_preprocess_data(val_file)

    # ধাপ ২: ফিচার সিলেকশন
    categorical_features = ['PU_DO']
    numerical_features = ['trip_distance']

    # ধাপ ৩: ভেক্টরাইজেশন
    X_train, X_val, dv = engineer_features(
        df_train, df_val, categorical_features, numerical_features
    )

    y_train = df_train['duration'].values
    y_val = df_val['duration'].values

    # ধাপ ৪: মডেল ট্রেইনিং ও মূল্যায়ন
    best_lr_model, _ = train_baseline_models(X_train, y_train, X_val, y_val)

    # ধাপ ৫: প্রোডাকশন সেভিং
    serialize_pipeline(dv, best_lr_model, model_export_file)


if __name__ == '__main__':
    main()
```
