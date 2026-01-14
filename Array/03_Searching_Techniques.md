
Here’s the ready‑to‑copy content for `Array/03_Searching_Techniques.md` — clean, simple, and interview‑focused.

```markdown
> 🔢 **Pattern: Array – Searching Techniques**  
> Linear Search, Binary Search, First/Last Occurrence, Search in Rotated Array.

---

### ✅ 1. Linear Search

- Search element in an **unsorted** array.  
- Traverse each element one by one.

```cpp
int linearSearch(vector<int>& nums, int target) {
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] == target) {
            return i;  // return index
        }
    }
    return -1;  // not found
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 2. Binary Search (Sorted Array)

- Only works on **sorted** arrays.  
- Compare target with middle element and reduce search space by half.

```cpp
int binarySearch(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    
    return -1;  // not found
}
```

- **Time:** O(log n)  
- **Space:** O(1)

---

### ✅ 3. First and Last Occurrence

- Find first index where `target` appears.  
- Find last index where `target` appears.

**Idea:**
- For first: when `nums[mid] == target`, store `mid` and move `right = mid - 1`.  
- For last: when `nums[mid] == target`, store `mid` and move `left = mid + 1`.

- **Time:** O(log n)  
- **Space:** O(1)

---

### ✅ 4. Search Insert Position

- If `target` is found, return its index.  
- Else, return the index where it should be inserted to keep sorted order.

**Idea:**
- Use binary search; at the end, `left` is the correct insert position.

- **Time:** O(log n)  
- **Space:** O(1)

---

### ✅ 5. Search in Rotated Sorted Array

- Array is rotated at some pivot.  
- Use modified binary search to decide which half is sorted.

**Idea:**
- Check if left half is sorted.  
- If yes, check if target lies in it; else go to right half.  
- Repeat.

- **Time:** O(log n)  
- **Space:** O(1)

---

### ⏱️ Complexity Summary

| Technique                     | Time       | Space     |
|-------------------------------|------------|-----------|
| Linear Search                 | O(n)       | O(1)      |
| Binary Search                 | O(log n)   | O(1)      |
| First/Last Occurrence         | O(log n)   | O(1)      |
| Search Insert Position        | O(log n)   | O(1)      |
| Search in Rotated Sorted Array| O(log n)   | O(1)      |

---

### 📌 Key Takeaways

- Use **Linear Search** for unsorted arrays.  
- Use **Binary Search** only on sorted arrays.  
- For **rotated arrays**, think: which half is sorted?  
- Always handle edge cases: empty array, single element, duplicates.
```

***

### ✅ How to Use

1. Copy the content above.  
2. In your `DSA-Approach-Notes` repo, go to:  
   `Array/03_Searching_Techniques.md` → click the pencil (Edit) icon  
3. Paste and commit.

Once done, just say:  
> “Done, Array/03_Searching_Techniques.md is updated.”

and we’ll move to the next file or go back to solving **Best Time to Buy and Sell Stock II**. You’re doing great — keep this momentum! 💪
