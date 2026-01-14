> 🔢 **Pattern: Array – Matrix / 2D Array**  
> Traversal (row-major, column-major), boundary, diagonal, spiral, and common problems.

---

### ✅ 1. Basic Traversal

#### Row-major (row by row)

```cpp
void printRowMajor(vector<vector<int>>& matrix) {
    int m = matrix.size();
    int n = matrix.size();
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            cout << matrix[i][j] << " ";
        }
        cout << endl;
    }
}
```

#### Column-major (column by column)

```cpp
void printColumnMajor(vector<vector<int>>& matrix) {
    int m = matrix.size();
    int n = matrix.size();
    for (int j = 0; j < n; j++) {
        for (int i = 0; i < m; i++) {
            cout << matrix[i][j] << " ";
        }
        cout << endl;
    }
}
```

- **Time:** O(m × n)  
- **Space:** O(1)

---

### ✅ 2. Boundary Traversal

Print all elements on the boundary of the matrix.

```cpp
void printBoundary(vector<vector<int>>& matrix) {
    int m = matrix.size();
    int n = matrix.size();
    
    // Top row
    for (int j = 0; j < n; j++) {
        cout << matrix[j] << " ";
    }
    
    // Right column (excluding corners)
    for (int i = 1; i < m - 1; i++) {
        cout << matrix[i][n - 1] << " ";
    }
    
    // Bottom row (if more than one row)
    if (m > 1) {
        for (int j = n - 1; j >= 0; j--) {
            cout << matrix[m - 1][j] << " ";
        }
    }
    
    // Left column (excluding corners)
    if (n > 1) {
        for (int i = m - 2; i >= 1; i--) {
            cout << matrix[i] << " ";
        }
    }
}
```

- **Time:** O(m + n)  
- **Space:** O(1)

---

### ✅ 3. Diagonal Traversal

#### Main Diagonal (top-left to bottom-right)

```cpp
void printMainDiagonal(vector<vector<int>>& matrix) {
    int n = min(matrix.size(), matrix.size());
    for (int i = 0; i < n; i++) {
        cout << matrix[i][i] << " ";
    }
}
```

#### Anti-diagonal (top-right to bottom-left)

```cpp
void printAntiDiagonal(vector<vector<int>>& matrix) {
    int m = matrix.size();
    int n = matrix.size();
    for (int i = 0; i < min(m, n); i++) {
        cout << matrix[i][n - 1 - i] << " ";
    }
}
```

- **Time:** O(min(m, n))  
- **Space:** O(1)

---

### ✅ 4. Spiral Traversal

Print elements in spiral order: top → right → bottom → left → repeat.

```cpp
vector<int> spiralOrder(vector<vector<int>>& matrix) {
    vector<int> result;
    if (matrix.empty() || matrix.empty()) return result;
    
    int top = 0, bottom = matrix.size() - 1;
    int left = 0, right = matrix.size() - 1;
    
    while (top <= bottom && left <= right) {
        // Top row
        for (int j = left; j <= right; j++) {
            result.push_back(matrix[top][j]);
        }
        top++;
        
        // Right column
        for (int i = top; i <= bottom; i++) {
            result.push_back(matrix[i][right]);
        }
        right--;
        
        // Bottom row
        if (top <= bottom) {
            for (int j = right; j >= left; j--) {
                result.push_back(matrix[bottom][j]);
            }
            bottom--;
        }
        
        // Left column
        if (left <= right) {
            for (int i = bottom; i >= top; i--) {
                result.push_back(matrix[i][left]);
            }
            left++;
        }
    }
    
    return result;
}
```

- **Time:** O(m × n)  
- **Space:** O(1) extra (excluding output)

---

### ✅ 5. Rotate Matrix 90° Clockwise

**Idea:**  
- Transpose the matrix (swap `matrix[i][j]` with `matrix[j][i]`).  
- Reverse each row.

```cpp
void rotate(vector<vector<int>>& matrix) {
    int n = matrix.size();
    
    // Transpose
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            swap(matrix[i][j], matrix[j][i]);
        }
    }
    
    // Reverse each row
    for (int i = 0; i < n; i++) {
        reverse(matrix[i].begin(), matrix[i].end());
    }
}
```

- **Time:** O(n²)  
- **Space:** O(1)

---

### ✅ 6. Set Matrix Zeros

**Idea:**  
- Use first row and first column as markers to indicate which rows/cols should be zeroed.  
- Use two flags to remember if first row/col originally had zero.

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    int m = matrix.size(), n = matrix.size();
    bool firstRowZero = false, firstColZero = false;
    
    // Check if first row has zero
    for (int j = 0; j < n; j++) {
        if (matrix[j] == 0) {
            firstRowZero = true;
            break;
        }
    }
    
    // Check if first col has zero
    for (int i = 0; i < m; i++) {
        if (matrix[i] == 0) {
            firstColZero = true;
            break;
        }
    }
    
    // Mark zeros in first row/col
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            if (matrix[i][j] == 0) {
                matrix[i] = 0;
                matrix[j] = 0;
            }
        }
    }
    
    // Set zeros in rows (except first)
    for (int i = 1; i < m; i++) {
        if (matrix[i] == 0) {
            for (int j = 1; j < n; j++) {
                matrix[i][j] = 0;
            }
        }
    }
    
    // Set zeros in cols (except first)
    for (int j = 1; j < n; j++) {
        if (matrix[j] == 0) {
            for (int i = 1; i < m; i++) {
                matrix[i][j] = 0;
            }
        }
    }
    
    // Set first row
    if (firstRowZero) {
        for (int j = 0; j < n; j++) {
            matrix[j] = 0;
        }
    }
    
    // Set first col
    if (firstColZero) {
        for (int i = 0; i < m; i++) {
            matrix[i] = 0;
        }
    }
}
```

- **Time:** O(m × n)  
- **Space:** O(1)

---

### ⏱️ Complexity Summary

| Problem Type                     | Time       | Space     |
|----------------------------------|------------|-----------|
| Row/Column Traversal             | O(m × n)   | O(1)      |
| Boundary Traversal               | O(m + n)   | O(1)      |
| Diagonal Traversal               | O(min(m,n))| O(1)      |
| Spiral Traversal                 | O(m × n)   | O(1)      |
| Rotate Matrix 90°                | O(n²)      | O(1)      |
| Set Matrix Zeros                 | O(m × n)   | O(1)      |

---

### 📌 Key Takeaways

- For **spiral**, use four boundaries: `top`, `bottom`, `left`, `right`.  
- For **rotate 90°**, transpose + reverse each row.  
- For **set matrix zeros**, use first row/col as markers to avoid extra space.  
- Always handle edge cases: empty matrix, single row, single column.  
- Think in terms of **boundaries** and **layers** for 2D problems.
