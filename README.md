# 🛡️ NSL-KDD: The 99% Accuracy Illusion
### *Building a "Digital Bouncer" for Zero-Day Attack Detection*

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Library](https://img.shields.io/badge/Library-Scikit--Learn-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📖 The Story
Imagine you run an exclusive club (your Network). You need a **Bouncer** at the door to stop troublemakers.
* **Easy Mode:** The bouncer blocks people he *knows* are bad (Known Attacks).
* **Hard Mode (Real Life):** The bouncer must spot bad behavior from people he has *never seen before* (Zero-Day Attacks).

Most projects on the **NSL-KDD Dataset** claim **99% accuracy**.
**Spoiler Alert:** They are cheating. They test on known attacks.

**This project is different.** We built a system that sacrifices "fake accuracy" for **real-world robustness**, achieving **~81% accuracy** on completely unknown threats.

---

## ⚠️ The "99% Illusion"
Why do you see 99% accuracy everywhere?
1.  They split the **Training Set** into Train/Test.
2.  The model memorizes the attack signatures.
3.  It gets a perfect score on the exam because it has seen the questions before.

**Our Approach:**
We tested on the `KDDTest+` dataset, which contains **17 specific attack types** (like `mscan`, `saint`) that are **NOT** in the training set. This simulates a real **Zero-Day Attack** scenario.

---

## 🛠️ The Process
### 1. Taming "Naked" Data
The raw dataset came without column headers. We had to:
* Map 43 features manually.
* Encode categorical data (Protocol, Service, Flag) into "Robot Language" (One-Hot Encoding).
* Handle the "Missing Guest" problem (mismatched columns between Train/Test).

### 2. The Analysis (EDA)
We discovered that:
* **ICMP** protocol is the favorite weapon for DoS attacks.
* **Private** services are highly suspicious.
* **SF** flag is the only "safe" handshake; **S0** is almost always malicious.

### 3. The Battle (Modeling)
We pitted 7 algorithms against each other, from simple Logistic Regression to heavyweights like XGBoost.

---

## 🏆 The Verdict: David vs. Goliath

We expected the complex models to win. **We were wrong.**

| Rank | Model | Accuracy on Zero-Day Attacks | Time (s) | Verdict |
| :--- | :--- | :--- | :--- | :--- |
| 🥇 | **Decision Tree** | **80.90%** | **1.57s** | **The Champion (Simple & Sharp)** |
| 🥈 | Gradient Boosting | 78.91% | 37.12s | Good, but slow |
| 🥉 | XGBoost | 78.76% | 2.16s | Over-complicated the problem |
| 📉 | Naive Bayes | 51.23% | 0.40s | Basically a coin flip |

**Insight:** In cybersecurity, a simple, strict rulebook (Decision Tree) often beats a complex committee (Random Forest/Boosting) when facing unknown threats.

---

## 🚀 Installation & Usage

1. **Clone the repo:**
```bash
git clone [https://github.com/YourUsername/NSL-KDD-Illusion.git](https://github.com/YourUsername/NSL-KDD-Illusion.git)
