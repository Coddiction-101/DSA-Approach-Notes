> 🔢 **Pattern: Array – Intervals**  
> Merge, insert, erase, and check overlap in intervals (start, end).

---

### ✅ 1. Merge Overlapping Intervals

**Idea:**  
- Sort intervals by start time.  
- Traverse and merge if current interval overlaps with the last merged interval.

```cpp
vector<vector<int>> merge(vector<vector<int>>& intervals) {
    if (intervals.empty()) return {};
    
    // Sort by start time
    sort(intervals.begin(), intervals.end());
    
    vector<vector<int>> merged;
    merged.push_back(intervals);
    
    for (int i = 1; i < intervals.size(); i++) {
        int lastEnd = merged.back();
        int currStart = intervals[i];
        int currEnd = intervals[i];
        
        if (currStart <= lastEnd) {
            // Overlap: merge
            merged.back() = max(lastEnd, currEnd);
        } else {
            // No overlap: add new interval
            merged.push_back(intervals[i]);
        }
    }
    
    return merged;
}
```

- **Time:** O(n log n)  
- **Space:** O(1) extra (excluding output)

---

### ✅ 2. Insert Interval

**Idea:**  
- Add all intervals that end before the new interval starts.  
- Merge overlapping intervals with the new interval.  
- Add all intervals that start after the new interval ends.

```cpp
vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
    vector<vector<int>> result;
    int i = 0, n = intervals.size();
    
    // Add all intervals ending before newInterval starts
    while (i < n && intervals[i] < newInterval) {
        result.push_back(intervals[i]);
        i++;
    }
    
    // Merge all overlapping intervals with newInterval
    while (i < n && intervals[i] <= newInterval) {
        newInterval = min(newInterval, intervals[i]);
        newInterval = max(newInterval, intervals[i]);
        i++;
    }
    result.push_back(newInterval);
    
    // Add remaining intervals
    while (i < n) {
        result.push_back(intervals[i]);
        i++;
    }
    
    return result;
}
```

- **Time:** O(n)  
- **Space:** O(1) extra (excluding output)

---

### ✅ 3. Erase/Remove Overlapping Intervals

**Idea:**  
- Sort by end time.  
- Greedily keep the interval with the smallest end time to minimize overlap.

```cpp
int eraseOverlapIntervals(vector<vector<int>>& intervals) {
    if (intervals.empty()) return 0;
    
    // Sort by end time
    sort(intervals.begin(), intervals.end(), [](const vector<int>& a, const vector<int>& b) {
        return a < b;
    });
    
    int count = 1;  // at least one interval can be kept
    int lastEnd = intervals;
    
    for (int i = 1; i < intervals.size(); i++) {
        if (intervals[i] >= lastEnd) {
            // No overlap
            count++;
            lastEnd = intervals[i];
        }
    }
    
    return intervals.size() - count;
}
```

- **Time:** O(n log n)  
- **Space:** O(1)

---

### ✅ 4. Check if Intervals are Non-Overlapping

**Idea:**  
- Sort by start time.  
- Check if any interval starts before the previous one ends.

```cpp
bool canAttendMeetings(vector<vector<int>>& intervals) {
    if (intervals.size() <= 1) return true;
    
    sort(intervals.begin(), intervals.end());
    
    for (int i = 1; i < intervals.size(); i++) {
        if (intervals[i] < intervals[i-1]) {
            return false;
        }
    }
    return true;
}
```

- **Time:** O(n log n)  
- **Space:** O(1)

---

### ✅ 5. Interval List Intersections

**Idea:**  
- Use two pointers to traverse both lists.  
- Intersection exists if `max(start1, start2) <= min(end1, end2)`.

```cpp
vector<vector<int>> intervalIntersection(vector<vector<int>>& firstList, vector<vector<int>>& secondList) {
    vector<vector<int>> result;
    int i = 0, j = 0;
    
    while (i < firstList.size() && j < secondList.size()) {
        int start = max(firstList[i], secondList[j]);
        int end = min(firstList[i], secondList[j]);
        
        if (start <= end) {
            result.push_back({start, end});
        }
        
        if (firstList[i] < secondList[j]) {
            i++;
        } else {
            j++;
        }
    }
    
    return result;
}
```

- **Time:** O(m + n)  
- **Space:** O(1) extra (excluding output)

---

### ⏱️ Complexity Summary

| Problem Type                     | Time       | Space     |
|----------------------------------|------------|-----------|
| Merge Intervals                  | O(n log n) | O(1)      |
| Insert Interval                  | O(n)       | O(1)      |
| Erase Overlapping Intervals      | O(n log n) | O(1)      |
| Check Non-Overlapping            | O(n log n) | O(1)      |
| Interval List Intersections      | O(m + n)   | O(1)      |

---

### 📌 Key Takeaways

- Always **sort intervals** by start (or end) before processing.  
- For **merge**, keep extending the last interval if overlap exists.  
- For **insert**, handle three parts: before, merge, after.  
- For **erase**, sort by end time and greedily keep non-overlapping ones.  
- For **intersection**, use two pointers and compute `max(start)` and `min(end)`.
