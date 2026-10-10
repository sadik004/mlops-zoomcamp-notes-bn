---
video_url: "https://www.youtube.com/watch?v=IXSiYkP23zo&list=PL3MmuxUbc_hIUISrluw_A7wDSmfOhErJK"
prev_url: 02-codespaces-bn.md
next_url: 04-read-parquet-bn.md
---

# এডব্লিউএস ভার্চুয়াল মেশিন সেটআপ (VM in AWS)

আপনি চাইলে আপনার লোকাল কম্পিউটার, GitHub Codespaces অথবা যেকোনো ক্লাউড প্রোভাইডার ব্যবহার করতে পারেন। এই গাইডে আমরা একটি **AWS EC2** মেশিন কনফিগারেশন দেখাব। আমরা Linux (Ubuntu) ব্যবহার করার পরামর্শ দিই, কারণ এতে কোর্সের সব কমান্ড ও টুলস কোনো জটিলতা ছাড়া সহজে চালানো যায়।

---

## ১. একটি EC2 ইন্সট্যান্স তৈরি করা (Create an EC2 instance)

AWS কনসোল থেকে EC2 ড্যাশবোর্ড ওপেন করে **Launch Instance**-এ ক্লিক করুন। 
- অপারেটিং সিস্টেম হিসেবে **Ubuntu** সিলেক্ট করুন।
- আর্কিটেকচার হিসেবে **x86** নির্বাচন করুন (ARM এড়িয়ে চলুন, কারণ কিছু পাইথন ও MLOps প্যাকেজ ARM-এ ঝামেলা করতে পারে)।
- ইন্সট্যান্স টাইপ নির্বাচনের সময় এমন একটি মেশিন বেছে নিন যাতে পর্যাপ্ত RAM থাকে (জুপিটার নোটবুক, ডকার ও MLflow একসাথে চালানোর জন্য ফ্রি-টিয়ার `t2.micro` অনেক সময় আটকে যেতে পারে; মাঝারি সাইজ যেমন `t3.medium` বা `t3.large` ভালো)।

![Ubuntu এবং x86 আর্কিটেকচার সিলেক্ট করা অবস্থায় EC2 লঞ্চ স্ক্রিন](images/03-aws-vm-01-ami.jpg)

একটি **Key Pair** তৈরি বা সিলেক্ট করুন। প্রাইভেট কি (`.pem` ফাইল) ডাউনলোড করে আপনার লোকাল কম্পিউটারের `.ssh` ডিরেক্টরিতে নিরাপদে রাখুন। এটি ব্যবহারের আগে ফাইলটির পারমিশন সীমাবদ্ধ করতে হবে।

কি (Key) ফাইলটি ব্যবহারের পূর্বে টার্মিনালে নিচের কমান্ডটি চালান:

```bash
chmod 400 name-of-your-private-key-file.pem
```

![টার্মিনালে `.ssh` ডিরেক্টরির ভেতরে ডাউনলোড করা SSH Key](images/03-aws-vm-02-key-pair.jpg)

এরপর SSH দিয়ে আপনার রিমোট ইন্সট্যান্সে কানেক্ট করুন এবং ডেভেলপমেন্ট টুলস ইনস্টল করুন।

---

## ২. ডকার ইনস্টল করা (Install Docker)

Ubuntu-এর অফিসিয়াল রিপোজিটরি থেকে Docker এবং Anaconda ইনস্টল করার কমান্ডসমূহ:

```bash
# Anaconda ডাউনলোড ও ইনস্টলেশন
wget https://repo.anaconda.com/archive/Anaconda3-2022.05-Linux-x86_64.sh
bash Anaconda3-2022.05-Linux-x86_64.sh

# Docker প্যাকেজ ও প্রয়োজনীয় ডিপেন্ডেন্সি
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# রুট ইউজার (sudo) ছাড়া Docker চালানোর অনুমতি
sudo groupadd docker
sudo usermod -aG docker $USER
```

যদি এরপরেও `sudo` ছাড়া ডকার না চলে, তবে একবার সেশনটি রিস্টার্ট (লগআউট ও পুনরায় লগইন) করুন। তারপর ইনস্টলেশন নিশ্চিত করতে নিচের কমান্ডটি রান করুন:

```bash
docker run hello-world
```

![VM টার্মিনালে সফলভাবে Docker টেস্ট রান হওয়ার দৃশ্য](images/03-aws-vm-03-docker.jpg)

> **নোট:** ক্লাউড VM ব্যবহার করা বাধ্যতামূলক নয়; আপনি যদি নিজের লোকাল মেশিনে লিনাক্স বা ডকার ব্যবহার করতে স্বাচ্ছন্দ্যবোধ করেন, তবে একই কমান্ডগুলো আপনার লোকাল কম্পিউটারেও কার্যকর হবে।
