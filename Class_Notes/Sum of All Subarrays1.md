# 🧠 Sum of All Subarrays — Contribution Technique (Optimal)

---

## 📌 Problem Statement

Given an array `a`, compute:

```text
Sum of all subarray sums
```

👉 Instead of generating all subarrays, use an **optimized O(n) approach**

---

## 💡 Example

```text
Array: [1, 2, 3]
```

Subarrays:

```text
[1] → 1  
[1,2] → 3  
[1,2,3] → 6  
[2] → 2  
[2,3] → 5  
[3] → 3  
```

👉 Total:

```text
20
```

---

## 🔥 Key Idea (Contribution Technique)

👉 Each element contributes to multiple subarrays

Instead of:

* Generating all subarrays ❌

We:

* Count how many times each element appears ✅

---

## 🧠 Intuition

For index `i`:

### 👉 Number of ways to choose start:

```text
(i + 1)
```

### 👉 Number of ways to choose end:

```text
(n - i)
```

---

## 🎯 Contribution Formula

```text
Contribution of a[i] = a[i] × (i + 1) × (n - i)
```

---

## 🚀 Algorithm

1. Loop through each index `i`
2. Compute:

```cpp
s = (i + 1)
e = (n - i)
```

3. Add contribution:

```cpp
ans += a[i] * s * e
```

---

## ✅ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

long long sumAll(vector<int> &a)
{
    int n = a.size();
    long long ans = 0;

    for (int i = 0; i < n; i++)
    {
        long long s = i + 1;
        long long e = n - i;

        ans += (long long)a[i] * s * e;
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

## 🔍 Dry Run (Small Example)

```text
Array: [1, 2, 3]
```

| i | a[i] | (i+1) | (n-i) | Contribution |
| - | ---- | ----- | ----- | ------------ |
| 0 | 1    | 1     | 3     | 3            |
| 1 | 2    | 2     | 2     | 8            |
| 2 | 3    | 3     | 1     | 9            |

👉 Total:

```text
3 + 8 + 9 = 20
```

---

## ⏱️ Complexity

| Type  | Value  |
| ----- | ------ |
| Time  | O(n) ✅ |
| Space | O(1)   |

---

## ⚠️ Common Mistakes

* ❌ Using `int` → overflow risk
* ❌ Forgetting `(i+1)*(n-i)` logic
* ❌ Trying to generate subarrays

---

## 🎯 Key Insight

> Each element appears in multiple subarrays → count its contribution directly

---

## 🧠 One-Line Summary

```text
Total sum = Σ (a[i] × (i+1) × (n-i))
```

---

## 🔁 Pattern Connection

| Problem          | Technique    |
| ---------------- | ------------ |
| All subarray sum | Contribution |
| Range sum        | Prefix sum   |
| Max subarray     | Kadane       |

---

## 🚀 Why This is Powerful

* Eliminates nested loops
* Converts O(n²) → O(n)
* Frequently asked in interviews

---

## 🔥 Final Thought

👉 This is a **high-level optimization pattern**
👉 Always think:

```text
Can I count contribution instead of generating all cases?
```

---

