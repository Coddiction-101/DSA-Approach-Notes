> 🔢 **Pattern: Array – Rearrangement**  
> Move zeros, segregate negatives/positives, alternate signs, parity-based, wiggle.

---

### ✅ 1. Move Zeros to End

**Idea:**  
- Use a write pointer `k` to place non-zero elements at the front.  
- After the loop, fill the rest with zeros.

```cpp
void moveZeroes(vector<int>& nums) {
    int k = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] != 0) {
            nums[k++] = nums[i];
        }
    }
    while (k < nums.size()) {
        nums[k++] = 0;
    }
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 2. Segregate Negative and Positive

**Idea:**  
- Use a partition-like approach: maintain index `j` for next negative position.  
- Traverse and swap every negative element to the left.

```cpp
void segregateNegPos(vector<int>& nums) {
    int j = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] < 0) {
            swap(nums[i], nums[j]);
            j++;
        }
    }
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 3. Rearrange to Alternate Positive and Negative

**Idea:**  
- First, partition array into negatives (left) and positives (right).  
- Then, swap every second negative with the next positive.

```cpp
void rearrangeAlternatePosNeg(vector<int>& nums) {
    int n = nums.size();
    int j = 0;
    for (int i = 0; i < n; i++) {
        if (nums[i] < 0) {
            swap(nums[i], nums[j]);
            j++;
        }
    }
    int pos = j, neg = 0;
    while (pos < n && neg < pos && nums[neg] < 0) {
        swap(nums[neg], nums[pos]);
        pos++;
        neg += 2;
    }
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 4. Sort Array by Parity (Even–Odd Indices)

**Idea:**  
- Place even numbers at even indices, odd numbers at odd indices.  
- Use two pointers: `i` for even index, `j` for odd index.

```cpp
void sortArrayByParityII(vector<int>& nums) {
    int n = nums.size();
    int i = 0, j = 1;
    while (i < n && j < n) {
        if (nums[i] % 2 == 0) {
            i += 2;
        } else if (nums[j] % 2 == 1) {
            j += 2;
        } else {
            swap(nums[i], nums[j]);
            i += 2;
            j += 2;
        }
    }
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 5. Wiggle Sort (Peak–Valley)

**Idea:**  
- Sort the array first.  
- Swap adjacent elements (1st & 2nd, 3rd & 4th, ...) to create a wiggle pattern.

```cpp
void wiggleSort(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    for (int i = 1; i + 1 < nums.size(); i += 2) {
        swap(nums[i], nums[i + 1]);
    }
}
```

- **Time:** O(n log n)  
- **Space:** O(1)

---

### ⏱️ Complexity Summary

| Problem Type                     | Time       | Space     |
|----------------------------------|------------|-----------|
| Move Zeros                       | O(n)       | O(1)      |
| Segregate Neg/Pos                | O(n)       | O(1)      |
| Alternate Pos/Neg                | O(n)       | O(1)      |
| Sort by Parity II                | O(n)       | O(1)      |
| Wiggle Sort                      | O(n log n) | O(1)      |

---

### 📌 Key Takeaways

- Use **two pointers** (write pointer or index pointers) for in-place rearrangement.  
- For **alternate sign** problems: partition first, then swap in a pattern.  
- For **parity-based** problems: maintain separate even/odd index pointers.  
- For **wiggle/peak–valley**: sort first, then swap adjacent pairs.  
- Always handle edge cases: empty array, all positive, all negative, single element.
```
