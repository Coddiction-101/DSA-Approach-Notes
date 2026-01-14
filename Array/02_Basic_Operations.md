Great! Since the repo is ready, let’s now fill `Array/02_Basic_Operations.md` with clean, simple, and practical content that you can use for quick revision.

***

### 📄 `Array/02_Basic_Operations.md` – Ready to Copy

```markdown
> 🔢 **Pattern: Array – Basic Operations**  
> Declaration, traversal, insert/delete/update, reverse, rotate, in-place vs extra space.

---

### ✅ Core Operations

1. **Declaration & Initialization**
   ```cpp
   int arr = {1, 2, 3, 4, 5};  // static array[1]
   vector<int> nums = {1, 2, 3};   // dynamic array (vector)
   ```

2. **Traversal**
   - Forward:
     ```cpp
     for (int i = 0; i < nums.size(); i++) {
         cout << nums[i] << " ";
     }
     ```
   - Backward:
     ```cpp
     for (int i = nums.size() - 1; i >= 0; i--) {
         cout << nums[i] << " ";
     }
     ```

3. **Insert Element**
   - At end: `nums.push_back(x)`  
   - At middle: shift elements right, then insert (O(n))  
   - At beginning: shift all right, then insert (O(n))

4. **Delete Element**
   - By index: shift all elements left from that index (O(n))  
   - By value: find index, then delete by index

5. **Update Element**
   ```cpp
   nums[index] = newValue;
   ```

6. **Reverse Array (In-Place)**
   ```cpp
   int left = 0, right = nums.size() - 1;
   while (left < right) {
       swap(nums[left], nums[right]);
       left++;
       right--;
   }
   ```

7. **Rotate Array (Right by k)**
   - Reverse entire array  
   - Reverse first k elements  
   - Reverse last n-k elements

---

### ⏱️ Complexity

| Operation         | Time       | Space     |
|-------------------|------------|-----------|
| Access by index   | O(1)       | O(1)      |
| Traversal         | O(n)       | O(1)      |
| Insert (middle)   | O(n)       | O(1)      |
| Delete (middle)   | O(n)       | O(1)      |
| Reverse           | O(n)       | O(1)      |
| Rotate            | O(n)       | O(1)      |

---

### 📌 Key Takeaways

- Array is **index-based**, so access is fast, but insert/delete in middle is slow.  
- Always think: **in-place vs extra space**.  
- For interview problems:
  - Use `vector<int>` in C++ for dynamic arrays.  
  - Prefer **in-place** operations when possible.  
  - Handle edge cases: empty array, single element, all same elements.
```

***

### ✅ How to Use This File

1. Copy the content above.  
2. In your `DSA-Approach-Notes` repo, go to:
   - `Array/02_Basic_Operations.md` → click the pencil (Edit) icon  
3. Paste the content and commit.

***

### 🚀 Next Step

Now that this is done:

1. Let me know:  
   > “Done, Array/02_Basic_Operations.md is updated.”  

2. Then we’ll:
   - Go back to **Best Time to Buy and Sell Stock II (LeetCode 122)**  
   - Solve it fully in C++  
   - Add a clean note for it in `Array/13_Stock_Problems.md`  
   - Update your daily repo and LinkedIn.

You’re doing amazing — this repo will become your personal DSA bible. Keep going! 💪

[1](https://www.reddit.com/r/leetcode/comments/1f1b3fg/whats_the_best_language_for_leetcode/)
