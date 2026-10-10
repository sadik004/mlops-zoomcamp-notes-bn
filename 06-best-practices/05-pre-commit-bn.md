---
video_url: "https://www.youtube.com/watch?v=lmMZ7Axk2T8&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Pre-commit hooks"
    path: code/.pre-commit-config.yaml
prev_url: 04-linting-formatting-bn.md
next_url: 06-makefiles-bn.md
---

# গিট প্রি-কমিট হুকস (Git Pre-commit Hooks)

**Pre-commit Hooks** হলো এমন কিছু অটোমেটেড চেক যা `git commit` করার সাথে সাথেই নিজে থেকে রান করে। কোডে কোনো ফর্ম্যাটিং এরর বা টেস্ট ফেইলিওর থাকলে এটি কমিট হতে দেয় না—ফলে নষ্ট কোড গিটহাবে পুশ হওয়া আটকে যায়।

---

## ১. হুক কনফিগারেশন (`.pre-commit-config.yaml`)

আমাদের কনফিগারেশন ফাইলে নিচের হুকগুলো সাজানো থাকে:
- অপ্রয়োজনীয় হোয়াইটস্পেস কাটা এবং YAML সিনট্যাক্স ভ্যালিডেশন।
- বড় সাইজের ফাইল দুর্ঘটনাবশত কমিট হওয়া আটকানো।
- `isort`, `black`, `pylint` এবং `pytest` চালানো।

![প্রি-কমিট স্ক্রিপ্ট এবং হুক কনফিগারেশনের দৃশ্য](images/05-pre-commit-01-commands.jpg)

হুকগুলো সক্রিয় করতে টার্মিনালে চালান:
```bash
# হুক ইনস্টল করা
pre-commit install

# রিপোজিটরির সব ফাইলের ওপর একবার পরীক্ষা করা
pre-commit run --all-files
```

![প্রজেক্টের ভেতর প্রি-কমিট কনফিগারেশন ফাইল](images/05-pre-commit-02-config.jpg)

> [!TIP]
> প্রি-কমিট হলো লোকাল সেফটি নেট। তবে টিম মেম্বাররা যেন এটি বাইপাস না করতে পারে, সেজন্য একই চেকগুলো আমরা পরবর্তীতে GitHub Actions CI-তেও বাধ্যতামূলক করব।
