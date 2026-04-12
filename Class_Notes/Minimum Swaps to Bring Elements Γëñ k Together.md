# 🧠 Minimum Swaps to Bring Elements ≤ k Together — Sliding Window

---

## 📌 Problem Statement

Given an array `a` and a number `k`, find:

```text
Minimum number of swaps required to bring all elements ≤ k together
```

---

## 💡 Example

```text
Array: [-7, 1, 5, 2, -4, 3, 0, 10]
k = 3
```

Good elements (≤ k):

```text
-7, 1, 2, -4, 3, 0 → total = 6
```

👉 Output:

```text
Minimum swaps required = 2
```

---

## 🔥 Key Idea (Sliding Window)

👉 We don’t actually perform swaps!

Instead:

* Group all **good elements (≤ k)** together
* Find a window where maximum good elements already exist

---

## 🧠 Intuition

* Let:

```text
W = number of elements ≤ k
```

👉 This is the **window size**

Inside any window:

```text
bad elements = W - good elements
```

👉 These bad elements need swapping

So:

```text
Minimum swaps = W - max_good_in_any_window
```

---

## 🚀 Algorithm

### Step 1: Count total good elements

```cpp
total_good = count of elements ≤ k
```

---

### Step 2: First window

```cpp
good = number of elements ≤ k in first window of size W
```

---

### Step 3: Slide the window

* Remove left element
* Add right element
* Update `good`

---

### Step 4: Track maximum good

```cpp
ans = max(good across all windows)
```

---

### Step 5: Final Answer

```cpp
min swaps = total_good - ans
```

---

## ✅ Code

```cpp
#include <iostream>
#include <vector>
using namespace std;

int minSwap(vector<int> &a, int k)
{
    int n = a.size();

    // Step 1: count good elements
    int total_good = 0;
    for (int i = 0; i < n; i++)
    {
        if (a[i] <= k)
            total_good++;
    }

    int W = total_good;

    // Step 2: first window
    int good = 0;
    for (int i = 0; i < W; i++)
    {
        if (a[i] <= k)
            good++;
    }

    int ans = good;

    // Step 3: sliding window
    for (int i = 1, j = W; j < n; i++, j++)
    {
        if (a[i - 1] <= k)
            good--;

        if (a[j] <= k)
            good++;

        ans = max(ans, good);
    }

    // Step 5: result
    return total_good - ans;
}

int main()
{
    vector<int> s = {-7, 1, 5, 2, -4, 3, 0, 10};
    cout << minSwap(s, 3);
    return 0;
}
```

---

## 🔍 Dry Run

```text
Array: [-7, 1, 5, 2, -4, 3, 0, 10]
k = 3
W = 6
```

### Windows:

| Window          | Good Count |
| --------------- | ---------- |
| [-7,1,5,2,-4,3] | 5          |
| [1,5,2,-4,3,0]  | 5          |
| [5,2,-4,3,0,10] | 4          |

👉 Max good = 5

---

## 🧮 Final Answer

```text
min swaps = 6 - 5 = 1
```

---

## ⏱️ Complexity

| Type  | Value  |
| ----- | ------ |
| Time  | O(n) ✅ |
| Space | O(1)   |

---

## ⚠️ Common Mistakes

* ❌ Trying to simulate swaps
* ❌ Using sorting (breaks positions)
* ❌ Not using fixed window size
* ❌ Forgetting to update both sides of window

---

## 🎯 Key Insight

> Maximize already correct elements → minimize swaps

---

## 🧠 One-Line Summary

```text
Minimum swaps = total_good - max_good_in_window
```

---

## 🔁 Pattern Connection

| Problem           | Technique      |
| ----------------- | -------------- |
| Min swaps         | Sliding window |
| Max sum (fixed k) | Sliding window |
| Range sum         | Prefix sum     |

---

## 🔥 Final Thought

👉 This is a **classic sliding window problem**
👉 Convert swapping problem → counting problem
👉 Think in terms of windows, not operations

---
