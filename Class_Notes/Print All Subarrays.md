# 🧠 Print All Subarrays — Brute Force (Triple Loop)

---

## 📌 Problem Statement

Given an array `a`, print **all possible subarrays**.

👉 A **subarray** is a contiguous part of the array.

---

## 💡 Example

```text id="k4w5he"
Array: [1, 2, 3]
```

👉 Subarrays:

```text id="9y5f0v"
[1]
[1,2]
[1,2,3]
[2]
[2,3]
[3]
```

---

## 🔥 Key Idea

To generate all subarrays:

* Fix starting index `i`
* Fix ending index `j`
* Print elements from `i → j`

---

## 🧠 Intuition

👉 Every subarray is uniquely defined by:

```text id="6q3r2s"
(start index i, end index j)
```

👉 Total number of subarrays:

```text id="b2n9lz"
n * (n + 1) / 2
```

---

## 🚀 Algorithm

1. Loop over all starting indices `i`
2. For each `i`, loop over ending indices `j`
3. Print elements from `i` to `j`

---

## ✅ Code

```cpp id="xg9d2p"
#include <iostream>
#include <vector>
using namespace std;

void printAll(vector<int> &a)
{
    int n = a.size();

    for (int i = 0; i < n; i++)          // start index
    {
        for (int j = i; j < n; j++)      // end index
        {
            for (int k = i; k <= j; k++) // print subarray
            {
                cout << a[k] << " ";
            }
            cout << "\n";
        }
    }
}

int main()
{
    vector<int> s = {-7, 1, 5, 2, -4, 3, 0, 10};
    printAll(s);
    return 0;
}
```

---

## 🔍 Dry Run (Small Example)

```text id="jqgkq1"
Array: [1, 2, 3]
```

| i | j | Subarray |
| - | - | -------- |
| 0 | 0 | [1]      |
| 0 | 1 | [1,2]    |
| 0 | 2 | [1,2,3]  |
| 1 | 1 | [2]      |
| 1 | 2 | [2,3]    |
| 2 | 2 | [3]      |

---

## ⏱️ Complexity

| Type  | Value |
| ----- | ----- |
| Time  | O(n³) |
| Space | O(1)  |

👉 Because:

* `i` loop → n
* `j` loop → n
* `k` loop → n

---

## ⚠️ Common Mistakes

* ❌ Using `k < j` instead of `k <= j`
* ❌ Mixing indices (`i`, `j`, `k`)
* ❌ Forgetting new line after each subarray

---

## 🎯 Key Insight

> Every subarray = combination of (start, end)

---

## 🧠 One-Line Summary

```text id="rx6r8z"
Fix start and end → print elements in between
```

---

## 🚀 Optimization Ideas

### 🔹 Print Only Count (O(1))

```text id="b9l6t1"
Total subarrays = n(n+1)/2
```

---

### 🔹 Max Subarray Sum (Kadane’s Algorithm → O(n))

Instead of generating all subarrays, optimize using:

* Prefix sum
* Kadane’s algorithm

---

## 🔁 Pattern Connection

| Problem             | Technique   |
| ------------------- | ----------- |
| Print all subarrays | Brute force |
| Max subarray sum    | Kadane      |
| Range queries       | Prefix sum  |

---

## 🔥 Final Thought

👉 This is the **foundation problem** for many array questions
👉 Most optimizations start from this brute-force idea
👉 Learn this → then optimize 🚀

---
