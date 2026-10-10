# মডিউল ৬: হোমওয়ার্ক (Module 6 Homework)

এই হোমওয়ার্কে, আমরা মডিউল ৪-এ ব্যাচ মোডে ডিপ্লয় করা রাইড ডিউরেশন প্রেডিকশন মডেলটি নিয়ে কাজ করব এবং ইউনিট টেস্ট ও ইন্টিগ্রেশন টেস্টের মাধ্যমে কোডের নির্ভরযোগ্যতা (reliability) বৃদ্ধি করব।

স্টার্টার কোডটি পাওয়া যাবে [homework](https://github.com/DataTalksClub/mlops-zoomcamp/tree/main/cohorts/2025/06-best-practices/homework/) ডিরেক্টরিতে।

---

## প্রশ্ন ১: রিফ্যাক্টরিং (Refactoring)

কোড টেস্টে কভার করার আগে, এটিকে রিফ্যাক্টর করতে হবে। গ্লোবাল ভেরিয়েবলগুলো দূর করার মাধ্যমে আমরা শুরু করব।

- `year` এবং `month` প্যারামিটার নিয়ে একটি `main` ফাংশন তৈরি করুন।
- `read_data` ব্যতীত বাকি সমস্ত কোড `main`-এর ভেতর নিয়ে যান।
- `categorical`-কে `read_data`-এর একটি প্যারামিটার হিসেবে তৈরি করুন এবং `main`-এর ভেতর থেকে এটি পাস করুন।

এখন আমাদের "main" ব্লক তৈরি করতে হবে যেখান থেকে `main` ফাংশনটি ইনভোক করা হবে। এর জন্য আমরা যে `if` স্টেটমেন্ট ব্যবহার করব তা দেখতে কেমন হবে?

> **হিন্ট**: রিফ্যাক্টরিং করার পর, কোডটি এখনো সঠিকভাবে চলে কিনা তা পরীক্ষা করুন। যেমন মার্চ ২০২৩ এর ডেটা দিয়ে রান করে দেখুন এটি সফলভাবে শেষ হয় কিনা।  
> সহজে রান করার জন্য লোকাল ফাইলসিস্টেমে রেজাল্ট রাইট করতে পারেন:
> ```python
> output_file = f'taxi_type=yellow_year={year:04d}_month={month:02d}.parquet'
> ```

---

## প্রশ্ন ২: pytest ইনস্টলেশন (Installing pytest)

এখন আমাদের `pytest` ইনস্টল করতে হবে:

```bash
pipenv install --dev pytest
```

এরপর, একটি `tests` ফোল্ডার তৈরি করুন এবং তার ভেতর দুটি ফাইল তৈরি করুন। একটি হবে টেস্ট ফাইল, যার নাম দেওয়া যায় `test_batch.py`।

অন্য ফাইলটির নাম কী হওয়া উচিত?

> **হিন্ট**: `batch.py`-কে টেস্ট করার জন্য আমাদের এটি ইমপোর্ট করতে হবে। এই অন্য ফাইলটি ছাড়া পাইথন প্যাকেজ হিসেবে এটি ইমপোর্ট করা যাবে না।

---

## প্রশ্ন ৩: প্রথম ইউনিট টেস্ট লেখা (Writing first unit test)

এবার আমাদের কোড ইউনিট টেস্ট দিয়ে কভার করব।

`read_data`-এর ভেতরের প্রি-প্রসেসিং লজিক দিয়ে আমরা শুরু করব। এটি সরাসরি টেস্ট করা কঠিন কারণ এটি প্রথমে ফাইল রিড করে এবং তারপর কিছু ট্রান্সফরমেশন চালায়। আমাদের এই কোডটিকে দুটি অংশে ভাগ করতে হবে: রিডিং (I/O) এবং ট্রান্সফরমেশন।

একটি ফাংশন `prepare_data` তৈরি করুন যা একটি ডেটাফ্রেম (এবং কিছু অন্যান্য প্যারামিটার) ইনপুট নেয় এবং তাতে ট্রান্সফরমেশন প্রয়োগ করে। (এটি মূলত Parquet ফাইল রিড করার পর `read_data` ফাংশনের বাকি অংশ)।

এখন একটি টেস্ট তৈরি করুন এবং ইনপুট হিসেবে এটি ব্যবহার করুন:

```python
import pandas as pd
from datetime import datetime

def dt(hour, minute, second=0):
    return datetime(2023, 1, 1, hour, minute, second)

data = [
    (None, None, dt(1, 1), dt(1, 10)),
    (1, 1, dt(1, 2), dt(1, 10)),
    (1, None, dt(1, 2, 0), dt(1, 2, 59)),
    (3, 4, dt(1, 2, 0), dt(2, 2, 1)),      
]

columns = ['PULocationID', 'DOLocationID', 'tpep_pickup_datetime', 'tpep_dropoff_datetime']
df = pd.DataFrame(data, columns=columns)
```

প্রত্যাশিত আউটপুট ডিফাইন করুন এবং `assert` ব্যবহার করে নিশ্চিত করুন যে আসল ডেটাফ্রেম প্রত্যাশিত ডেটাফ্রেমের সাথে হুবহু মিলছে।

> **টিপ**: যখন আপনি দুটি Pandas ডেটাফ্রেম তুলনা করবেন, ফলাফলও একটি ডেটাফ্রেম হয়। একই কথা সিরিজ বা ডিকশনারির তালিকার ক্ষেত্রেও প্রযোজ্য।

প্রত্যাশিত ডেটাফ্রেমে কতগুলো সারি (rows) থাকা উচিত?

- 1
- 2
- 3
- 4

---

## প্রশ্ন ৪: LocalStack দিয়ে S3 মক করা (Mocking S3 with Localstack)

এবার ইন্টিগ্রেশন টেস্টের প্রস্তুতি নেওয়া যাক। আমাদের স্ক্রিপ্টে ডেটা S3-তে রাইট করা হয়, তাই S3 মক করার জন্য আমরা **LocalStack** ব্যবহার করব।

প্রথমে Docker Compose দিয়ে LocalStack রান করুন। শুধুমাত্র `localstack` সার্ভিস যুক্ত একটি `docker-compose.yaml` তৈরি করুন, যেখানে শুধু S3 সার্ভিস চলবে।

সার্ভিস চালু করুন এবং আউটপুট সংরক্ষণের জন্য "nyc-duration" নামের একটি বাকেট তৈরি করে পরীক্ষা করুন।

AWS CLI দিয়ে বাকেট তৈরি করার নিয়ম:

```bash
aws s3 mb s3://nyc-duration
```

এবং বাকেট তৈরি হয়েছে কিনা তা চেক করার নিয়ম:

```bash
aws s3 ls
```

উভয় ক্ষেত্রে LocalStack-এর জন্য কমান্ড এডজাস্ট করতে হবে। এর জন্য আমাদের কোন অপশনটি ব্যবহার করতে হবে?

- `--backend-store-uri`
- `--profile`
- `--endpoint-url`
- `--version`

---

## ইনপুট ও আউটপুট পাথ কনফিগারেবল করা

টেস্টিংয়ের সুবিধার জন্য এনভায়রনমেন্ট ভেরিয়েবলের মাধ্যমে `INPUT_FILE_PATTERN` এবং `OUTPUT_FILE_PATTERN` নির্ধারণ করুন:

```bash
export INPUT_FILE_PATTERN="s3://nyc-duration/in/{year:04d}-{month:02d}.parquet"
export OUTPUT_FILE_PATTERN="s3://nyc-duration/out/{year:04d}-{month:02d}.parquet"
```

এবং স্ক্রিপ্টে এভাবে লোড করুন:

```python
import os

def get_input_path(year, month):
    default_input_pattern = 'https://d37ci6vzurychx.cloudfront.net/trip-data/yellow_tripdata_{year:04d}-{month:02d}.parquet'
    input_pattern = os.getenv('INPUT_FILE_PATTERN', default_input_pattern)
    return input_pattern.format(year=year, month=month)

def get_output_path(year, month):
    default_output_pattern = 's3://nyc-duration-prediction-alexey/taxi_type=fhv/year={year:04d}/month={month:02d}/predictions.parquet'
    output_pattern = os.getenv('OUTPUT_FILE_PATTERN', default_output_pattern)
    return output_pattern.format(year=year, month=month)
```

---

## Pandas দিয়ে LocalStack S3 থেকে রিড করা

LocalStack S3 থেকে Parquet ফাইল পড়ার জন্য এন্ডপয়েন্ট URL উল্লেখ করতে হবে:

```python
options = {
    'client_kwargs': {
        'endpoint_url': S3_ENDPOINT_URL
    }
}

df = pd.read_parquet('s3://bucket/file.parquet', storage_options=options)
```

আমাদের `read_data` ফাংশন মডিফাই করুন:
- যদি `S3_ENDPOINT_URL` সেট করা থাকে, তবে এটি রিড করার জন্য ব্যবহার করুন।
- অন্যথায় সাধারণ পদ্ধতি ব্যবহার করুন।

---

## প্রশ্ন ৫: টেস্ট ডেটা তৈরি করা (Creating test data)

এখন `integration_test.py` তৈরি করুন।

আমরা প্রশ্ন ৩-এ তৈরি করা ডেটাফ্রেমটি ব্যবহার করব এবং এটি LocalStack S3-তে সংরক্ষণ করব। আমরা ধরে নেব এটি জানুয়ারি ২০২৩ এর ডেটা।

স্ক্রিপ্টটি রান করার পর AWS CLI দিয়ে ফাইলটি তৈরি হয়েছে কিনা তা যাচাই করুন:

ফাইল সেভ করার জন্য নিচের স্নিপেট ব্যবহার করুন:

```python
df_input.to_parquet(
    input_file,
    engine='pyarrow',
    compression=None,
    index=False,
    storage_options=options
)
```

ফাইলটির সাইজ (সাইজ ইন বাইটস) কত?

- 3620
- 23620
- 43620
- 63620

---

## প্রশ্ন ৬: ইন্টিগ্রেশন টেস্ট সম্পন্ন করা (Finish the integration test)

LocalStack S3 থেকে রিড করার পাশাপাশি আমাদের সেখানে রাইটও করতে হবে।

`read_data`-এর মতো একটি ফাংশন `save_data` তৈরি করুন যা দিয়ে ডেটাফ্রেম সেভ করা যায়।

এবার জানুয়ারি ২০২৩ এর ফেক ডেটার জন্য `batch.py` স্ক্রিপ্টটি চালান (পাইথনের `os.system` ব্যবহার করতে পারেন)।

এখন প্রেডিকশনের রেজাল্টটি রিড করুন এবং ফলাফল ভেরিফাই করুন।

টেস্ট ডেটাফ্রেমের প্রেডিক্ট করা ডিউরেশনগুলোর মোট যোগফল (sum) কত?

- 13.08
- 36.28
- 69.28
- 81.08

---

## সাবমিশন (Submission)

- ফলাফল জমা দেওয়ার লিঙ্ক: [Courses DataTalksClub Module 6 HW](https://courses.datatalks.club/mlops-zoomcamp-2025/homework/hw6)
