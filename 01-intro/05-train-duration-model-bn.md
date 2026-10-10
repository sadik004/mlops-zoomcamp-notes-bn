---
video_url: "https://www.youtube.com/watch?v=iRunifGSHFc&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Duration prediction notebook"
    path: duration-prediction.ipynb
prev_url: 04-read-parquet-bn.md
next_url: 06-course-overview-bn.md
---

# রাইড ডিউরেশন প্রেডিকশন মডেল ট্রেনিং (Training a Ride Duration Prediction Model)

এই পাঠে আমরা ট্যাক্সি রাইডের সময় প্রেডিক্ট করার জন্য প্রথম ভার্সনের মেশিন লার্নিং মডেলটি তৈরি করব। এই কোড সিকোয়েন্সটি অত্যন্ত গুরুত্বপূর্ণ, কারণ পরবর্তী মডিউলগুলোতে আমরা এই নোটবুকটিকে একটি সুশৃঙ্খল, ট্র্যাকড (MLflow) এবং ডিপ্লয়যোগ্য প্রোডাকশন পাইপলাইনে রূপান্তর করব।

---

## ১. ডেটা লোড ও প্রস্তুত করা (Load and prepare the data)

Pandas দিয়ে ২০২১ সালের জানুয়ারি ও ফেব্রুয়ারি মাসের ডেটা লোড করুন। আমরা **জানুয়ারি মাসের ডেটা ট্রেনিংয়ের জন্য** এবং **ফেব্রুয়ারি মাসের ডেটা ভ্যালিডেশনের (Validation) জন্য** ব্যবহার করব। ডেটাসেটের কলামগুলোর মধ্যে রয়েছে পিকআপ ও ড্রপ-অফের সময়, লোকেশন আইডি, ভ্রমণের দূরত্ব এবং যাত্রীর তথ্য।

![ট্রেনিং নোটবুকে লোড করা ট্যাক্সি ডেটাফ্রেম](images/05-train-duration-model-01-dataframe.jpg)

### টার্গেট ভ্যারিয়েবল (Target) তৈরি:
ড্রপ-অফের সময় থেকে পিকআপের সময় বিয়োগ করে ট্রিপের সময় (Duration) মিনিট এককে বের করুন। এছাড়া অস্বাভাবিক বা ভুল ডেটা (যেমন নেগেটিভ সময় বা ১০০ ঘণ্টার বেশি সময়) বাদ দিয়ে একটি নির্দিষ্ট স্বাভাবিক রেঞ্জের ডেটা ফিল্টার করুন।

```python
df['duration'] = (
    df['lpep_dropoff_datetime'] - df['lpep_pickup_datetime']
).dt.total_seconds() / 60
```

---

## ২. ফিচার ম্যাট্রিক্স তৈরি (Build the feature matrix)

মডেলের প্রথম ভার্সনে আমরা ৩টি ফিচার ব্যবহার করব:
- **PULocationID** (পিকআপ লোকেশন - ক্যাটেগরিক্যাল)
- **DOLocationID** (ড্রপ-অফ লোকেশন - ক্যাটেগরিক্যাল)
- **trip_distance** (ভ্রমণের দূরত্ব - নিউমেরিক্যাল)

লোকেশন আইডিগুলোকে ক্যাটেগরিক্যাল স্ট্রিং হিসেবে রূপান্তর করে `DictVectorizer` দিয়ে ওয়ান-হট এনকোডিং (One-Hot Encoding) করা হয়:

![লোকেশন ও দূরত্বের ফিচার প্রস্তুত করার স্ক্রিনশট](images/05-train-duration-model-02-features.jpg)

```python
from sklearn.feature_extraction import DictVectorizer

categorical = ['PULocationID', 'DOLocationID']
numerical = ['trip_distance']

# ডিকশনারিতে কনভার্ট করা
train_dicts = df[categorical + numerical].to_dict(orient='records')

dv = DictVectorizer()
X_train = dv.fit_transform(train_dicts)
```

> **সতর্কতা:** ভেক্টরাইজারটি শুধুমাত্র ট্রেনিং ডেটাতে `fit_transform` করবেন এবং পরবর্তীতে ভ্যালিডেশন ডেটাতে কেবল `transform` কল করবেন, যাতে উভয় ম্যাট্রিক্সে হুবহু একই ফিচার কলাম থাকে (Data Leakage রোধের জন্য)।

---

## ৩. বেসলাইন মডেল ট্রেন ও মূল্যায়ন (Train and evaluate a baseline)

একটি সাধারণ **Linear Regression** মডেল ফিট করুন এবং **RMSE (Root Mean Squared Error)** দিয়ে ভুলের মাত্রা পরিমাপ করুন:

```python
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

model = LinearRegression()
model.fit(X_train, y_train)

y_pred = model.predict(X_val)
rmse = mean_squared_error(y_val, y_pred, squared=False)
print(f"Validation RMSE: {rmse}")
```

![নোটবুকে লিনিয়ার রিগ্রেশন ফিট করা এবং বেসলাইন এরর হিসাব করার স্ক্রিনশট](images/05-train-duration-model-03-linear-regression.jpg)

এই বেসলাইন মডেলে সাধারণত ট্রেনিং এরর আসে প্রায় **৯ মিনিট** এবং ভ্যালিডেশন এরর আসে প্রায় **১০ মিনিট** (অর্থাৎ মডেলের প্রেডিকশন গড়ে প্রায় ৯-১০ মিনিট ভুল করে)। এটি আমাদের একটি বেসলাইন দেয় যা পরবর্তী মডিউলগুলোতে আরও উন্নত করা হবে।

আমরা Lasso রিগ্রেশন চালিয়ে বিভিন্ন `alpha` প্যারামিটার দিয়েও তুলনা করি। কিন্তু এভাবে ম্যানুয়ালি নোটবুকে রান চালালে মনে রাখা কঠিন হয়ে যায় কোন প্যারামিটারে কত এরর এসেছিল। **ঠিক এই সমস্যার সমাধানের জন্যই মডিউল ২-এ MLflow দিয়ে সব রানের ইতিহাস স্বয়ংক্রিয়ভাবে ট্র্যাক করা হবে।**
