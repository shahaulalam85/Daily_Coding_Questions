# 🧠 Maximum Sum of Subarray of Size K — All Approaches

---

## 📌 Problem Statement

Given an array `a` and an integer `k`, find:

```text
Maximum sum of any subarray of size k
```

---

## 💡 Example

```text
Array: [-7, 1, 5, 2, -4, 3, 0, 10]
k = 3
```

Subarrays of size 3:

```text
[-7,1,5] → -1  
[1,5,2] → 8  
[5,2,-4] → 3  
[2,-4,3] → 1  
[-4,3,0] → -1  
[3,0,10] → 13  ✅
```

👉 Output:

```text
13
```

---

# 🔴 1. Brute Force Approach

## 💡 Idea

* Generate every subarray of size `k`
* Compute sum each time

---

## ✅ Code

```cpp
long maxSum(vector<int> &a, int k)
{
    int n = a.size(), i = 0, j = k - 1;
    long ans = LONG_MIN;

    while (j < n)
    {
        long sum = 0;

        for (int h = i; h <= j; h++)
        {
            sum += a[h];
        }

        ans = max(ans, sum);
        i++;
        j++;
    }

    return ans;
}
```

---

## ⏱️ Complexity

| Type  | Value      |
| ----- | ---------- |
| Time  | O(n × k) ❌ |
| Space | O(1)       |

---

## ⚠️ Problem

👉 Recomputes sum every time → inefficient

---

# 🟡 2. Prefix Sum Approach

## 💡 Idea

* Precompute cumulative sums
* Use formula to get range sum in O(1)

---

## ✅ Code

```cpp
long maxSum(vector<int> &a, int k)
{
    int n = a.size();
    vector<long> ps(n);

    ps[0] = a[0];
    for (int i = 1; i < n; i++)
        ps[i] = ps[i - 1] + a[i];

    long ans = ps[k - 1];

    for (int i = 1, j = k; j < n; i++, j++)
    {
        long s = ps[j] - ps[i - 1];
        ans = max(ans, s);
    }

    return ans;
}
```

---

## ⏱️ Complexity

| Type  | Value  |
| ----- | ------ |
| Time  | O(n) ✅ |
| Space | O(n) ❌ |

---

## ⚠️ Problem

👉 Extra space used for prefix array

---

# 🟢 3. Sliding Window (Optimal)

## 💡 Idea

👉 Instead of recomputing:

```text
Next window = Previous window + new element - removed element
```

---

## 🔑 Key Formula

```text
sum = sum + a[j] - a[i-1]
```

---

## ✅ Code

```cpp
long maxSum(vector<int> &a, int k)
{
    int n = a.size();

    long sum = 0, maxSumVal = LONG_MIN;

    // first window
    for (int i = 0; i < k; i++)
        sum += a[i];

    maxSumVal = sum;

    // sliding
    for (int i = k; i < n; i++)
    {
        sum += a[i] - a[i - k];
        maxSumVal = max(maxSumVal, sum);
    }

    return maxSumVal;
}
```

---

## ⏱️ Complexity

| Type  | Value  |
| ----- | ------ |
| Time  | O(n) ✅ |
| Space | O(1) ✅ |

---

# 🔥 Comparison Summary

| Approach       | Time  | Space | Idea               |
| -------------- | ----- | ----- | ------------------ |
| Brute Force    | O(nk) | O(1)  | Recompute sum      |
| Prefix Sum     | O(n)  | O(n)  | Precompute sums    |
| Sliding Window | O(n)  | O(1)  | Reuse previous sum |

---

# 🧠 Intuition Ladder (VERY IMPORTANT)

```text
Brute Force → Recompute everything
Prefix Sum  → Store past work
Sliding Window → Reuse last result
```

---

# ⚠️ Common Mistakes

* ❌ Forgetting first window initialization
* ❌ Wrong index (`i-k` vs `i-1`)
* ❌ Not handling k > n
* ❌ Using int → overflow risk

---

# 🎯 Key Insight

> Sliding window avoids redundant computation by updating only changed elements

---

# 🧠 One-Line Summary

```text
Move window → add next element → remove previous element
```

---

# 🚀 Interview Tip

If interviewer asks:

👉 Start with brute force
👉 Optimize to prefix sum
👉 Final answer = sliding window

---

# 🔥 Final Thought

👉 This is one of the **most important patterns in DSA**
👉 Used in:

* Fixed window problems
* Maximum/minimum subarray
* String problems

---
