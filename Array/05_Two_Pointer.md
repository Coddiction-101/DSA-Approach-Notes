Here’s the ready‑to‑copy content for `Array/05_Two_Pointer.md` — clean, simple, and focused on what matters for interviews.

```markdown
> 🔢 **Pattern: Array – Two Pointer**  
> Same direction (remove duplicates, move zeros), opposite direction (two sum, three sum, container with most water).

---

### ✅ 1. Same Direction (Write Pointer)

Used in: Remove Element, Remove Duplicates, Move Zeroes.

**Idea:**
- Use a write pointer `k` that points to the next position where a valid element should be placed.
- Traverse the array with index `i`:
  - If `nums[i]` is valid (≠ val, not duplicate, not zero), copy it to `nums[k]` and increment `k`.
- Return `k` as the new length.

```cpp
// Remove Element
int removeElement(vector<int>& nums, int val) {
    int k = 0;
    for (int i = 0; i < nums.size(); i++) {
        if (nums[i] != val) {
            nums[k] = nums[i];
            k++;
        }
    }
    return k;
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 2. Opposite Direction (Two Sum, Container With Most Water)

Used in: Two Sum (sorted), Three Sum, Container With Most Water.

**Idea:**
- One pointer at start (`left`), one at end (`right`).
- Move pointers based on condition:
  - If sum is too small → `left++`
  - If sum is too large → `right--`
  - If sum is correct → record and move both.

```cpp
// Two Sum II (sorted array)
vector<int> twoSum(vector<int>& nums, int target) {
    int left = 0, right = nums.size() - 1;
    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) {
            return {left + 1, right + 1};  // 1-indexed
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }
    return {};
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 3. Three Sum / Four Sum

**Idea:**
- Fix one element, then use two pointers on the remaining array.
- For duplicates: skip same values after using them.

```cpp
// Three Sum
vector<vector<int>> threeSum(vector<int>& nums) {
    sort(nums.begin(), nums.end());
    vector<vector<int>> result;
    int n = nums.size();
    
    for (int i = 0; i < n - 2; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;  // skip duplicates
        
        int left = i + 1, right = n - 1;
        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            if (sum == 0) {
                result.push_back({nums[i], nums[left], nums[right]});
                while (left < right && nums[left] == nums[left + 1]) left++;
                while (left < right && nums[right] == nums[right - 1]) right--;
                left++;
                right--;
            } else if (sum < 0) {
                left++;
            } else {
                right--;
            }
        }
    }
    return result;
}
```

- **Time:** O(n²)  
- **Space:** O(1) (excluding output)

---

### ✅ 4. Container With Most Water

**Idea:**
- Use two pointers at both ends.
- Area = `min(height[left], height[right]) * (right - left)`
- Move the pointer with smaller height inward.

```cpp
int maxArea(vector<int>& height) {
    int left = 0, right = nums.size() - 1;
    int maxArea = 0;
    
    while (left < right) {
        int area = min(height[left], height[right]) * (right - left);
        maxArea = max(maxArea, area);
        
        if (height[left] < height[right]) {
            left++;
        } else {
            right--;
        }
    }
    return maxArea;
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ⏱️ Complexity Summary

| Problem Type               | Time       | Space     |
|----------------------------|------------|-----------|
| Same Direction (Write Ptr)| O(n)       | O(1)      |
| Opposite Direction         | O(n)       | O(1)      |
| Three Sum / Four Sum       | O(n²)      | O(1)      |
| Container With Most Water  | O(n)       | O(1)      |

---

### 📌 Key Takeaways

- Same direction: use a **write pointer** for in-place modification.  
- Opposite direction: use **left and right** pointers for sorted arrays.  
- For Three Sum:
  - Sort first.  
  - Fix one, use two pointers on rest.  
  - Skip duplicates.  
- For Container With Most Water:
  - Move the pointer with smaller height.  
  - Greedy: we never lose the optimal solution by moving the smaller one.
```
