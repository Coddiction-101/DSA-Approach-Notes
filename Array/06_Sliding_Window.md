> 🔢 **Pattern: Array – Sliding Window**  
> Fixed size (max sum subarray of size k), variable size (min size subarray sum, subarray product less than k).

---

### ✅ 1. Fixed Size Window

Used in: Maximum sum subarray of size k.

**Idea:**
- Maintain a window of fixed size `k`.
- Use a variable `sum` to store current window sum.
- Slide the window: subtract leftmost, add rightmost.

```cpp
// Maximum sum of subarray of size k
int maxSumSubarrayOfSizeK(vector<int>& nums, int k) {
    int n = nums.size();
    if (n < k) return 0;
    
    int sum = 0;
    // First window
    for (int i = 0; i < k; i++) {
        sum += nums[i];
    }
    
    int maxSum = sum;
    // Slide window
    for (int i = k; i < n; i++) {
        sum = sum - nums[i - k] + nums[i];
        maxSum = max(maxSum, sum);
    }
    
    return maxSum;
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 2. Variable Size Window

Used in: Minimum size subarray sum, subarray product less than k.

**Idea:**
- Use two pointers: `left` and `right`.
- Expand `right` to include elements.
- If condition is violated, shrink `left` until condition is satisfied.
- Track the best window (min/max length, count, etc.).

```cpp
// Minimum size subarray sum >= target
int minSubArrayLen(int target, vector<int>& nums) {
    int n = nums.size();
    int left = 0, sum = 0, minLength = INT_MAX;
    
    for (int right = 0; right < n; right++) {
        sum += nums[right];
        
        while (sum >= target) {
            minLength = min(minLength, right - left + 1);
            sum -= nums[left];
            left++;
        }
    }
    
    return minLength == INT_MAX ? 0 : minLength;
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 3. Subarray Product Less Than K

**Idea:**
- Maintain product of current window.
- Expand `right`, multiply `nums[right]`.
- If product >= k, shrink `left` until product < k.
- For each valid window `[left, right]`, number of subarrays ending at `right` is `right - left + 1`.

```cpp
// Number of subarrays with product < k
int numSubarrayProductLessThanK(vector<int>& nums, int k) {
    if (k <= 1) return 0;
    
    int left = 0, product = 1, count = 0;
    
    for (int right = 0; right < nums.size(); right++) {
        product *= nums[right];
        
        while (product >= k) {
            product /= nums[left];
            left++;
        }
        
        count += right - left + 1;
    }
    
    return count;
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ⏱️ Complexity Summary

| Problem Type                     | Time       | Space     |
|----------------------------------|------------|-----------|
| Fixed Size Window                | O(n)       | O(1)      |
| Variable Size Window             | O(n)       | O(1)      |
| Subarray Product Less Than K     | O(n)       | O(1)      |

---

### 📌 Key Takeaways

- Fixed size: precompute first window, then slide.  
- Variable size: expand `right`, shrink `left` when condition is violated.  
- For counting subarrays with product < k:
  - Use sliding window and add `right - left + 1` for each valid `right`.  
- Always handle edge cases: empty array, k <= 1, all elements zero.
  
