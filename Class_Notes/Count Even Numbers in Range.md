# 🧠 Count Even Numbers in Range — Prefix Sum + Carry Forward

---

## 📌 Problem Statement

Given:

* An array `a`
* Queries `Qmat` where each query is `[L, R]`

👉 For each query, count:

```text
Number of EVEN elements in the range [L, R]
```

---

## 💡 Example

```text
Array: [-7, 1, 5, 2, -4, 3, 0, 10]

Queries:
[0,0], [1,1], [2,6], [3,4], [0,7]
```

👉 Output:

```text
0 0 3 2 4
```

---

## 🔥 Key Idea (Transform + Prefix Sum)

Instead of checking each query manually (**O(nq) ❌**):

### Step 1: Transform array

Convert:

```text
Even → 1
Odd  → 0
```

👉 Trick:

```cpp
a[i] = 1 - abs(a[i] % 2)
```

---

## 🧠 Why This Works?

| Value | a[i] % 2 | abs | Result | Meaning  |
| ----- | -------- | --- | ------ | -------- |
| Even  | 0        | 0   | 1      | count it |
| Odd   | ±1       | 1   | 0      | ignore   |

---

## 🚀 Algorithm

### Step 1: Convert array

```cpp
for each element:
    a[i] = 1 (if even) else 0
```

---

### Step 2: Build Prefix Sum

```cpp
ps[i] = ps[i-1] + a[i]
```

---

### Step 3: Answer Queries

```cpp
If L == 0 → ps[R]
Else       → ps[R] - ps[L-1]
```

---

## ✅ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

void evenCount(vector<int> &a, vector<vector<int>> &Qmat)
{
    int n = a.size(), q = Qmat.size();

    // Step 1: Transform array (even → 1, odd → 0)
    for (int i = 0; i < n; i++)
    {
        a[i] = 1 - abs(a[i] % 2);
    }

    // Step 2: Prefix sum
    vector<long> ps(n);
    ps[0] = a[0];

    for (int i = 1; i < n; i++)
    {
        ps[i] = ps[i - 1] + a[i];
    }

    // Step 3: Answer queries
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
    vector<int> s = {-7, 1, 5, 2, -4, 3, 0, 10};
    vector<vector<int>> q = {{0, 0}, {1, 1}, {2, 6}, {3, 4}, {0, 7}};

    evenCount(s, q);
    return 0;
}
```

---

## 🔍 Dry Run

### Step 1: Transform

```text
Original: [-7, 1, 5, 2, -4, 3, 0, 10]
Binary:   [ 0, 0, 0, 1,  1, 0, 1,  1]
```

---

### Step 2: Prefix Sum

```text
ps = [0, 0, 0, 1, 2, 2, 3, 4]
```

---

### Step 3: Queries

| Query | Calculation   | Result |
| ----- | ------------- | ------ |
| [0,0] | ps[0]         | 0      |
| [1,1] | ps[1] - ps[0] | 0      |
| [2,6] | ps[6] - ps[1] | 3      |
| [3,4] | ps[4] - ps[2] | 2      |
| [0,7] | ps[7]         | 4      |

---

## ⏱️ Complexity

| Type          | Value    |
| ------------- | -------- |
| Preprocessing | O(n)     |
| Each Query    | O(1)     |
| Total         | O(n + q) |

---

## ⚠️ Common Mistakes

* ❌ Forgetting to transform array
* ❌ Wrong parity check (`a[i] % 2 == 0`) without handling negatives
* ❌ Modifying original array unintentionally

---

## 🎯 Key Insight

> Convert problem into counting (0/1), then apply prefix sum

---

## 🧠 One-Line Summary

```text
Convert even → 1, then range sum = count of even numbers
```

---

## 🔁 Carry Forward Pattern

```text
Transform + Prefix = Powerful combo
```

| Problem           | Trick            |
| ----------------- | ---------------- |
| Even count        | 0/1 conversion   |
| Range sum         | Prefix sum       |
| Frequency queries | Prefix + hashing |

---

## 🚀 Advanced Insight

Instead of modifying array, you can use:

```cpp
int val = (a[i] % 2 == 0);
```

👉 Cleaner + safer

---

## 🔥 Final Thought

👉 This pattern is extremely common in CP
👉 Convert complex condition → numeric form
👉 Then use prefix sum for fast queries

---
