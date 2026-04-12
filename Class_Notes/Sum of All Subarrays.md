# 🧠 Sum of All Subarrays — Prefix Sum Approach

---

## 📌 Problem Statement

Given an array `a`, compute:

```text
Sum of all subarray sums
```

👉 That means:

* Generate every subarray
* Add all their sums together

---

## 💡 Example

```text id="o8d7l2"
Array: [1, 2, 3]
```

Subarrays:

```text id="d9v8p1"
[1] → 1  
[1,2] → 3  
[1,2,3] → 6  
[2] → 2  
[2,3] → 5  
[3] → 3  
```

👉 Total:

```text id="f1k7mz"
1 + 3 + 6 + 2 + 5 + 3 = 20
```

---

## 🔥 Your Approach (Prefix Sum + Double Loop)

### Step 1: Build Prefix Sum

```cpp id="k1y8ax"
ps[i] = sum from 0 → i
```

---

### Step 2: Generate All Subarrays

For each `(i, j)`:

```cpp id="9g7h2l"
if i == 0:
    sum = ps[j]
else:
    sum = ps[j] - ps[i-1]
```

---

## ✅ Code

```cpp id="x4v9kp"
#include <iostream>
#include <vector>
using namespace std;

long sumAll(vector<int> &a)
{
    int n = a.size();
    long ans = 0;

    // Prefix sum
    vector<int> ps(n);
    ps[0] = a[0];

    for (int i = 1; i < n; i++)
    {
        ps[i] = ps[i - 1] + a[i];
    }

    // All subarrays
    for (int i = 0; i < n; i++)
    {
        for (int j = i; j < n; j++)
        {
            if (i == 0)
                ans += ps[j];
            else
                ans += ps[j] - ps[i - 1];
        }
    }

    return ans;
}

int main()
{
    vector<int> s = {-7, 1, 5, 2, -4, 3, 0, 10};
    cout << sumAll(s);
    return 0;
}
```

---

## 🔍 Complexity

| Type  | Value |
| ----- | ----- |
| Time  | O(n²) |
| Space | O(n)  |

👉 Better than brute force O(n³), but still not optimal

---

## ⚠️ Observations

* You optimized **subarray sum calculation** using prefix sum
* But still iterate over all `(i, j)` pairs → O(n²)

---

## 🚀 OPTIMAL APPROACH (O(n)) — Contribution Technique

### 🔥 Key Idea

Each element contributes to multiple subarrays.

👉 For element `a[i]`:

* It appears in:

```text id="2wrq9v"
(i + 1) * (n - i) subarrays
```

---

### 🧠 Why?

* Start can be chosen from `0 → i` → `(i + 1)` ways
* End can be chosen from `i → n-1` → `(n - i)` ways

---

### 🎯 Formula

```text id="3qk8dl"
Contribution of a[i] = a[i] * (i+1) * (n-i)
```

---

## ✅ Optimal Code

```cpp id="7k2mne"
long long sumAll(vector<int> &a)
{
    int n = a.size();
    long long ans = 0;

    for (int i = 0; i < n; i++)
    {
        ans += (long long)a[i] * (i + 1) * (n - i);
    }

    return ans;
}
```

---

## 🔍 Dry Run (Small Example)

```text id="7cbk3v"
Array: [1, 2, 3]
```

| i | a[i] | Contribution  |
| - | ---- | ------------- |
| 0 | 1    | 1 × 1 × 3 = 3 |
| 1 | 2    | 2 × 2 × 2 = 8 |
| 2 | 3    | 3 × 3 × 1 = 9 |

👉 Total:

```text id="qzv7kt"
3 + 8 + 9 = 20
```

---

## ⏱️ Complexity Comparison

| Approach     | Time   |
| ------------ | ------ |
| Brute force  | O(n³)  |
| Prefix sum   | O(n²)  |
| Contribution | O(n) ✅ |

---

## ⚠️ Common Mistakes

* ❌ Forgetting `(i+1)*(n-i)` logic
* ❌ Using `int` → overflow risk
* ❌ Misunderstanding contribution idea

---

## 🎯 Key Insight

> Instead of generating subarrays, count how many times each element appears

---

## 🧠 One-Line Summary

```text id="m2x9qa"
Each element contributes to multiple subarrays → sum contributions directly
```

---

## 🔁 Pattern Connection

| Problem          | Technique    |
| ---------------- | ------------ |
| Range sum        | Prefix sum   |
| All subarray sum | Contribution |
| Max subarray     | Kadane       |

---

## 🔥 Final Thought

👉 This is a **classic optimization jump**
👉 From generating → counting contributions
👉 Very common in interviews & CP

---
