---
video_url: "https://www.youtube.com/watch?v=YWao0rnqVoI&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK&index=51"
code:
  - label: "Cloud end-to-end test"
    path: code/scripts/test_cloud_e2e.sh
  - label: "Kinesis integration test"
    path: code/integration-test/test_kinesis.py
prev_url: 09-terraform-pipeline-bn.md
next_url: 11-cicd-introduction-bn.md
---

# এন্ড-টু-এন্ড পাইপলাইন টেস্ট করা (Test the Pipeline End to End)

Terraform দিয়ে রিসোর্সগুলো সফলভাবে ডিপ্লয় করার পর, একটি টেস্ট রাইড ইভেন্ট পাঠিয়ে পুরো পাইপলাইন এন্ড-টু-এন্ড যাচাই করতে হবে। 
- ইভেন্টটি ইনপুট Kinesis স্ট্রিমে প্রবেশ করবে।
- এটি AWS Lambda-কে ট্রিগার করবে।
- Lambda S3 থেকে মডেল আর্টিফ্যাক্ট লোড করবে।
- প্রেডিকশন তৈরি করে আউটপুট স্ট্রিমে নতুন রেকর্ড পুশ করবে।

![The deployed pipeline ready for an end-to-end test](images/10-terraform-testing-01-pipeline.jpg)

---

## ১. টেস্ট রান এবং ফলাফল পর্যবেক্ষণ

- স্ক্রিপ্টে Run ID এবং স্ট্রিমগুলোর নাম সেট করুন।
- একটি পরিচিত (known) টেস্ট ইভেন্ট ইনপুট স্ট্রিমে পাঠান।
- Lambda এবং CloudWatch লগ পর্যবেক্ষণ করে প্রেডিকশন আউটপুট চেক করুন।
- টেস্টটি নিশ্চিত করবে কোন ইনপুটের প্রেক্ষিতে কোন প্রেডিকশন তৈরি হয়েছে এবং রেসপন্স স্ট্রাকচার প্রত্যাশার সাথে না মিললে টেস্টটি ফেইল করবে।

![Invoking the deployed pipeline](images/10-terraform-testing-02-invoke.jpg)

---

## ২. ডিপেন্ডেন্সি ট্র্যাকিং ও রিপ্রোডিউসিবিলিটি

Terraform কনফিগারেশন, অ্যাপ্লিকেশন ডকার ইমেজ, মডেল আর্টিফ্যাক্ট এবং টেস্ট ইভেন্ট—প্রত্যেকটি স্বতন্ত্র ডিপেন্ডেন্সি। প্রতিটি কম্পোনেন্টের সুনির্দিষ্ট ভার্সন রেকর্ড রাখুন, যেন টেস্ট ফেইল করলে সমস্যার কারণ নিখুঁতভাবে রিপ্রোডিউস এবং ডিবাগ করা যায়।
