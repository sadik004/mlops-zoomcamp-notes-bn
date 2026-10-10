---
video_url: "https://www.youtube.com/watch?v=CJp1eFQP5nk&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Python model service"
    path: code/model.py
  - label: "pytest model tests"
    path: code/tests/model_test.py
prev_url: ../05-monitoring/10-monitoring-example-bn.md
next_url: 02-docker-compose-tests-bn.md
---

# পাইথন কোড টেস্টিং: pytest (Testing Python Code with pytest)

বেস্ট প্র্যাকটিসের প্রথম ধাপ হলো পুরো ক্লাউড ইনফ্রাস্ট্রাকচারে ডিপ্লয় না করেই লোকাল মেশিনে মডেলের কোড যাতে টেস্ট করা যায় তা নিশ্চিত করা।

---

## ১. লজিককে ক্লাউড ইনফ্রা থেকে আলাদা করা (Separate logic from infrastructure)

ফিচার প্রিপারেশন এবং মডেল প্রেডিকশনের মূল পাইথন লজিককে ক্লাউড SDK (যেমন AWS Kinesis বা S3) থেকে আলাদা ফাংশনে রাখুন:
- ক্লাউড কলগুলো থাকবে শুধু ইন্টিগ্রেশন বাউন্ডারিতে।
- মূল ফাংশন যেন কোনো ক্লাউড ক্রেডেনশিয়াল বা ইন্টারনেট কানেকশন ছাড়াই একটি সাধারণ ডিকশনারি ইনপুট নিয়ে প্রেডিকশন দিতে পারে।

![স্ট্রিমিং, Lambda মডেল সার্ভিস এবং প্রেডিকশন পাথ আর্কিটেকচার](AWS-stream-pipeline.png)

---

## ২. pytest দিয়ে ইউনিট টেস্ট চালানো

`pytest` দিয়ে টেস্ট লিখলে প্রত্যাশিত ইনপুট ও আউটপুট একদম স্পষ্ট থাকে:

```python
def test_prepare_features():
    ride = {
        "PULocationID": 10,
        "DOLocationID": 50,
        "trip_distance": 40
    }
    actual_features = prepare_features(ride)
    expected_features = {
        "PU_DO": "10_50",
        "trip_distance": 40
    }
    assert actual_features == expected_features
```

টার্মিনালে কমান্ড দিন:
```bash
pytest tests/
```

![মডেল সার্ভিস এবং তার pytest টেস্ট পাসের ফলাফল](images/01-pytest-02-model-service.jpg)

কোনো ক্লাউড অ্যাকাউন্ট বা খরচ ছাড়াই কোডের প্রতিটি পরিবর্তনের পর লোকালি ইউনিট টেস্ট রান করা সম্ভব।
