# 🧠 Range Sum Queries using Prefix Sum — Carry Forward Technique

---

## 📌 Problem Statement

Given:

* An array `a`
* Multiple queries `Qmat`, where each query is `[L, R]`

👉 For each query, find:

```text
Sum of elements from index L to R
```

---

## 💡 Example

```text
Array: [-7, 1, 5, 2, -4, 3, 0]

Queries:
[0,0], [1,1], [2,6], [3,4], [0,6]
```

👉 Output:

```text
-7 1 6 -2 0
```

---

## 🔥 Key Idea (Prefix Sum + Carry Forward)

Instead of computing sum for every query (**O(n) per query ❌**),
we precompute prefix sum once and answer each query in **O(1)**.

---

## 🧠 Intuition

👉 Prefix sum stores cumulative sum:

```text
ps[i] = sum from index 0 to i
```

---

## ⚡ Range Sum Formula

To find sum from `L` to `R`:

```text
If L == 0 → ps[R]
Else       → ps[R] - ps[L-1]
```

---

## 🚀 Algorithm

### Step 1: Build Prefix Sum

```cpp
ps[0] = a[0]
for i = 1 → n-1:
    ps[i] = ps[i-1] + a[i]
```

---

### Step 2: Answer Queries

For each query `[L, R]`:

```cpp
if L == 0:
    answer = ps[R]
else:
    answer = ps[R] - ps[L-1]
```

---

## ✅ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

void RangeSum(vector<int> &a, vector<vector<int>> Qmat)
{
    int n = a.size(), q = Qmat.size();

    // Step 1: Prefix Sum
    vector<long> ps(n);
    ps[0] = a[0];

    for (int i = 1; i < n; i++)
    {
        ps[i] = ps[i - 1] + a[i];
    }

    // Step 2: Answer Queries
    for (int i = 0; i < q; i++)
    {
        int s = Qmat[i][0], e = Qmat[i][1];

        if (s == 0)
            cout << ps[e] << " ";
        else
            cout << ps[e] - ps[s - 1] << " ";
    }
}

int main()
{
    vector<int> s = {-7, 1, 5, 2, -4, 3, 0};
    vector<vector<int>> q = {{0, 0}, {1, 1}, {2, 6}, {3, 4}, {0, 6}};

    RangeSum(s, q);
    return 0;
}
```

---

## 🔍 Dry Run

### Prefix Sum:

```text
ps = [-7, -6, -1, 1, -3, 0, 0]
```

---

### Queries:

| Query | Calculation   | Result |
| ----- | ------------- | ------ |
| [0,0] | ps[0]         | -7     |
| [1,1] | ps[1] - ps[0] | 1      |
| [2,6] | ps[6] - ps[1] | 6      |
| [3,4] | ps[4] - ps[2] | -2     |
| [0,6] | ps[6]         | 0      |

---

## ⏱️ Complexity

| Type          | Value    |
| ------------- | -------- |
| Preprocessing | O(n)     |
| Each Query    | O(1)     |
| Total         | O(n + q) |

---

## ⚠️ Common Mistakes

* ❌ Forgetting `L == 0` case
* ❌ Off-by-one errors (`ps[L-1]`)
* ❌ Recomputing sum for each query

---

## 🎯 Key Insight

> Precompute once → answer multiple queries instantly

---

## 🧠 One-Line Summary

```text
Range sum = ps[R] - ps[L-1]
```

---

## 🔁 Carry Forward Pattern

```text
When repeated queries exist → preprocess and reuse
```

| Problem Type | Technique            |
| ------------ | -------------------- |
| Range Sum    | Prefix Sum           |
| Equilibrium  | Carry left sum       |
| Leaders      | Carry max from right |

---

## 🚀 Real-World Analogy

Imagine:

* You track your daily expenses cumulatively
* To find expenses between day 3 and 7 → subtract totals

👉 Same idea as prefix sum

---

## 🔥 Final Thought

👉 Prefix sum transforms **slow repeated work → instant answers**
👉 Core concept in competitive programming
👉 Foundation for advanced topics (Fenwick tree, segment tree)

---
