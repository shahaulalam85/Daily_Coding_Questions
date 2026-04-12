# 🧠 Leaders in an Array (Carry Forward Technique)

---

## 📌 Problem Statement

Given an array, find the **number of leaders**.

👉 A **leader** is an element that is **greater than all elements to its right**.

---

## 💡 Example

```text
Array: [16, 17, 4, 3, 5, 2]
```

### Leaders:

```text
17, 5, 2
```

👉 Output:

```text
3
```

---

## 🔥 Key Idea (Carry Forward Concept)

Instead of checking each element with all elements on the right (**O(n²)** ❌),
we traverse **from right to left** and **carry forward the maximum**.

---

## 🧠 Intuition

* The **last element is always a leader**
* Keep track of the **maximum element seen so far (from right)**
* If current element > max → it is a leader

---

## 🚀 Algorithm

1. Start from the **last element**
2. Initialize:

```cpp
max = last element
count = 1
```

3. Traverse from right → left:

   * If `a[i] > max`

     * Update max
     * Increment count
4. Return count

---

## ✅ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int leader(vector<int> &a)
{
    int n = a.size();
    int count = 1;              // last element is always leader
    int maxVal = a[n - 1];     // carry forward max

    for (int i = n - 2; i >= 0; i--)
    {
        if (a[i] > maxVal)
        {
            maxVal = a[i];
            count++;
        }
    }
    return count;
}

int main()
{
    vector<int> a = {16, 17, 4, 3, 5, 2};
    int ans = leader(a);
    cout << ans;
    return 0;
}
```

---

## 🔍 Dry Run

```text
Array: [16, 17, 4, 3, 5, 2]
```

| Index | Value | Max So Far | Leader? |
| ----- | ----- | ---------- | ------- |
| 5     | 2     | 2          | ✅       |
| 4     | 5     | 5          | ✅       |
| 3     | 3     | 5          | ❌       |
| 2     | 4     | 5          | ❌       |
| 1     | 17    | 17         | ✅       |
| 0     | 16    | 17         | ❌       |

👉 Leaders = **3**

---

## ⏱️ Complexity

| Type  | Value |
| ----- | ----- |
| Time  | O(n)  |
| Space | O(1)  |

---

## ⚠️ Common Mistakes

* ❌ Traversing left → right
* ❌ Comparing with all right elements (O(n²))
* ❌ Forgetting last element is always a leader

---

## 🎯 Key Insight

> Always process from **right to left** and carry forward the maximum.

---

## 🧠 One-Line Summary

```text
An element is a leader if it is greater than all elements to its right.
```

---

## 🚀 Bonus (Return Actual Leaders)

```cpp
vector<int> leaders(vector<int> &a)
{
    int n = a.size();
    vector<int> result;

    int maxVal = a[n - 1];
    result.push_back(maxVal);

    for (int i = n - 2; i >= 0; i--)
    {
        if (a[i] > maxVal)
        {
            maxVal = a[i];
            result.push_back(a[i]);
        }
    }

    return result; // reverse if needed
}
```

---

## 🔥 Final Thought

This is a **classic carry-forward pattern**:

👉 Used in:

* Leaders problem
* Max suffix arrays
* Stock span variations

---
