```markdown
> 🔢 **Pattern: Array – Kadane’s Algorithm**  
> Maximum subarray sum (Kadane), minimum subarray sum, circular subarray.

---

### ✅ 1. Kadane’s Algorithm (Maximum Subarray Sum)

**Idea:**
- At each index, decide: extend the current subarray or start a new one.  
- `maxEndingHere = max(nums[i], maxEndingHere + nums[i])`  
- `maxSoFar = max(maxSoFar, maxEndingHere)`

```cpp
int maxSubArray(vector<int>& nums) {
    int maxEndingHere = nums;
    int maxSoFar = nums;
    
    for (int i = 1; i < nums.size(); i++) {
        maxEndingHere = max(nums[i], maxEndingHere + nums[i]);
        maxSoFar = max(maxSoFar, maxEndingHere);
    }
    
    return maxSoFar;
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 2. Minimum Subarray Sum

Same idea, but track minimum.

```cpp
int minSubArray(vector<int>& nums) {
    int minEndingHere = nums;
    int minSoFar = nums;
    
    for (int i = 1; i < nums.size(); i++) {
        minEndingHere = min(nums[i], minEndingHere + nums[i]);
        minSoFar = min(minSoFar, minEndingHere);
    }
    
    return minSoFar;
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 3. Maximum Circular Subarray Sum

**Idea:**
- Case 1: Maximum subarray is non‑circular → use Kadane.  
- Case 2: Maximum subarray is circular → wrap around.  
  - Total sum – minimum subarray sum (middle part)  
- Answer = `max(nonCircular, circular)`  
- Special case: if all numbers are negative, return `maxSoFar`.

```cpp
int maxCircularSubarray(vector<int>& nums) {
    int totalSum = 0;
    int maxEndingHere = nums, maxSoFar = nums;
    int minEndingHere = nums, minSoFar = nums;
    
    for (int num : nums) {
        totalSum += num;
        
        // Kadane for max
        maxEndingHere = max(num, maxEndingHere + num);
        maxSoFar = max(maxSoFar, maxEndingHere);
        
        // Kadane for min
        minEndingHere = min(num, minEndingHere + num);
        minSoFar = min(minSoFar, minEndingHere);
    }
    
    // If all elements are negative, maxSoFar is the answer
    if (totalSum == minSoFar) {
        return maxSoFar;
    }
    
    return max(maxSoFar, totalSum - minSoFar);
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 4. Maximum Sum of Non‑Overlapping Subarrays

**Idea:**
- Use Kadane to compute maximum subarray sum ending at each index.  
- Then use another pass to compute maximum sum of two non‑overlapping subarrays.

```cpp
// Maximum sum of two non‑overlapping subarrays (each of size k)
int maxSumTwoNoOverlap(vector<int>& nums, int firstLen, int secondLen) {
    int n = nums.size();
    vector<int> prefix(n + 1, 0);
    for (int i = 0; i < n; i++) {
        prefix[i + 1] = prefix[i] + nums[i];
    }
    
    // Helper: max sum of subarray of length len ending at or before i
    auto maxSum = [&](int len) {
        vector<int> maxSum(n + 1, 0);
        int sum = 0;
        for (int i = 0; i < len; i++) {
            sum += nums[i];
        }
        maxSum[len] = sum;
        for (int i = len; i < n; i++) {
            sum = sum - nums[i - len] + nums[i];
            maxSum[i + 1] = max(maxSum[i], sum);
        }
        return maxSum;
    };
    
    vector<int> maxFirst = maxSum(firstLen);
    vector<int> maxSecond = maxSum(secondLen);
    
    int result = 0;
    for (int i = firstLen + secondLen; i <= n; i++) {
        result = max(result, maxFirst[i - secondLen] + maxSecond[i]);
        result = max(result, maxSecond[i - firstLen] + maxFirst[i]);
    }
    return result;
}
```

- **Time:** O(n)  
- **Space:** O(n)

---

### ⏱️ Complexity Summary

| Problem Type                     | Time       | Space     |
|----------------------------------|------------|-----------|
| Maximum Subarray (Kadane)        | O(n)       | O(1)      |
| Minimum Subarray                 | O(n)       | O(1)      |
| Maximum Circular Subarray        | O(n)       | O(1)      |
| Two Non‑Overlapping Subarrays    | O(n)       | O(n)      |

---

### 📌 Key Takeaways

- Kadane: at each step, choose `nums[i]` or `maxEndingHere + nums[i]`.  
- For circular subarray: answer = `max(nonCircular, totalSum - minSubarray)`.  
- Handle the all‑negative case: if `totalSum == minSoFar`, return `maxSoFar`.  
- For two non‑overlapping subarrays, use prefix sums and precomputed max subarray sums.
  
