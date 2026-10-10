---
video_url: "https://www.youtube.com/watch?v=iaJz-T7VWec&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Duration prediction notebook"
    path: duration-prediction.ipynb
prev_url: 02-mlflow-getting-started-bn.md
next_url: 04-model-management-bn.md
---

# MLflow দিয়ে এক্সপেরিমেন্ট ট্র্যাকিং (Experiment Tracking with MLflow)

নোটবুকে ম্যানুয়ালি `alpha` বা হাইপারপ্যারামিটার পরিবর্তন করলে আগের ফলাফলের ইতিহাস হারিয়ে যায়। MLflow প্রতিটি ট্রায়ালকে একটি অনন্য **Run** হিসেবে রেজিস্টার করে এবং প্রয়োজনীয় সকল মান সংরক্ষণ করে যাতে পরবর্তীতে পাশাপাশি রেখে তুলনা করা যায়।

---

## ১. অবজেক্টিভ ফাংশন নির্ধারণ (Define the objective)

স্বয়ংক্রিয় হাইপারপ্যারামিটার টিউনিংয়ের জন্য (Hyperopt ব্যবহার করে) আমরা একটি `objective` ফাংশন তৈরি করি। এই ফাংশনটি এক সেট প্যারামিটার গ্রহণ করে, মডেল ট্রেন করে এবং ভ্যালিডেশন ডেটাসেটে **RMSE** হিসাব করে রিটার্ন করে। অপটিমাইজার এই RMSE মানকে সর্বনিম্ন (minimize) করার চেষ্টা করে এবং প্রতিটি ট্রায়ালের তথ্য MLflow-তে লগ করে।

![মডেল টিউনিংয়ের জন্য ব্যবহৃত হাইপারপ্যারামিটার সার্চ স্পেস](images/03-experiment-tracking-01-search-space.jpg)

- **Search Space:** অপটিমাইজার কোন কোন রেঞ্জে মানগুলো পরীক্ষা করবে তা নির্ধারণ করা হয়। যেমন: `max_depth` হতে পারে ৪ থেকে ১০ এর মধ্যে পূর্ণসংখ্যা, আর `learning_rate` হতে পারে লগারিদমিক স্কেল।

---

## ২. প্রতিটি রান লগ করা (Log each run)

অবজেক্টিভ ফাংশনের ভেতরে `mlflow.start_run()` দিয়ে একটি রান শুরু করা হয় এবং যেসব প্যারামিটার ও ডেটা ফলাফলকে প্রভাবিত করে সেগুলো লগ করা হয়:

```python
with mlflow.start_run():
    # সব হাইপারপ্যারামিটার ডিকশনারি একবারে লগ করা
    mlflow.log_params(params)
    
    # রেজাল্ট বা মেট্রিক লগ করা
    mlflow.log_metric('rmse', rmse)
    
    # ডেটাসেটের পাথ লগ করা
    mlflow.log_param('train_data', train_data_path)
    mlflow.log_param('valid_data', valid_data_path)
```

![MLflow UI-তে পাশাপাশি একাধিক টিউনিং রানের তুলনা](images/03-experiment-tracking-02-comparison.jpg)

MLflow ড্যাশবোর্ডে গিয়ে আপনি ফিল্টার করতে পারেন এবং দেখতে পারেন কোন কোন হাইপারপ্যারামিটারে RMSE সবচেয়ে কম এসেছে। এছাড়া রানের শুরু হওয়ার সময়, কত সেকেন্ড সময় লেগেছে এবং কে রান করেছে—সব স্বয়ংক্রিয়ভাবে রেকর্ড হয়।

---

## ৩. সেরা মডেলটি নির্বাচন ও সংরক্ষণ (Select and save the best model)

সবগুলো ট্রায়ালের পর যখন সবচেয়ে সেরা প্যারামিটারগুলো পেয়ে যাই, তখন সেই সেরা মানগুলো দিয়ে একটি ফাইনাল মডেল ট্রেন করা হয়। এরপর ফাইনাল প্যারামিটার, অর্জিত RMSE এবং ট্রেইন্ড মডেল আর্টফ্যাক্ট MLflow-তে লগ করা হয়।

![MLflow-তে নির্বাচিত সেরা প্যারামিটার এবং লগ করা ফাইনাল রান](images/03-experiment-tracking-03-best-params.jpg)
