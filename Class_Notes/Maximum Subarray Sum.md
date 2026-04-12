# 🧠 Maximum Subarray Sum — Kadane’s Algorithm (Carry Forward)

---

## 📌 Problem Statement

Given an array `a`, find:

```text
Maximum possible sum of any subarray
```

👉 Subarray must be **contiguous**

---

## 💡 Example

```text
Array: [-7, 1, 5, 2, -4, 3, 0, 10]
```

👉 Best subarray:

```text
[1, 5, 2, -4, 3, 0, 10] → sum = 17
```

👉 Output:

```text
17
```

---

## 🔥 Key Idea (Carry Forward)

Instead of checking all subarrays (**O(n²) ❌**),
we **carry forward the best sum** while iterating.

---

## 🧠 Intuition

At each index:

* Either extend previous subarray
* Or start new subarray

👉 If sum becomes negative → discard it

---

## 🚀 Algorithm (Kadane’s)

1. Initialize:

```cpp
sum = 0
maxSum = -∞
```

2. Traverse array:

```cpp
sum += a[i]
maxSum = max(maxSum, sum)

if (sum < 0)
    sum = 0
```

---

## ✅ Code (Fixed Version)

```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

long long maxSum(vector<int> &a)
{
    int n = a.size();
    long long sum = 0;
    long long maxSumVal = LLONG_MIN;

    for (int i = 0; i < n; i++)
    {
        sum += a[i];

        if (sum > maxSumVal)
            maxSumVal = sum;

        if (sum < 0)
            sum = 0;
    }

    return maxSumVal;
}

int main()
{
    vector<int> s = {-7, 1, 5, 2, -4, 3, 0, 10};
    cout << maxSum(s);
    return 0;
}
```

---

## 🔍 Dry Run

```text
Array: [-7, 1, 5, 2, -4, 3, 0, 10]
```

| i | a[i] | sum    | max |
| - | ---- | ------ | --- |
| 0 | -7   | -7 → 0 | -7  |
| 1 | 1    | 1      | 1   |
| 2 | 5    | 6      | 6   |
| 3 | 2    | 8      | 8   |
| 4 | -4   | 4      | 8   |
| 5 | 3    | 7      | 8   |
| 6 | 0    | 7      | 8   |
| 7 | 10   | 17     | 17  |

👉 Final Answer:

```text
17
```

---

## ⏱️ Complexity

| Type  | Value  |
| ----- | ------ |
| Time  | O(n) ✅ |
| Space | O(1)   |

---

## ⚠️ Issues in Your Code

### ❌ 1. Missing Header

```cpp
INT_MIN
```

👉 Needs:

```cpp
#include <climits>
```

---

### ❌ 2. Variable Name `max`

```cpp
long max = INT_MIN;
```

👉 Bad practice (conflicts with `std::max`)

✔️ Use:

```cpp
maxSumVal
```

---

### ❌ 3. Use `long long`

Safer for large inputs

---

## 🎯 Key Insight

> Drop negative prefix — it will only reduce future sum

---

## 🧠 One-Line Summary

```text
Keep adding elements, reset when sum becomes negative
```

---

## 🔁 Pattern Connection

| Problem          | Technique    |
| ---------------- | ------------ |
| Max subarray sum | Kadane       |
| All subarray sum | Contribution |
| Range queries    | Prefix sum   |

---

## 🚀 Variations (Important)

* 🔥 Maximum subarray with indices
* 🔥 Circular array version
* 🔥 Maximum product subarray

---

## 🔥 Final Thought

👉 Kadane’s is one of the **most important algorithms**
👉 Converts O(n²) → O(n)
👉 Must master for interviews

---
