# Limitations of AI Benchmarks: Data Contamination and Overfitting (বাংলায়)

AI মডেলের ক্ষমতা মাপার জন্য বিভিন্ন Benchmark ব্যবহার করা হয়, যেমন MMLU, GPQA, HumanEval, SWE-bench ইত্যাদি। কিন্তু Benchmark Score সবসময় বাস্তব দক্ষতার সঠিক প্রতিফলন নয়। এর দুটি বড় কারণ হলো **Data Contamination** এবং **Overfitting**।

---

# ১. Data Contamination কী?

Data Contamination ঘটে যখন Benchmark-এর প্রশ্ন বা তার খুব কাছাকাছি তথ্য মডেলের Training Data-তে আগে থেকেই উপস্থিত থাকে।

সহজ উদাহরণ:

ধরুন একজন ছাত্রকে পরীক্ষার আগে প্রশ্নপত্র দেখিয়ে দেওয়া হলো।

পরীক্ষায় সে 95% নম্বর পেল।

এখন প্রশ্ন হলো:

* সে কি সত্যিই বিষয়টি বুঝেছে?
* নাকি আগে থেকেই উত্তর মুখস্থ ছিল?

AI Model-এর ক্ষেত্রেও একই সমস্যা হতে পারে।

---

## উদাহরণ

ধরুন একটি Benchmark-এ প্রশ্ন আছে:

> "What is the capital of France?"

যদি মডেল Training-এর সময় লক্ষ লক্ষ বার এই প্রশ্ন-উত্তর দেখে থাকে, তাহলে পরীক্ষায় ভালো ফল করা তার প্রকৃত Reasoning Ability প্রমাণ করে না।

---

## কেন এটি সমস্যা?

এতে Benchmark Score কৃত্রিমভাবে বেড়ে যায়।

ফলাফল:

* Model-এর প্রকৃত ক্ষমতা বোঝা কঠিন হয়
* বিভিন্ন Model-এর তুলনা বিভ্রান্তিকর হতে পারে
* বাস্তব জগতে Performance কম হতে পারে

---

# Data Leakage বনাম Data Contamination

অনেক সময় এই দুই শব্দ কাছাকাছি অর্থে ব্যবহৃত হয়।

### Data Leakage

টেস্ট ডেটা ভুলবশত Training Data-তে চলে যাওয়া।

### Data Contamination

Training Data-তে Benchmark সম্পর্কিত তথ্য থেকে যাওয়া।

দুটির ফল একই:

> Benchmark Score বাস্তব দক্ষতার চেয়ে বেশি দেখায়।

---

# ২. Overfitting কী?

Overfitting হলো যখন Model নির্দিষ্ট Benchmark-এ ভালো করার জন্য অতিরিক্তভাবে মানিয়ে যায়, কিন্তু নতুন সমস্যায় ভালো কাজ করতে পারে না।

---

## সহজ উদাহরণ

একজন ছাত্র ১০০০টি পুরনো প্রশ্ন মুখস্থ করল।

পরীক্ষায় একই ধরনের প্রশ্ন এলে সে ভালো করবে।

কিন্তু নতুন প্রশ্ন এলে সমস্যায় পড়বে।

এটাই Overfitting।

---

## AI Model-এর ক্ষেত্রে

যদি Model Developer বারবার Benchmark ব্যবহার করে Model উন্নত করেন:

1. Benchmark Run
2. ভুল বিশ্লেষণ
3. Model Update
4. আবার Benchmark Run

এই চক্র বহুবার চললে Model Benchmark-এর প্রতি Overfit হয়ে যেতে পারে।

---

# Overfitting-এর লক্ষণ

### Benchmark Score বাড়ছে

* MMLU: 80 → 90 → 95

### কিন্তু বাস্তব কাজে

* Reasoning দুর্বল
* নতুন Domain-এ ভুল
* Hallucination বেশি

তাহলে বোঝা যায় Model Benchmark-এর জন্য Optimize হয়েছে।

---

# Benchmark Saturation

কিছু Benchmark এত বেশি ব্যবহৃত হয়েছে যে আধুনিক LLM-গুলো প্রায় "মুখস্থ" করে ফেলেছে।

ফলে:

* Score-এর পার্থক্য কমে যায়
* Ranking কম অর্থবহ হয়ে যায়
* নতুন Benchmark দরকার হয়

---

# কেন নতুন Benchmark তৈরি হয়?

এই সমস্যাগুলো সমাধানের জন্য গবেষকরা নতুন Benchmark তৈরি করেন।

উদাহরণ:

* OpenAI এর HumanEval
* GPQA
* MMLU-Pro
* LiveBench
* SWE-bench

এগুলোতে সাধারণত:

* কঠিন প্রশ্ন
* নতুন ডেটা
* কম Contamination
* বাস্তবধর্মী Task

ব্যবহার করা হয়।

---

# Benchmark Score কেন সবকিছু নয়?

একটি Model:

* MMLU-তে 90%
* GPQA-তে 60%

অন্য Model:

* MMLU-তে 85%
* GPQA-তে 75%

দ্বিতীয় Model বাস্তব Reasoning-এ বেশি শক্তিশালী হতে পারে।

তাই শুধু একটি Benchmark দেখে সিদ্ধান্ত নেওয়া ঠিক নয়।

---

# ভালো Evaluation-এর উপায়

একটি Model মূল্যায়নের সময়:

✅ একাধিক Benchmark দেখুন

✅ বাস্তব কাজ (Real-world Tasks) পরীক্ষা করুন

✅ Coding Task দেখুন

✅ Reasoning Task দেখুন

✅ Long Context Performance দেখুন

✅ Human Evaluation বিবেচনা করুন

---

# সংক্ষেপে

### Data Contamination

* Benchmark-এর তথ্য Training Data-তে চলে আসে
* Score কৃত্রিমভাবে বেড়ে যায়
* প্রকৃত দক্ষতা বোঝা কঠিন হয়

### Overfitting

* Model Benchmark-এর জন্য অতিরিক্ত Optimize হয়
* নতুন সমস্যায় Performance কমে যায়
* বাস্তব দক্ষতার ভুল ধারণা দেয়

### মূল শিক্ষা

> **উচ্চ Benchmark Score মানেই সেরা AI Model নয়।**
>
> একটি Model-এর প্রকৃত ক্ষমতা বুঝতে Benchmark Score-এর পাশাপাশি বাস্তব কাজ, Reasoning, Coding, Generalization এবং Human Evaluation-ও বিবেচনা করতে হয়।
