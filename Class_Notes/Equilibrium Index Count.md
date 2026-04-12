# 🧠 Equilibrium Index Count — Carry Forward Technique

---

## 📌 Problem Statement

Given an array `a`, count the number of indices `i` such that:

```text
sum of elements on left of i == sum of elements on right of i
```

👉 These positions are called **Equilibrium Indices**

---

## 💡 Example

```text
Array: [-7, 1, 5, 2, -4, 3, 0]
```

👉 Output:

```text
2
```

(Indices where left sum = right sum)

---

## 🔥 Key Idea (Carry Forward from Left)

Instead of recomputing left and right sums every time (**O(n²)** ❌),
we use a **carry-forward approach**:

* Compute total sum once
* Maintain left sum while traversing

---

## 🧠 Intuition

At index `i`:

```text
Left sum  = lsum
Right sum = total_sum - lsum - a[i]
```

👉 So no need to compute right sum separately!

---

## 🚀 Algorithm

### Step 1: Compute total sum

```cpp
sum = total sum of array
```

---

### Step 2: Traverse and carry left sum

```cpp
lsum = 0
```

For each index:

* Compute:

```cpp
rsum = sum - lsum - a[i]
```

* If:

```cpp
lsum == rsum → equilibrium index
```

* Update:

```cpp
lsum += a[i]
```

---

## ✅ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int equilibrium(vector<int> &a)
{
    int n = a.size();
    int count = 0;

    long sum = 0;
    for (int i = 0; i < n; i++)
        sum += a[i];

    long lsum = 0;

    for (int i = 0; i < n; i++)
    {
        long rsum = sum - lsum - a[i];

        if (lsum == rsum)
            count++;

        lsum += a[i];
    }

    return count;
}

int main()
{
    vector<int> s = {-7, 1, 5, 2, -4, 3, 0};
    cout << equilibrium(s) << endl;
    return 0;
}
```

---

## 🔍 Dry Run

```text
Array: [-7, 1, 5, 2, -4, 3, 0]
Total Sum = 0
```

| Index | Value | lsum | rsum = sum-lsum-a[i] | Equilibrium? |
| ----- | ----- | ---- | -------------------- | ------------ |
| 0     | -7    | 0    | 7                    | ❌            |
| 1     | 1     | -7   | 6                    | ❌            |
| 2     | 5     | -6   | 1                    | ❌            |
| 3     | 2     | -1   | -1                   | ✅            |
| 4     | -4    | 1    | 3                    | ❌            |
| 5     | 3     | -3   | 0                    | ❌            |
| 6     | 0     | 0    | 0                    | ✅            |

👉 Total = **2 equilibrium indices**

---

## ⏱️ Complexity

| Type  | Value |
| ----- | ----- |
| Time  | O(n)  |
| Space | O(1)  |

---

## ⚠️ Common Mistakes

* ❌ Recomputing left/right sums every time
* ❌ Forgetting to subtract `a[i]` from right sum
* ❌ Updating `lsum` before checking condition

---

## 🎯 Key Insight

> Right sum can always be derived from total sum — no need to scan right side

---

## 🧠 One-Line Summary

```text
Equilibrium if: left_sum == total_sum - left_sum - current_element
```

---

## 🔁 Carry Forward Pattern Summary

```text
When same data computed multiple times → carry it forward
```

| Problem      | Carry Variable    | Direction    |
| ------------ | ----------------- | ------------ |
| Leaders      | maxR              | right → left |
| ab-pairs     | count of 'b' (cb) | right → left |
| ABA triplets | count of 'a' (la) | left → right |
| Equilibrium  | left sum (lsum)   | left → right |

---

## ⚡ Formula Tricks

```text
ra   = T - la                  (Triplets: avoid right scan)
rsum = total - lsum - a[i]     (Equilibrium: avoid right scan)
```

---

## 🔥 Final Thought

This is one of the **cleanest carry-forward applications**:

👉 Convert 2-direction dependency → 1 pass
👉 Replace repeated work with math formula
👉 Achieve optimal O(n)

---
