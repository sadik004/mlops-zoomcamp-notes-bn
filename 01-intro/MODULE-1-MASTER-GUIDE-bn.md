# মডিউল ১: সম্পূর্ণ মাস্টার গাইড ও ইঞ্জিনিয়ারিং হ্যান্ডবুক (Module 1 Master Guide)

> **লক্ষ্য**: মেশিন লার্নিং মডেলকে জুপিটার নোটবুকের পরীক্ষামূলক কোড থেকে প্রোডাকশন-রেডি সিস্টেমে রূপান্তর করার প্রথম ধাপ। এই গাইডে সম্পূর্ণ কোড, আর্কিটেকচার ডায়াগ্রাম এবং প্রতিটি কোড লাইনের পেছনের বাস্তব প্রকৌশলগত ও গাণিতিক কারণ (**"কোড কেন লেখা হলো"**) বিশদভাবে ব্যাখ্যা করা হয়েছে।

---

## সূচিপত্র (Table of Contents)
1. [MLOps পরিচিতি ও লাইফসাইকেল](#১-mlops-পরিচিতি-ও-লাইফসাইকেল)
2. [ডেভেলপমেন্ট এনভায়রনমেন্ট সেটআপ](#২-ডেভেলপমেন্ট-এনভায়রনমেন্ট-সেটআপ)
3. [ডেটাসেট ও Parquet ফরম্যাট হ্যান্ডলিং](#৩-ডেটাসেট-ও-parquet-ফরম্যাট-হ্যান্ডলিং)
4. [ডেটা প্রিপারেশন ও ফিচার ইঞ্জিনিয়ারিং ("কোড কেন লেখা হলো")](#৪-ডেটা-প্রিপারেশন-ও-ফিচার-ইঞ্জিনিয়ারিং-কোড-কেন-লেখা-হলো)
5. [ভেক্টরাইজেশন ও মডেল ট্রেইনিং ("কোড কেন লেখা হলো")](#৫-ভেক্টরাইজেশন-ও-মডেল-ট্রেইনিং-কোড-কেন-লেখা-হলো)
6. [মডেল ইভ্যালুয়েশন ও ডিস্ট্রিবিউশন প্লট](#৬-মডেল-ইভ্যালুয়েশন-ও-ডিস্ট্রিবিউশন-প্লট)
7. [মডেল আর্টিফ্যাক্ট সিরিয়ালাইজেশন (Pickle)](#৭-মডেল-আর্টিফ্যাক্ট-সিরিয়ালাইজেশন-pickle)
8. [নোটবুক থেকে প্রোডাকশন পাইপলাইনে ট্রানজিশন](#৮-নোটবুক-থেকে-প্রোডাকশন-পাইপলাইনে-ট্রানজিশন)
9. [MLOps ম্যাচিউরিটি মডেল (Maturity Levels)](#৯-mlops-ম্যাচিউরিটি-মডেল-maturity-levels)
10. [এক ক্লিকে রানযোগ্য সম্পূর্ণ পাইথন স্ক্রিপ্ট](#১০-এক-ক্লিকে-রানযোগ্য-সম্পূর্ণ-পাইথন-স্ক্রিপ্ট)

---

## ১. MLOps পরিচিতি ও লাইফসাইকেল

### ১.১ MLOps কী এবং কেন প্রয়োজন?
সাধারণ সফটওয়্যার ইঞ্জিনিয়ারিংয়ে কোড এবং রিকোয়ারমেন্ট ম্যানেজ করাই মূল কাজ। কিন্তু মেশিন লার্নিং সিস্টেমে তিনটি পরিবর্তনশীল উপাদান থাকে: **Code + Data + Model**। 
- ডেটা সময়ের সাথে পরিবর্তিত হয় (Data Drift)।
- বিজনেস ট্রেন্ড এবং বাহ্যিক পরিবেশ পরিবর্তিত হয় (Concept Drift)।
- শুধু জুপিটার নোটবুকে একটি মডেল ৯০% অ্যাকুরেসি অর্জন করলেই কাজ শেষ হয় না; যতক্ষণ না সেটি নির্ভরযোগ্যভাবে এপিআই হিসেবে ক্লায়েন্ট রিকোয়েস্ট হ্যান্ডেল করতে পারে এবং নিয়মিত মনিটর হয়।

![The Taxi Trip Prediction Problem](images/01-introduction-01-taxi-trip.jpg)

### ১.২ বিজনেস প্রবলেম স্টেটমেন্ট
নিউ ইয়র্ক সিটির ট্যাক্সি সার্ভিসের জন্য রাইড শুরুর সময় আমাদের প্রেডিক্ট করতে হবে: **ট্যাক্সিটির গন্তব্যে পৌঁছাতে আনুমানিক কত মিনিট সময় (duration) লাগবে?**
- ইনপুট: পিকআপ লোকেশন, ড্রপঅফ লোকেশন, পিকআপের সময়, ট্রিপ ডিসট্যান্স।
- আউটপুট: আনুমানিক ট্রিপের সময় (মিনিটে)।
- বিজনেস ভ্যালু: ট্যাক্সি ড্রাইভার ও যাত্রীদের সঠিক ভাড়া ও সময় প্রদর্শন, রুট অপটিমাইজেশন।

### ১.৩ ML সিস্টেমের তিনটি পর্যায় (Design, Train, Operate)
1. **Design**: সমস্যা চিহ্নিতকরণ, বিজনেস ম্যাট্রিক নির্ধারণ, ডেটা সোর্স আবিষ্কার।
2. **Train**: ডেটা ক্লিনিং, ফিচার ইঞ্জিনিয়ারিং, মডেল ট্রেনিং ও এক্সপেরিমেন্টেশন।
3. **Operate**: মডেল ডিপ্লয়মেন্ট, এপিআই সার্ভিসিং, কনটিনিউয়াস মনিটরিং ও রি-ট্রেইনিং।

![ML Deployment Architecture](images/01-introduction-02-deployment.jpg)
![Design, Train, Operate Lifecycle](images/01-introduction-03-design-train-operate.jpg)

---

## ২. ডেভেলপমেন্ট এনভায়রনমেন্ট সেটআপ

MLOps-এ যেকোনো পাইপলাইন তৈরির প্রথম শর্ত হলো **রিপ্রোডিউসিবল এনভায়রনমেন্ট**।

### ২.১ GitHub Codespaces
GitHub Codespaces ক্লাউডে প্রি-কনফিগার করা লিনাক্স কন্টেইনার সরবরাহ করে। এর ফলে লোকাল অপারেটিং সিস্টেম (Windows/Mac) নির্বিশেষে সব ডেভেলপার একই পাইথন সংস্করণ ও প্যাকেজ ব্যবহার করতে পারে।

![Codespaces Editor Interface](images/02-codespaces-01-editor.jpg)
![Codespaces Terminal Commands](images/02-codespaces-02-terminal.jpg)
![Codespaces Jupyter Extension](images/02-codespaces-03-jupyter.jpg)

### ২.২ AWS EC2 ভার্চুয়াল মেশিন সেটআপ
প্রোডাকশন-গ্রেড ট্রেনিংয়ের জন্য AWS EC2 ইনস্ট্যান্স (যেমন `t2.medium` বা `t3.large`) ব্যবহার করা হয়:
- **AMI**: Ubuntu Server LTS।
- **Key Pair**: নিরাপদ SSH অ্যাক্সেসের জন্য `.pem` ফাইল।
- **Docker**: কন্টেইনারাইজড সার্ভিস রান করার ইঞ্জিন।

![AWS EC2 AMI Selection](images/03-aws-vm-01-ami.jpg)
![AWS SSH Key Pair Configuration](images/03-aws-vm-02-key-pair.jpg)
![AWS Docker Service Setup](images/03-aws-vm-03-docker.jpg)

---

## ৩. ডেটাসেট ও Parquet ফরম্যাট হ্যান্ডলিং

### ৩.১ ডেটাসেট ডাউনলোড
NYC TLC (Taxi and Limousine Commission) ট্রিপ রেকর্ড থেকে জানুয়ারি ২০২১ এবং ফেব্রুয়ারি ২০২১-এর গ্রিন ট্যাক্সি ডেটা ডাউনলোড করা হয়:

```bash
mkdir data
wget https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2021-01.parquet -O data/green_tripdata_2021-01.parquet
wget https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2021-02.parquet -O data/green_tripdata_2021-02.parquet
```

![Dataset Download](images/04-read-parquet-01-download.jpg)

### ৩.২ কেন CSV নয়, Parquet ব্যবহার করা হলো?
| বৈশিষ্ট্য | CSV | Parquet | ইঞ্জিনিয়ারিং সুবিধা |
| :--- | :--- | :--- | :--- |
| **স্টোরেজ স্ট্রাকচার** | Row-oriented | Column-oriented | শুধুমাত্র প্রয়োজনীয় কলাম মেমরিতে লোড করা যায় |
| **কম্প্রেশন** | বড় ফাইল (অদক্ষ) | Snappy/Gzip কম্প্রেসড | ফাইলের সাইজ প্রায় ৭০-৮০% পর্যন্ত ছোট হয় |
| **স্কিমা ইন্টিগ্রিটি** | ডাটাটাইপ হারিয়ে যায় | কলাম টাইপ বিল্ট-ইন থাকে | ডেটা পড়ার সময় ডাটাটাইপ কাস্টিং এরর হয় না |
| **I/O গতি** | অত্যন্ত ধীর | অবিশ্বাস্য দ্রুত | গিগাবাইট ডেটাসেট কয়েক সেকেন্ডে লোড হয় |

### ৩.৩ পাইথনে Parquet রিড করা ও ইঞ্জিন এরর সমাধান
ডিফল্ট Pandas-এ Parquet পড়ার ইঞ্জিন বিল্ট-ইন থাকে না। তাই `pyarrow` বা `fastparquet` ইনস্টল করতে হয়।

```bash
pip install pyarrow fastparquet
```

![Missing Parquet Engine](images/04-read-parquet-02-missing-engine.jpg)
![Reading Data in Pandas](images/04-read-parquet-03-read-data.jpg)

---

## ৪. ডেটা প্রিপারেশন ও ফিচার ইঞ্জিনিয়ারিং ("কোড কেন লেখা হলো")

এই সেকশনে আমরা কোডের প্রতিটি ব্লক বিশ্লেষণ করব এবং জানব কেন এটি এভাবে লেখা হয়েছে।

```python
import pandas as pd

# ১. Parquet ফাইল মেমরিতে লোড
df = pd.read_parquet('./data/green_tripdata_2021-01.parquet')
```

### ৪.১ টার্গেট ভেরিয়েবল ক্যালকুলেশন (`duration`)

```python
df['duration'] = df.lpep_dropoff_datetime - df.lpep_pickup_datetime
df.duration = df.duration.apply(lambda td: td.total_seconds() / 60)
```

#### 🔍 কোড কেন লেখা হলো?
1. **টাইমস্ট্যাম্প ডিফারেন্স**: `lpep_dropoff_datetime` থেকে `lpep_pickup_datetime` বিয়োগ করলে আমরা পাই একটি Pandas `Timedelta` অবজেক্ট।
2. **মিনিটে রূপান্তর**: ব্যবসায়িক দিক থেকে ট্যাক্সি ট্রিপের সময় সেকেন্ডের চেয়ে **মিনিট** এককে হিসাব করা সবচেয়ে অর্থপূর্ণ। তাই `.total_seconds() / 60` দিয়ে সেকেন্ডকে ফ্লোটিং-পয়েন্ট মিনিটে রূপান্তর করা হয়েছে। এটিই আমাদের সুপারভাইজড লার্নিংয়ের টার্গেট ভেরিয়েবল ($y$)।

---

### ৪.২ আউ举报টলায়ার ফিল্টারিং (Outlier Removal)

```python
df = df[(df.duration >= 1) & (df.duration <= 60)]
```

#### 🔍 কোড কেন লেখা হলো?
ট্যাক্সি ট্রিপের ডেটাতে প্রায়শই সেন্সর ত্রুটি বা ক্যান্সেল হওয়া ট্রিপের অসঙ্গতি থাকে:
- **`duration < 1` মিনিট**: ড্রপঅফ হওয়ার ১ সেকেন্ডের মধ্যে ট্রিপ শেষ হওয়া বাস্তবসম্মত নয়; এগুলো বেশিরভাগ ক্ষেত্রেই ট্রিপ শুরু করেই বাতিল হওয়া ডেটা বা মিটার এরর।
- **`duration > 60` মিনিট**: ড্রাইভের সময় ভুলে মিটার চালু রেখে দেওয়া বা অস্বাভাবিক অস্বাভাবিক ডেটা যা মডেলের লস ফাংশনকে (MSE) স্কয়ারড পেনাল্টির কারণে বিভ্রান্ত করে।
- **সিদ্ধান্ত**: ১ থেকে ৬০ মিনিটের মধ্যে ডেটা সীমাবদ্ধ রাখলে মডেল ট্রিপের স্বাভাবিক প্যাটার্ন শিখতে পারে এবং গ্রেডিয়েন্ট এক্সপ্লোশন বা অস্বাভাবিক প্রেডিকশন তৈরি করে না।

---

### ৪.৩ ক্যাটেগরিক্যাল ফিচার কাস্টিং (Type Casting)

```python
categorical = ['PULocationID', 'DOLocationID']
numerical = ['trip_distance']

df[categorical] = df[categorical].astype(str)
```

#### 🔍 কোড কেন লেখা হলো?
- `PULocationID` (পিকআপ লোকেশন) এবং `DOLocationID` (ড্রপঅফ লোকেশন) আসলে পূর্ণসংখ্যা (যেমন `43`, `120`) হিসেবে স্টোর থাকে।
- **ভুলের আশঙ্কা**: যদি এগুলোকে সংখ্যা (`int` বা `float`) হিসেবে মডেলে পাঠানো হয়, তবে লিনিয়ার রিগ্রেশন ধরে নেবে: $\text{Location } 86 = 2 \times \text{Location } 43$! এটি মারাত্মক গাণিতিক ভুল।
- **সমাধান**: `.astype(str)` দিয়ে এগুলোকে স্ট্রিং বানিয়ে স্পষ্টভাবে **Categorical Variable** হিসেবে সংজ্ঞায়িত করা হলো, যাতে ভেক্টরাইজার এদের স্বতন্ত্র ক্যাটাগরি হিসেবে ওয়ান-হট এনকোডিং করতে পারে।

![Dataframe Inspection](images/05-train-duration-model-01-dataframe.jpg)

---

### ৪.৪ ফিচার ক্রসিং (Feature Interaction: `PU_DO`)

```python
df['PU_DO'] = df['PULocationID'] + '_' + df['DOLocationID']
categorical = ['PU_DO']
```

#### 🔍 কোড কেন লেখা হলো?
- আলাদাভাবে `PULocationID` জানা এবং আলাদাভাবে `DOLocationID` জানা মডেলকে কেবল স্থানটির গড় সময় বোঝায়।
- কিন্তু ট্রাফিক জ্যাম ও দূরত্বের আসল সত্য লুকিয়ে থাকে **নির্দিষ্ট রুট (OD Pair - Origin/Destination)**-এর মধ্যে! লোকেশন ৪৩ থেকে লোকেশন ১০০-তে যাওয়ার প্যাটার্ন সম্পূর্ণ আলাদা।
- দুটি স্ট্রিং যোগ করে `PU_DO` (যেমন `"43_100"`) ফিচার তৈরি করা হলো। একে মেশিন লার্নিংয়ের পরিভাষায় **Feature Crossing** বলা হয়। এর ফলে লিনিয়ার মডেল নন-লিনিয়ার ইন্টারঅ্যাকশন প্যাটার্ন শিখতে সক্ষম হয় এবং মডেলের RMSE উল্লেখযোগ্যভাবে হ্রাস পায়।

![Features Representation](images/05-train-duration-model-02-features.jpg)

---

## ৫. ভেক্টরাইজেশন ও মডেল ট্রেইনিং ("কোড কেন লেখা হলো")

### ৫.১ DictVectorizer ব্যবহার

```python
from sklearn.feature_extraction import DictVectorizer

train_dicts = df[categorical + numerical].to_dict(orient='records')

dv = DictVectorizer()
X_train = dv.fit_transform(train_dicts)
```

#### 🔍 কোড কেন লেখা হলো?
1. **ডিকশনারি স্ট্রাকচার**: `to_dict(orient='records')` প্রতিটি রো-কে একটি পাইথন ডিকশনারিতে রূপান্তর করে (যেমন `{'PU_DO': '43_100', 'trip_distance': 3.5}`). এটি প্রোডাকশন এপিআই-তে JSON রিকোয়েস্টের হুবহু অনুরূপ!
2. **স্পার্স ম্যাট্রিক্স (Sparse Matrix)**: ট্যাক্সি জোনের সংখ্যা শত শত হওয়ায় ওয়ান-হট এনকোডিং করলে হাজার হাজার কলাম তৈরি হয় যার ৯৯% ভ্যালু `0`। `DictVectorizer` স্বয়ংক্রিয়ভাবে অত্যন্ত মেমরি-সাশ্রয়ী **SciPy CSR Sparse Matrix** তৈরি করে, যা RAM ক্র্যাশ হওয়া প্রতিরোধ করে।
3. **`fit_transform` বনাম `transform`**:
   - ট্রেইনিং ডেটায় `dv.fit_transform()` ব্যবহার করা হয়, যা ট্রেইনিং ডেটার সব ইউনিক ক্যাটাগরি শিখে এবং এনকোড করে।
   - ভ্যালিডেশন বা প্রোডাকশন ডেটায় **শুধুমাত্র** `dv.transform()` ব্যবহার করতে হবে! নতুন ডেটাতে কখনোই `fit` করা যাবে না, অন্যথায় **Data Leakage** ঘটবে।

---

### ৫.২ বেসলাইন মডেল: লিনিয়ার রিগ্রেশন (Linear Regression)

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import root_mean_squared_error

target = 'duration'
y_train = df[target].values

lr = LinearRegression()
lr.fit(X_train, y_train)

y_pred = lr.predict(X_train)
train_rmse = root_mean_squared_error(y_train, y_pred)
print(f"Train RMSE: {train_rmse:.2f}")
```

#### 🔍 কোড কেন লেখা হলো?
- MLOps-এর গোল্ডেন রুল: **"সর্বদা সবচেয়ে সহজ মডেল দিয়ে বেসলাইন শুরু করুন।"**
- সরাসরি জটিল ডিপ লার্নিং বা XGBoost দিয়ে শুরু না করে Linear Regression দিয়ে দেখা হয় সাধারণ সমীকরণ $y = w^T X + b$ কতটা ভালো প্রেডিকশন দেয়।
- এর ফলে দ্রুত ফিডব্যাক পাওয়া যায় এবং ইনফারেন্স ল্যাটেন্সি মাত্র কয়েক মিলি-সেকেন্ডে সীমাবদ্ধ থাকে।

![Linear Regression Training](images/05-train-duration-model-03-linear-regression.jpg)

---

### ৫.৩ রেগুলারাইজেশন: Lasso রিগ্রেশন

```python
from sklearn.linear_model import Lasso

lr_lasso = Lasso(alpha=0.01)
lr_lasso.fit(X_train, y_train)

y_pred_val = lr_lasso.predict(X_val)
val_rmse = root_mean_squared_error(y_val, y_pred_val)
```

#### 🔍 কোড কেন লেখা হলো?
- `PU_DO` ফিচার ক্রসিংয়ের ফলে হাজার হাজার ফিচার তৈরি হওয়ায় কিছু রুট মাত্র ১-২ বার দেখা যেতে পারে, যা ওভারফিটিং তৈরি করে।
- **L1 Regularization (Lasso)**: পেনাল্টি টার্ম $\alpha \sum |w_i|$ যোগ করার মাধ্যমে অপ্রয়োজনীয় বা নয়েজি ফিচারের ওজন (weights) একেবারে **০ (zero)** বানিয়ে দেয়। এটি মডেলের সাইজ ছোট করে এবং ফিচার সিলেকশনের কাজ করে।

---

## ৬. মডেল ইভ্যালুয়েশন ও ডিস্ট্রিবিউশন প্লট

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
শুধু একটি একক সংখ্যা (RMSE = 6.99) দেখে সম্পূর্ণ সত্য বোঝা যায় না। প্রেডিকশন এবং আসল ডেটার কার্ভ পাশাপাশি প্লট করলে দেখা যায়:
- মডেল কি লম্বা ট্রিপগুলোকে আন্ডার-এস্টিমেট করছে?
- নাকি মাঝারিমানে বেশি পুঞ্জীভূত হচ্ছে?
- এই প্লট মডেলের বায়াস ও ভ্যারিয়েন্স বুঝতে সাহায্য করে।

---

## ৭. মডেল আর্টিফ্যাক্ট সিরিয়ালাইজেশন (Pickle)

```python
import os
import pickle

os.makedirs('models', exist_ok=True)
with open('models/lin_reg.bin', 'wb') as f_out:
    pickle.dump((dv, lr), f_out)
```

#### 🔍 কোড কেন লেখা হলো?
1. **টাপলে দুটি অবজেক্ট কেন? `(dv, lr)`**:
   - এটি একটি মারাত্মক প্রোডাকশন পিটফল! অনেক ডেভেলপার শুধু মডেল `lr` সেভ করে, কিন্তু ভেক্টরাইজার `dv` সেভ করতে ভুলে যায়।
   - প্রোডাকশন এপিআই যখন কাঁচা JSON পাবে, তখন ভেক্টরাইজার ছাড়া সেটিকে সংখ্যাসূচক ম্যাট্রিক্সে রূপান্তর করা অসম্ভব।
   - তাই প্রি-প্রসেসর `dv` এবং লার্নার `lr` একসাথে টাপল আকারে সেভ করা হলো যাতে ইনফারেন্স পাইপলাইনে কোনো বৈষম্য না ঘটে।
2. **বাইনারি মোড (`wb`)**: সিরিয়ালাইজড বাইনারি অবজেক্ট ডিস্কে সেভ করার নিরাপদ পদ্ধতি।

---

## ৮. নোটবুক থেকে প্রোডাকশন পাইপলাইনে ট্রানজিশন

জুপিটার নোটবুক এক্সপেরিমেন্টেশনের জন্য অসাধারণ, কিন্তু প্রোডাকশনের জন্য ক্ষতিকর কারণ:
- সেলগুলো উল্টাপাল্টা অর্ডারে রান করা যায় (Hidden State Bug)।
- অটোমেটেড টেস্টিং ও ভার্সন কন্ট্রোল করা যায় না।

তাই সব লজিককে ক্লাসিক্যাল সফটওয়্যার ইঞ্জিনিয়ারিংয়ের মতো **রিউজেবল পাইথন ফাংশনে** মোড়কজাত করা হয়:

```python
def read_dataframe(filename: str) -> pd.DataFrame:
    """Parquet বা CSV ফাইল থেকে ডেটা লোড করে ক্লিনিং সম্পন্ন করে।"""
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
```

![Notebook to Script Transition](images/06-course-overview-01-notebook.jpg)
![Training Pipeline Orchestration](images/06-course-overview-02-pipeline.jpg)
![Model Serving as a Service](images/06-course-overview-03-service.jpg)

---

## ৯. MLOps ম্যাচিউরিটি মডেল (Maturity Levels)

গুগল ও মাইক্রোসফটের প্রস্তাবিত স্ট্যান্ডার্ড অনুযায়ী MLOps তিনটি মূল স্তরে বিভক্ত:

```
[Level 0: Manual Process]
       │
       ▼ (Automate Training Pipeline)
[Level 1: ML Pipeline Automation]
       │
       ▼ (Automate CI/CD & Deployments)
[Level 2: Full CI/CD Pipeline Automation]
```

1. **Level 0 (Manual Process)**:
   - ডেটা সাইন্টিস্টরা নোটবুকে কোড লেখেন।
   - ম্যানুয়ালি ডেটা ডাউনলোড ও ক্লিন করা হয়।
   - মডেল ড্রপবক্স/ড্রাইভে ফাইল আকারে শেয়ার করা হয়। কোনো অটোমেশন নেই।
2. **Level 1 (ML Pipeline Automation)**:
   - নতুন ডেটা আসলেই স্বয়ংক্রিয়ভাবে মডেল ট্রেনিং পাইপলাইন রান হয় (Continuous Training - CT)।
   - কিন্তু মডেল ডিপ্লয়মেন্ট এখনো ম্যানুয়াল বা আংশিক স্ক্রিপ্টেড।
3. **Level 2 (Full CI/CD Automation)**:
   - কোড বা ডেটাতে যেকোনো পরিবর্তন হলে অটোমেটেড ইউনিট টেস্ট, ইন্টিগ্রেশন টেস্ট রান হয়।
   - প্রি-প্রোডাকশন গেট পাস করলে স্বয়ংক্রিয়ভাবে লাইভ সার্ভারে ডিপ্লয় হয় এবং ড্র্রিফট মনিটর করা হয়।

---

## ১০. এক ক্লিকে রানযোগ্য সম্পূর্ণ পাইথন স্ক্রিপ্ট

নিচে সম্পূর্ণ এন্ড-টু-এন্ড কোডটি দেওয়া হলো, যা কোনো নোটবুক ছাড়াই সরাসরি কমান্ড লাইন থেকে চালানো যাবে:

```python
"""
NYC Green Taxi Trip Duration Prediction Model
Module 1: End-to-End Production Baseline Pipeline
"""

import os
import pickle
import pandas as pd
from sklearn.feature_extraction import DictVectorizer
from sklearn.linear_model import LinearRegression, Lasso
from sklearn.metrics import root_mean_squared_error


def read_dataframe(filename: str) -> pd.DataFrame:
    """Parquet ফাইল পড়ে আউটলায়ার ফিল্টার ও ডাটা টাইপ কনভার্ট করে।"""
    print(f"Reading data from {filename}...")
    df = pd.read_parquet(filename)

    # ১. টার্গেট ভেরিয়েবল মিনিট এককে রূপান্তর
    df['duration'] = df.lpep_dropoff_datetime - df.lpep_pickup_datetime
    df.duration = df.duration.apply(lambda td: td.total_seconds() / 60)

    # ২. আউটলায়ার ফিল্টারিং (১ থেকে ৬০ মিনিটের ট্রিপ)
    df = df[(df.duration >= 1) & (df.duration <= 60)]

    # ৩. লোকেশন আইডিকে ক্যাটাগরিক্যাল স্ট্রিংয়ে রূপান্তর
    categorical = ['PULocationID', 'DOLocationID']
    df[categorical] = df[categorical].astype(str)

    # ৪. ফিচার ক্রসিং (রুট ফিচার তৈরি)
    df['PU_DO'] = df['PULocationID'] + '_' + df['DOLocationID']
    return df


def main():
    # ডেটা পাথ
    train_path = './data/green_tripdata_2021-01.parquet'
    val_path = './data/green_tripdata_2021-02.parquet'

    # ফাইল এক্সিস্টেন্স চেক
    if not os.path.exists(train_path) or not os.path.exists(val_path):
        raise FileNotFoundError(
            "Please download green_tripdata_2021-01.parquet and green_tripdata_2021-02.parquet into ./data/ folder."
        )

    # ডেটা প্রসেসিং
    df_train = read_dataframe(train_path)
    df_val = read_dataframe(val_path)

    print(f"Train records: {len(df_train)}, Validation records: {len(df_val)}")

    # ফিচার ডিফাইন
    categorical = ['PU_DO']
    numerical = ['trip_distance']

    # ভেক্টরাইজেশন (DictVectorizer)
    dv = DictVectorizer()

    train_dicts = df_train[categorical + numerical].to_dict(orient='records')
    X_train = dv.fit_transform(train_dicts)

    val_dicts = df_val[categorical + numerical].to_dict(orient='records')
    X_val = dv.transform(val_dicts)

    # টার্গেট এক্সট্রাকশন
    target = 'duration'
    y_train = df_train[target].values
    y_val = df_val[target].values

    # ১. লিনিয়ার রিগ্রেশন বেসলাইন
    print("\n--- Training Linear Regression Baseline ---")
    lr = LinearRegression()
    lr.fit(X_train, y_train)

    y_pred_val = lr.predict(X_val)
    val_rmse = root_mean_squared_error(y_val, y_pred_val)
    print(f"Linear Regression Validation RMSE: {val_rmse:.2f} minutes")

    # ২. লাসো রিগ্রেশন (L1 Regularization)
    print("\n--- Training Lasso Regression (alpha=0.01) ---")
    lasso = Lasso(alpha=0.01)
    lasso.fit(X_train, y_train)

    y_pred_lasso = lasso.predict(X_val)
    lasso_rmse = root_mean_squared_error(y_val, y_pred_lasso)
    print(f"Lasso Regression Validation RMSE: {lasso_rmse:.2f} minutes")

    # ৩. মডেল সেভ করা (Pre-processor + Estimator)
    os.makedirs('models', exist_ok=True)
    model_path = 'models/lin_reg.bin'
    with open(model_path, 'wb') as f_out:
        pickle.dump((dv, lr), f_out)
    print(f"\nSuccessfully serialized preprocessor and model to {model_path} ✅")


if __name__ == '__main__':
    main()
```
