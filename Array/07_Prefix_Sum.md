> 🔢 **Pattern: Array – Prefix Sum**  
> Precompute cumulative sums to answer range sum queries in O(1).

---

### ✅ 1. What is Prefix Sum?

- `prefix[i] = nums[0] + nums[1] + ... + nums[i]`  
- `prefix[0] = nums[0]`  
- For `i > 0`, `prefix[i] = prefix[i-1] + nums[i]`

**Idea:**
- Precompute prefix array once.  
- Sum of subarray from `l` to `r` = `prefix[r] - prefix[l-1]` (if `l > 0`).

```cpp
// Build prefix sum array
vector<int> buildPrefixSum(vector<int>& nums) {
    int n = nums.size();
    vector<int> prefix(n);
    prefix = nums;
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i-1] + nums[i];
    }
    return prefix;
}

// Range sum query: sum from l to r
int rangeSum(vector<int>& prefix, int l, int r) {
    if (l == 0) return prefix[r];
    return prefix[r] - prefix[l-1];
}
```

- **Preprocessing Time:** O(n)  
- **Query Time:** O(1)  
- **Space:** O(n)

---

### ✅ 2. Range Sum Query – Immutable (LeetCode 303)

**Idea:**
- Precompute prefix sum in constructor.  
- For each query, use `prefix[r] - prefix[l-1]`.

```cpp
class NumArray {
private:
    vector<int> prefix;
public:
    NumArray(vector<int>& nums) {
        int n = nums.size();
        prefix.resize(n);
        if (n > 0) {
            prefix = nums;
            for (int i = 1; i < n; i++) {
                prefix[i] = prefix[i-1] + nums[i];
            }
        }
    }
    
    int sumRange(int left, int right) {
        if (left == 0) return prefix[right];
        return prefix[right] - prefix[left-1];
    }
};
```

- **Time:** O(n) preprocessing, O(1) per query  
- **Space:** O(n)

---

### ✅ 3. Subarray Sum Equals K (LeetCode 560)

**Idea:**
- Use prefix sum and a hash map to store frequency of each prefix sum.  
- If `prefix[i] - k` exists in map, then there is a subarray ending at `i` with sum `k`.

```cpp
int subarraySum(vector<int>& nums, int k) {
    unordered_map<int, int> prefixCount;
    prefixCount = 1;  // empty prefix
    
    int prefix = 0, count = 0;
    for (int num : nums) {
        prefix += num;
        if (prefixCount.find(prefix - k) != prefixCount.end()) {
            count += prefixCount[prefix - k];
        }
        prefixCount[prefix]++;
    }
    return count;
}
```

- **Time:** O(n)  
- **Space:** O(n)

---

### ✅ 4. Running Sum of 1d Array (LeetCode 1480)

```cpp
vector<int> runningSum(vector<int>& nums) {
    vector<int> result = nums;
    for (int i = 1; i < nums.size(); i++) {
        result[i] += result[i-1];
    }
    return result;
}
```

- **Time:** O(n)  
- **Space:** O(1) extra (if modifying input allowed)

---

### ⏱️ Complexity Summary

| Problem Type                     | Time       | Space     |
|----------------------------------|------------|-----------|
| Build Prefix Array               | O(n)       | O(n)      |
| Range Sum Query                  | O(1)       | O(1)      |
| Subarray Sum Equals K            | O(n)       | O(n)      |
| Running Sum                      | O(n)       | O(1)      |

---

### 📌 Key Takeaways

- Use prefix sum when you need to answer many range sum queries.  
- For “subarray sum equals K”, use prefix sum + hash map.  
- Remember: `sum(l, r) = prefix[r] - prefix[l-1]` (handle `l=0` separately).  
- Always initialize `prefix[0] = nums[0]` and handle empty array edge case.
