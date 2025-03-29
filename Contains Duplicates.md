# Contains Duplicates II

**Statement** :- Given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k.

**Examples :-**
```
Example 1:

Input: nums = [1,2,3,1], k = 3
Output: true
Example 2:

Input: nums = [1,0,1,1], k = 1
Output: true
Example 3:

Input: nums = [1,2,3,1,2,3], k = 2
Output: false
```

**Approach :-** 
The approach uses a nested loop where the outer loop (`i`) iterates through each element, and the inner loop (`j`) starts from `i + 1` to check for duplicates within a distance of `k`. It compares `nums[i]` and `nums[j]`, and if they are equal and `j - i <= k`, it returns `true`. To optimize, it breaks out of the inner loop if the distance exceeds `k`. The overall time complexity is \(O(n^2)\) due to the nested loops.


**Code :-**

```c++
class Solution {
public:
    bool containsNearbyDuplicate(vector<int>& nums, int k) {
        for(int i = 0; i<nums.size(); i++)
        {
            for(int j =i+1 ; j<nums.size();j++ )
            {
                if(nums[i]== nums[j] && abs(i-j)<=k)
                return true;
                if(abs(i-j)>k)
                break;
                else 
                continue;
            }
        }
        return false;
    }
};
```

**Complexity :-**
- *Time Complexity :-* O(n^2)
- *Space Complexity :-* O(1)

Thanks for visiting 😊
Feell free to contact ;
