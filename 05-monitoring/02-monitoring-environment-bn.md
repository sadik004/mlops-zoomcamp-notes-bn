---
video_url: "https://www.youtube.com/watch?v=yixA3C1xSxc&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Monitoring Compose stack"
    path: docker-compose.yml
  - label: "Monitoring requirements"
    path: requirements.txt
prev_url: 01-ml-monitoring-bn.md
next_url: 03-reference-model-bn.md
---

# মনিটরিং এনভায়রনমেন্ট সেটআপ (Environment Setup)

মনিটরিংয়ের জন্য আমরা একটি স্বয়ংসম্পূর্ণ লোকাল স্ট্যাক ব্যবহার করব:
- **Python / Evidently:** ড্রিফট ও কোয়ালিটি মেট্রিক্স হিসাব করবে।
- **PostgreSQL:** হিসাব করা মেট্রিক্স ডাটাবেজে সংরক্ষণ করবে।
- **Grafana:** ডাটাবেজ থেকে মেট্রিক্স নিয়ে লাইভ ভিজ্যুয়াল ড্যাশবোর্ডে প্রদর্শন করবে।
- **Adminer:** ব্রাউজার থেকে সহজে PostgreSQL টেবিল দেখার ওয়েব ইন্টারফেস।

---

## ১. পাইথন এনভায়রনমেন্ট তৈরি করা

একটি আলাদা এনভায়রনমেন্ট তৈরি করে প্রয়োজনীয় প্যাকেজ ইনস্টল করুন:

```bash
pip install -r requirements.txt
```

![মনিটরিং প্রজেক্ট ফাইল এবং পাইথন সেটআপের চিত্র](images/02-monitoring-environment-01-compose.jpg)

রেফারেন্স ডেটাসেট ও ট্রেইন্ড মডেল সংরক্ষণের জন্য লোকাল `data/` এবং `models/` ডিরেক্টরি ব্যবহার করা হয়।

---

## ২. ডকার কম্পোজ দিয়ে সার্ভিসগুলো চালু করা (Start the services)

`docker-compose.yml` ফাইলে PostgreSQL, Adminer এবং Grafana ডিফাইন করা রয়েছে। 

সার্ভিসগুলো চালু করতে টার্মিনালে রান করুন:

```bash
docker compose up -d
```

![Docker Compose-এ PostgreSQL এবং Grafana সার্ভিসসমূহ](images/02-monitoring-environment-02-services.jpg)

- **Grafana ড্যাশবোর্ড:** ব্রাউজারে যান `http://localhost:3000` (ইউজারনেম ও পাসওয়ার্ড: `admin` / `admin`)
- **Adminer ডাটাবেজ ভিউয়ার:** `http://localhost:8080`

![লোকাল Grafana মনিটরিং ড্যাশবোর্ড](images/02-monitoring-environment-03-dashboard.jpg)
