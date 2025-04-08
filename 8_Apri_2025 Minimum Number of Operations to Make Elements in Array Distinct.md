# Minimum Number of Operations to Make Elements Array Distinct

**Statement** You are given an integer array nums. You need to ensure that the elements in the array are distinct. To achieve this, you can perform the following operation any number of times:
- Remove 3 elements from the beginning of the array. 
- If the array has fewer than 3 elements, remove all remaining elements.
Note that an empty array is considered to have distinct elements. Return the minimum number of operations needed to make the elements in the array distinct

**Examples**
```
Input: nums = [1,2,3,4,2,3,3,5,7]

Output: 2

Explanation:

In the first operation, the first 3 elements are removed, resulting in the array [4, 2, 3, 3, 5, 7].
In the second operation, the next 3 elements are removed, resulting in the array [3, 5, 7], which has distinct elements.
Therefore, the answer is 2.

Example 2:

Input: nums = [4,5,6,4,4]

Output: 2

Explanation:

In the first operation, the first 3 elements are removed, resulting in the array [4, 4].
In the second operation, all remaining elements are removed, resulting in an empty array.
Therefore, the answer is 2.

Example 3:

Input: nums = [6,7,8,9]

Output: 0

Explanation:

The array already contains distinct elements. Therefore, the answer is 0.
```

## Apporach 

| **Step** | **Action** | **Details** |
|----------|------------|-------------|
| 1 | **Input** | A vector `nums` of integers is given. |
| 2 | **Initialize** | Set `operations = 0`. This variable keeps track of how many times we remove elements. |
| 3 | **Check for uniqueness** | Use the `checkUnique` function to see if all elements in `nums` are unique. |
| 4 | **Inside `checkUnique` function** | Loop through all pairs `(i, j)` where `i ≠ j`. If `nums[i] == nums[j]`, return `false`. Else, return `true`. |
| 5 | **If `nums` is unique** | Return the current value of `operations` as the answer. |
| 6 | **If not unique** | Remove the first 3 elements from `nums` using `erase()` function. |
| 7 | **Increment `operations`** | Increase the `operations` counter by 1. |
| 8 | **Repeat steps 3–7** | Loop again until `nums` becomes empty or all elements are unique. |
| 9 | **If `nums` becomes empty** | Exit the loop and return `operations`. |


## Code

```cpp
class Solution {
public:
bool checkunique(vector <int>& arr)
{
    int n = arr.size();
    for ( int i =0; i<n; i++)
    {
        for (int j = 0; j<n;j++)
        {
            if(i==j)
            continue;
            if(arr[i]== arr[j])
            return false;
        }
    }
    return true;
}
    int minimumOperations(vector<int>& nums) {
        int operations = 0;
        while(nums.size()>0)
        {
            if(checkunique(nums))
            {
                return operations;
            }
            else
            {
                int remove = min(3, (int)nums.size());
                nums.erase(nums.begin(), nums.begin()+ remove)   ; 
                operations++;
            }
        }
        return operations;
    }
};

```

THANKS FOR VISITING 😊😊😊
