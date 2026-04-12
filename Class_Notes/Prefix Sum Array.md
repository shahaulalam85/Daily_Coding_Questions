# 🧠 Prefix Sum Array — Carry Forward Technique

---

## 📌 Problem Statement

Given an array `a`, construct its **Prefix Sum Array**.

👉 Prefix sum at index `i` = sum of all elements from index `0` to `i`

---

## 💡 Example

```text
Array: [-7, 1, 5, 2, -4, 3, 0]
```

👉 Prefix Sum:

```text
[-7, -6, -1, 1, -3, 0, 0]
```

---

## 🔥 Key Idea (Carry Forward)

Instead of recomputing sum every time (**O(n²)** ❌),
we **carry forward the sum**:

```text
ps[i] = ps[i-1] + a[i]
```

---

## 🧠 Intuition

* First element:

```text
ps[0] = a[0]
```

* Every next element:

```text
Add current value to previous prefix sum
```

👉 So we reuse previous computation → efficient

---

## 🚀 Algorithm

1. Create prefix array `ps` of size `n`
2. Initialize:

```cpp
ps[0] = a[0]
```

3. For `i = 1 → n-1`:

```cpp
ps[i] = ps[i-1] + a[i]
```

4. Return `ps`

---

## ✅ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

vector<long> ps(vector<int> &a)
{
    int n = a.size();
    vector<long> ps(n);

    ps[0] = a[0];

    for (int i = 1; i < n; i++)
    {
        ps[i] = ps[i - 1] + a[i];
    }

    return ps;
}

int main()
{
    vector<int> s = {-7, 1, 5, 2, -4, 3, 0};
    vector<long> p = ps(s);

    for (long x : p)
        cout << x << " ";

    return 0;
}
```

---

## 🔍 Dry Run

```text
Array: [-7, 1, 5, 2, -4, 3, 0]
```

| Index | a[i] | ps[i] |
| ----- | ---- | ----- |
| 0     | -7   | -7    |
| 1     | 1    | -6    |
| 2     | 5    | -1    |
| 3     | 2    | 1     |
| 4     | -4   | -3    |
| 5     | 3    | 0     |
| 6     | 0    | 0     |

---

## ⏱️ Complexity

| Type  | Value |
| ----- | ----- |
| Time  | O(n)  |
| Space | O(n)  |

---

## ⚠️ Common Mistakes

* ❌ Not initializing `ps[0]`
* ❌ Using `ps[i] = a[i] + a[i-1]` (wrong logic)
* ❌ Off-by-one errors

---

## 🎯 Key Insight

> Prefix sum stores cumulative information so future queries become fast

---

## 🧠 One-Line Summary

```text
Prefix sum at index i = sum of all elements from 0 to i
```

---

## 🚀 Applications

Prefix sums are extremely powerful:

* Range sum queries → O(1)
* Subarray problems
* Equilibrium index
* Sliding window optimization
* 2D prefix sums (advanced)

---

## ⚡ Range Query Trick

To find sum from `L` to `R`:

```text
if L == 0 → ps[R]
else → ps[R] - ps[L-1]
```

---

## 🔁 Carry Forward Pattern

```text
When same computation repeats → store and reuse it
```

| Problem     | Carry Variable |
| ----------- | -------------- |
| Prefix Sum  | cumulative sum |
| Equilibrium | left sum       |
| Leaders     | max from right |

---

## 🔥 Final Thought

👉 Prefix sum is one of the **most important concepts** in DSA
👉 Converts repeated work → constant time queries
👉 Foundation for many advanced algorithms

---
