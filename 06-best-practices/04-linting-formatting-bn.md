---
video_url: "https://www.youtube.com/watch?v=uImvWE-iSDQ&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Python project configuration"
    path: code/pyproject.toml
  - label: "Pre-commit configuration"
    path: code/.pre-commit-config.yaml
prev_url: 03-localstack-bn.md
next_url: 05-pre-commit-bn.md
---

# কোড কোয়ালিটি: লিন্টিং এবং ফরম্যাটিং (Code Quality: Linting and Formatting)

টেস্ট কোডের কার্যকারিতা যাচাই করে, আর **লিন্টিং (Linting)** ও **ফরম্যাটিং (Formatting)** কোডকে ক্লিন, সুন্দর এবং বাগ-মুক্ত রাখতে সাহায্য করে।

---

## ১. স্ট্যান্ডার্ড টুলস ব্যবহার করা

আমরা পাইথনের প্রধান তিনটি টুল ব্যবহার করি:
- **`isort`:** কোডের সব ইমপোর্টকে বর্ণানুক্রমে ও ক্যাটাগরি অনুযায়ী সাজিয়ে রাখে।
- **`black`:** পাইথন কোডকে ইন্ডাস্ট্রি-স্ট্যান্ডার্ড নিয়মে নিজে থেকেই ফরম্যাট করে দেয়।
- **`pylint` / `ruff`:** কোড কোয়ালিটি চেক করে এবং অপ্রয়োজনীয় ইমপোর্ট বা সম্ভাব্য সিনট্যাক্স ভুলগুলো চিহ্নিত করে।

সবগুলোর কনফিগারেশন `pyproject.toml` ফাইলে রাখা হয় যাতে লোকাল এবং গিটহাব CI উভয় জায়গায় একই নিয়ম কার্যকর হয়।

![প্রজেক্টে লিন্টিং এবং ফরম্যাটিং টুলস রান হওয়ার দৃশ্য](images/04-linting-formatting-01-lint.jpg)

টার্মিনালে এই টুলগুলো চালিয়ে ওয়ার্নিংগুলো ফিক্স করে ফেলুন।

![লিন্টিং এরর যেগুলো সমাধান করা প্রয়োজন](images/04-linting-formatting-02-errors.jpg)
