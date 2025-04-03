# Search a 2D Matrix

**Description :-** You are given an m x n integer matrix matrix with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.
- Given an integer target, return true if target is in matrix or false otherwise.

**Example:**
```
1)
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
Output: true
```
![image](https://github.com/user-attachments/assets/faf705f4-a189-490e-8cd3-c1c87c5c7edd)

```
2)
Input: matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
Output: false
```
![image](https://github.com/user-attachments/assets/659fd751-08f9-4160-be3b-a8149e0db9b6)


I have solved this problem statement using 2 appraches,

**Approach 1 Row-wise Binary Search (O(m log n))**
This approach applies binary search on each row individually.

Steps:
- Iterate through each row in the matrix.
- Check if the target can be in the current row:
- If target < matrix[i][0] (smaller than first element) → Skip row
-If target > matrix[i].back() (larger than last element) → Skip row
-Perform binary search on the current row.
-If found, return true; otherwise, continue searching.
-If no match is found after checking all rows, return false.

**Time Complexity:**
Each row takes O(log n) (binary search).
``` cpp
class Solution {
public:

  
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        for(int i = 0; i<matrix.size(); i++)
        {
            int n = matrix[i].size()-1;
            
            {
                if(matrix[i][n]<target || matrix[i][0]>target)
                {
                    continue;
                }
                if (binary_search(matrix[i].begin(), matrix[i].end(), target))
                return true;
            }
        }
        return false;
    }
};
```

### **Approach 2: Binary Search on a Flattened Matrix (O(log(m * n)))**  

Since the matrix is sorted **row-wise**, we can treat it as a **1D sorted array** and perform **binary search** directly.  

---

### **Steps:**
1. **Flatten the Matrix Virtually:**  
   - Consider the 2D matrix as a 1D array of size `m * n`.  
   - Instead of actually flattening it, compute the **row and column indices** dynamically.  

2. **Initialize Binary Search Pointers:**  
   - `left = 0` (first element)  
   - `right = m * n - 1` (last element)  

3. **Perform Binary Search:**  
   - Compute `mid = left + (right - left) / 2`.  
   - Convert `mid` to 2D indices:  
     \[
     \text{row} = \frac{\text{mid}}{\text{cols}}, \quad \text{col} = \text{mid} \% \text{cols}
     \]
   - Compare `matrix[row][col]` with `target`:  
     - If **equal**, return `true`.  
     - If **smaller**, search the **right half** (`left = mid + 1`).  
     - If **larger**, search the **left half** (`right = mid - 1`).  

4. **If target is not found, return `false`**.  

---

### **Time Complexity:**
- **O(log(m * n))** since we perform binary search over `m * n` elements.  

### **Space Complexity:**  
- **O(1)** (No extra space used).  

---

### **Optimized Code:**
```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size();
        int n = matrix[0].size();
        int left = 0, right = m * n - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            int row = mid / n;
            int col = mid % n;
            int midElement = matrix[row][col];

            if (midElement == target) {
                return true;
            } else if (midElement < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return false;
    }
};
```


**Feel Free to tell me more 😊😊**
