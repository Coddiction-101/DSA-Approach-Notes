> 🔢 **Pattern: Array – Sorting Algorithms**  
> Bubble, Selection, Insertion, Merge, Quick, Heap, Counting, Radix.

---

### ✅ 1. Bubble Sort

- Repeatedly swap adjacent elements if they are in wrong order.  
- After each pass, largest element “bubbles” to the end.

```cpp
void bubbleSort(vector<int>& nums) {
    int n = nums.size();
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (nums[j] > nums[j + 1]) {
                swap(nums[j], nums[j + 1]);
            }
        }
    }
}
```

- **Time:** O(n²)  
- **Space:** O(1)

---

### ✅ 2. Selection Sort

- Find the minimum element in remaining unsorted array and swap it with the first unsorted element.

```cpp
void selectionSort(vector<int>& nums) {
    int n = nums.size();
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (nums[j] < nums[minIndex]) {
                minIndex = j;
            }
        }
        swap(nums[i], nums[minIndex]);
    }
}
```

- **Time:** O(n²)  
- **Space:** O(1)

---

### ✅ 3. Insertion Sort

- Build sorted array one element at a time.  
- For each element, place it in correct position among already sorted elements.

```cpp
void insertionSort(vector<int>& nums) {
    int n = nums.size();
    for (int i = 1; i < n; i++) {
        int key = nums[i];
        int j = i - 1;
        while (j >= 0 && nums[j] > key) {
            nums[j + 1] = nums[j];
            j--;
        }
        nums[j + 1] = key;
    }
}
```

- **Time:** O(n²)  
- **Space:** O(1)

---

### ✅ 4. Merge Sort

- Divide array into two halves, sort each half, then merge them.  
- Classic divide and conquer.

```cpp
void merge(vector<int>& nums, int left, int mid, int right) {
    vector<int> temp(right - left + 1);
    int i = left, j = mid + 1, k = 0;
    
    while (i <= mid && j <= right) {
        if (nums[i] <= nums[j]) {
            temp[k++] = nums[i++];
        } else {
            temp[k++] = nums[j++];
        }
    }
    
    while (i <= mid) temp[k++] = nums[i++];
    while (j <= right) temp[k++] = nums[j++];
    
    for (int i = 0; i < k; i++) {
        nums[left + i] = temp[i];
    }
}

void mergeSort(vector<int>& nums, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(nums, left, mid);
        mergeSort(nums, mid + 1, right);
        merge(nums, left, mid, right);
    }
}
```

- **Time:** O(n log n)  
- **Space:** O(n)

---

### ✅ 5. Quick Sort

- Choose a pivot, partition array around it, then sort left and right parts.  
- In-place, but worst case O(n²).

```cpp
int partition(vector<int>& nums, int low, int high) {
    int pivot = nums[high];
    int i = low - 1;
    for (int j = low; j < high; j++) {
        if (nums[j] <= pivot) {
            i++;
            swap(nums[i], nums[j]);
        }
    }
    swap(nums[i + 1], nums[high]);
    return i + 1;
}

void quickSort(vector<int>& nums, int low, int high) {
    if (low < high) {
        int pi = partition(nums, low, high);
        quickSort(nums, low, pi - 1);
        quickSort(nums, pi + 1, high);
    }
}
```

- **Time:** O(n log n) average, O(n²) worst  
- **Space:** O(log n) average (recursion stack)

---

### ✅ 6. Heap Sort (using array as heap)

- Build max heap, then repeatedly extract max and place at end.  
- Uses array as a complete binary tree.

- **Time:** O(n log n)  
- **Space:** O(1)

---

### ✅ 7. Counting Sort

- Use when range of numbers is small.  
- Count frequency of each number, then reconstruct array.

- **Time:** O(n + k) where k = range  
- **Space:** O(k)

---

### ✅ 8. Radix Sort

- Sort numbers digit by digit (LSD or MSD).  
- Uses counting sort as subroutine.

- **Time:** O(d * (n + k)) where d = digits, k = base  
- **Space:** O(n + k)

---

### ⏱️ Complexity Summary

| Algorithm       | Time (Avg) | Time (Worst) | Space     |
|-----------------|------------|--------------|-----------|
| Bubble Sort     | O(n²)      | O(n²)        | O(1)      |
| Selection Sort  | O(n²)      | O(n²)        | O(1)      |
| Insertion Sort  | O(n²)      | O(n²)        | O(1)      |
| Merge Sort      | O(n log n) | O(n log n)   | O(n)      |
| Quick Sort      | O(n log n) | O(n²)        | O(log n)  |
| Heap Sort       | O(n log n) | O(n log n)   | O(1)      |
| Counting Sort   | O(n + k)   | O(n + k)     | O(k)      |
| Radix Sort      | O(d(n+k))  | O(d(n+k))    | O(n + k)  |

---

### 📌 Key Takeaways

- For interviews:
  - Know **Merge Sort** and **Quick Sort** well (logic, not just code).  
  - Use **STL sort()** in C++ unless asked to implement a specific sort.  
- For small range: **Counting Sort**.  
- For digits: **Radix Sort**.  
- Always think: is the array already sorted? Can we do better than O(n log n)?
```
