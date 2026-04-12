# 🧠 Counting Pairs ("a" before "b") — Carry Forward Technique

---

## 📌 Problem Statement

Given a string `s`, count the number of pairs:

```text
(i, j) such that:
i < j AND s[i] = 'a' AND s[j] = 'b'
```

👉 In simple words:

> Count how many times **'a' appears before 'b'** in the string.

---

## 💡 Example

```text
s = "baabdcabb"
```

We need to count all valid `(a, b)` pairs.

---

## 🔥 Key Idea (Carry Forward from Right)

Instead of checking all pairs (**O(n²)** ❌),
we **traverse from right → left** and:

* Maintain count of `'b'` seen so far
* For every `'a'`, add all those `'b'` to answer

---

## 🧠 Intuition

* Think: “How many `'b'` are to the right of this `'a'`?”
* If there are `k` `'b'`, then this `'a'` contributes `k` pairs

---

## 🚀 Algorithm

1. Initialize:

```cpp
cb = 0   // count of 'b'
ans = 0  // result
```

2. Traverse from right → left:

   * If `'b'` → increment `cb`
   * If `'a'` → add `cb` to `ans`

3. Return `ans`

---

## ✅ Code

```cpp
#include <iostream>
using namespace std;

int pairFind(string s)
{
    int n = s.size();
    int cb = 0;   // count of 'b'
    int ans = 0;

    for (int i = n - 1; i >= 0; i--)
    {
        if (s[i] == 'b')
            cb++;
        else if (s[i] == 'a')
            ans += cb;
    }
    return ans;
}

int main()
{
    string s = "baabdcabb";
    cout << pairFind(s) << endl;
    return 0;
}
```

---

## 🔍 Dry Run

```text
s = "baabdcabb"
```

Traverse from right:

| Index | Char | cb (b count) | ans |
| ----- | ---- | ------------ | --- |
| 8     | b    | 1            | 0   |
| 7     | b    | 2            | 0   |
| 6     | a    | 2            | 2   |
| 5     | c    | 2            | 2   |
| 4     | d    | 2            | 2   |
| 3     | b    | 3            | 2   |
| 2     | a    | 3            | 5   |
| 1     | a    | 3            | 8   |
| 0     | b    | 4            | 8   |

👉 Final Answer:

```text
8
```

---

## ⏱️ Complexity

| Type  | Value |
| ----- | ----- |
| Time  | O(n)  |
| Space | O(1)  |

---

## ⚠️ Common Mistakes

* ❌ Using nested loops → O(n²)
* ❌ Traversing left → right (harder logic)
* ❌ Forgetting to count all future `'b'`

---

## 🎯 Key Insight

> Each `'a'` pairs with **all future ****`'b'`**

---

## 🧠 One-Line Summary

```text
For every 'a', add number of 'b' to its right.
```

---

## 🚀 Bonus (Generalization)

You can solve similar problems like:

* Count pairs `(x, y)` where `x < y`
* Count inversions (advanced)
* Count "01" pairs in binary strings

---

## 🔥 Final Thought

This is a classic **carry-forward pattern from right**:

👉 Store future information → use it instantly
👉 Avoid recomputation → achieve O(n)

---
