# 🧠 Counting Triplets ("a" before "b" before "a") — Carry Forward Technique

---

## 📌 Problem Statement

Given a string `s`, count the number of triplets:

```text
(i, j, k) such that:
i < j < k AND s[i] = 'a', s[j] = 'b', s[k] = 'a'
```

👉 In simple words:

> Count how many times pattern **"a b a"** appears (not necessarily contiguous).

---

## 💡 Example

```text
s = "baabdcabbba"
```

We need to count all valid `(a, b, a)` triplets.

---

## 🔥 Key Idea (Carry Forward Both Sides)

We use a **two-side carry forward idea**:

* Left side → number of `'a'` before current index → `la`
* Right side → number of `'a'` after current index → `ra`

👉 For every `'b'`:

```text
triplets formed = la × ra
```

---

## 🧠 Intuition

At each `'b'`:

* Choose any `'a'` from left
* Choose any `'a'` from right

👉 Total combinations:

```text
la * ra
```

---

## 🚀 Algorithm

### Step 1: Count total `'a'`

```cpp
T = total count of 'a'
```

---

### Step 2: Traverse array

* Maintain:

```cpp
la = number of 'a' seen so far
```

* For each index:

  * If `'b'`:

    ```cpp
    ra = T - la
    ans += la * ra
    ```
  * If `'a'`:

    ```cpp
    la++
    ```

---

## ✅ Code

```cpp
#include <iostream>
#include <string>
using namespace std;

int tripletFind(string s)
{
    int n = s.size();
    int ans = 0;

    int T = 0;   // total 'a'
    int la = 0;  // left 'a'

    // count total 'a'
    for (int i = 0; i < n; i++)
    {
        if (s[i] == 'a')
            T++;
    }

    // main logic
    for (int j = 0; j < n; j++)
    {
        if (s[j] == 'b')
        {
            int ra = T - la;   // right 'a'
            ans += la * ra;
        }

        if (s[j] == 'a')
            la++;
    }

    return ans;
}

int main()
{
    string s = "baabdcabbba";
    cout << tripletFind(s) << endl;
    return 0;
}
```

---

## 🔍 Dry Run

```text
s = "baabdcabbba"
```

Total `'a'`:

```text
T = 4
```

| Index | Char | la | ra = T-la | Contribution | ans |
| ----- | ---- | -- | --------- | ------------ | --- |
| 0     | b    | 0  | 4         | 0            | 0   |
| 1     | a    | 1  | -         | -            | 0   |
| 2     | a    | 2  | -         | -            | 0   |
| 3     | b    | 2  | 2         | 4            | 4   |
| 4     | d    | 2  | -         | -            | 4   |
| 5     | c    | 2  | -         | -            | 4   |
| 6     | a    | 3  | -         | -            | 4   |
| 7     | b    | 3  | 1         | 3            | 7   |
| 8     | b    | 3  | 1         | 3            | 10  |
| 9     | b    | 3  | 1         | 3            | 13  |
| 10    | a    | 4  | -         | -            | 13  |

👉 Final Answer:

```text
13
```

---

## ⏱️ Complexity

| Type  | Value |
| ----- | ----- |
| Time  | O(n)  |
| Space | O(1)  |

---

## ⚠️ Common Mistakes

* ❌ Trying triple loops → O(n³)
* ❌ Not precomputing total `'a'`
* ❌ Forgetting order (i < j < k)
* ❌ Mixing left and right counts

---

## 🎯 Key Insight

> Each `'b'` acts as a **bridge** connecting left `'a'` and right `'a'`.

---

## 🧠 One-Line Summary

```text
For every 'b', add (left a count × right a count)
```

---

## 🚀 Pattern Recognition

This is a **next-level carry-forward pattern**:

| Problem Type      | Idea                  |
| ----------------- | --------------------- |
| Pair (a, b)       | Count from one side   |
| Triplet (a, b, a) | Count from both sides |

---

## 🔥 Final Thought

👉 This pattern is extremely powerful in:

* String problems
* Subsequence counting
* Combinatorics in arrays

---
