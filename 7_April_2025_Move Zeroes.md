# Move Zeros
**Statement :** Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

```
 

Example 1:

Input: nums = [0,1,0,3,12]
Output: [1,3,12,0,0]

Example 2:

Input: nums = [0]
Output: [0]

```

## Approach Steps:

- Create a counter count to keep track of the number of zeroes.
- Create a temporary vector ans to store the result.
- Traverse the Input Array (nums)
- Loop through each element of nums.
- If the element is non-zero, add it to ans.
- If the element is zero, increment the count variable.
- Add Zeroes at the End
- After the loop, ans contains all non-zero elements.
- Append count number of zeroes to ans.
- Update the Original Vector (nums)
- Copy the contents of ans back to nums.

## Code :- 

``` cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int count = 0;
        vector<int> ans ;
        for( int i = 0; i<nums.size(); i++)
        {
            if(nums[i]==0)
            {
                count++;
            }
            else
            ans.push_back(nums[i]);
        }
        for(int i = 0; i<count; i++)
        {
            ans.push_back(0);
        }
        nums = ans;
    }
};
```

Thanks 😊
