---
video_url: "https://www.youtube.com/watch?v=F6DZdvbRZQQ&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
code:
  - label: "Project Makefile"
    path: code/Makefile
prev_url: 05-pre-commit-bn.md
next_url: 07-terraform-introduction-bn.md
---

# Makefiles এবং অটোমেশন (Makefiles and make)

প্রজেক্টে টেস্টিং, লিন্টিং, ডকার বিল্ড এবং ডিপ্লয়মেন্টের জন্য অনেকগুলো দীর্ঘ কমান্ড থাকে। **Makefile** এই সব জটিল কমান্ডকে এক শব্দের সহজ শর্টকাটে রূপান্তর করে।

---

## ১. টার্গেট এবং ডিপেন্ডেন্সি (Targets and dependencies)

আমাদের `Makefile`-এ সংজ্ঞায়িত মূল কমান্ডসমূহ:
- `make test`: সব ইউনিট টেস্ট চালানো।
- `make quality_checks`: `isort`, `black`, এবং `pylint` চালানো।
- `make build`: ডকার ইমেজ বিল্ড করার আগে স্বয়ংক্রিয়ভাবে টেস্ট ও কোয়ালিটি চেক নিশ্চিত করা।
- `make integration_test`: ডকার কম্পোজ দিয়ে ইন্টিগ্রেশন টেস্ট রান করা।

![টার্গেট ও ডিপেন্ডেন্সি সহ Makefile-এর গঠন](images/06-makefiles-01-makefile.jpg)

ডেভেলপমেন্টের সময় টার্মিনালে শুধু `make test` বা `make build` লিখলেই সব কাজ ক্রমানুসারে সম্পন্ন হয়।

![টার্মিনালে Makefile টার্গেট রান করার দৃশ্য](images/06-makefiles-02-targets.jpg)
