> 🔢 **Pattern: Array – Frequency Counting**  
> Count frequency of elements using map/array; solve problems like duplicates, missing numbers, anagrams, etc.

---

### ✅ 1. Count Frequency Using Map

**Idea:**  
- Use `unordered_map<int, int>` to store frequency of each element.  
- Iterate once to build frequency map, then use it to answer queries.

```cpp
unordered_map<int, int> buildFrequencyMap(vector<int>& nums) {
    unordered_map<int, int> freq;
    for (int num : nums) {
        freq[num]++;
    }
    return freq;
}
```

- **Time:** O(n)  
- **Space:** O(n)

---

### ✅ 2. Find All Duplicates in Array

**Idea:**  
- Use frequency map: if `freq[num] > 1`, it’s a duplicate.  
- Or, if array elements are in range `[1, n]`, use array itself as frequency map (mark negative).

```cpp
// Using map
vector<int> findDuplicates(vector<int>& nums) {
    unordered_map<int, int> freq;
    vector<int> duplicates;
    for (int num : nums) {
        freq[num]++;
        if (freq[num] == 2) {
            duplicates.push_back(num);
        }
    }
    return duplicates;
}
```

```cpp
// In-place (for 1 ≤ nums[i] ≤ n)
vector<int> findDuplicates(vector<int>& nums) {
    vector<int> duplicates;
    for (int num : nums) {
        int index = abs(num) - 1;
        if (nums[index] < 0) {
            duplicates.push_back(abs(num));
        } else {
            nums[index] = -nums[index];
        }
    }
    // Restore original array (optional)
    for (int& num : nums) num = abs(num);
    return duplicates;
}
```

- **Time:** O(n)  
- **Space:** O(1) extra (in-place version)

---

### ✅ 3. Find Missing Number (1 to n)

**Idea:**  
- Use frequency map: iterate from `1` to `n`, return the one with `freq[i] == 0`.  
- Or, use sum: `expectedSum - actualSum`.

```cpp
// Using frequency map
int missingNumber(vector<int>& nums) {
    unordered_set<int> present(nums.begin(), nums.end());
    int n = nums.size();
    for (int i = 0; i <= n; i++) {
        if (present.find(i) == present.end()) {
            return i;
        }
    }
    return -1;
}
```

```cpp
// Using sum
int missingNumber(vector<int>& nums) {
    int n = nums.size();
    int expectedSum = n * (n + 1) / 2;
    int actualSum = 0;
    for (int num : nums) {
        actualSum += num;
    }
    return expectedSum - actualSum;
}
```

- **Time:** O(n)  
- **Space:** O(1) (sum version)

---

### ✅ 4. Check Anagram (Two Strings)

**Idea:**  
- Build frequency map for both strings.  
- Two strings are anagrams if their frequency maps are equal.

```cpp
bool isAnagram(string s, string t) {
    if (s.length() != t.length()) return false;
    
    unordered_map<char, int> freq;
    for (char c : s) freq[c]++;
    for (char c : t) freq[c]--;
    
    for (auto& p : freq) {
        if (p.second != 0) return false;
    }
    return true;
}
```

- **Time:** O(n)  
- **Space:** O(1) (if only lowercase letters, map size ≤ 26)

---

### ✅ 5. Subarray Sum Equals K (Using Prefix + Frequency)

**Idea:**  
- Use prefix sum and a map to store frequency of each prefix sum.  
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

### ⏱️ Complexity Summary

| Problem Type                     | Time       | Space     |
|----------------------------------|------------|-----------|
| Build Frequency Map              | O(n)       | O(n)      |
| Find Duplicates (map)            | O(n)       | O(n)      |
| Find Duplicates (in-place)       | O(n)       | O(1)      |
| Missing Number (sum)             | O(n)       | O(1)      |
| Anagram Check                    | O(n)       | O(1)      |
| Subarray Sum Equals K            | O(n)       | O(n)      |

---

### 📌 Key Takeaways

- Use **frequency map** when you need to count how many times each element appears.  
- For **duplicates/missing** in range `[1, n]`, consider in-place marking (negate) to save space.  
- For **anagram**, compare frequency maps of two strings.  
- For **subarray sum equals K**, combine prefix sum with frequency map.  
- Always think: can we use the array itself as a frequency map to reduce space?
