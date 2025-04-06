# Largest Divisible Subset

**Problem :-** Given a set of distinct positive integers nums, return the largest subset answer such that every pair (answer[i], answer[j]) of elements in this subset satisfies:
answer[i] % answer[j] == 0, or
answer[j] % answer[i] == 0
If there are multiple solutions, return any of them.

**Examples :**

```
Example 1:

Input: nums = [1,2,3]
Output: [1,2]
Explanation: [1,3] is also accepted.
Example 2:

Input: nums = [1,2,4,8]
Output: [1,2,4,8]

```

**Approach**

Step	Action
1	    Sort the array
2	    Loop through each number as starting point
3	    Try building a divisible subset from that point
4	    Store all such subsets
5	    Print them for debugging
6	    Select the longest one
7	    Return that as the final result

**Code:-**

``` cpp
# include <iostream>
class Solution {
public:
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector <vector<int>> temp;

        for(int k = 0; k<nums.size(); k++)
        {
            vector <int>tempin;
        tempin.push_back(nums[k]);
        //nums.erase(nums.begin()+k);
        for(int i = 0; i<nums.size(); i++)
        {
            if(i==k)
            continue;
            //vector<int> tempin[i];
            int nd = 0;
            for(auto j : tempin)
            {   if(j==0) continue;
                if(nums[i]== 0) continue;
                if (nums[i] % j != 0)
                        nd++;
            }
            if(nd==0)
            tempin.push_back(nums[i]);
        }
        temp.push_back(tempin);
        }
        cout << "All subsets built:\n";
for (auto subset : temp) {
    for (auto num : subset) {
        cout << num << " ";
    }
    cout << endl;
}

        vector <int> result;
        for( auto subset : temp)
        {
            if (subset.size() > result.size()) {
                result = subset;
        }
        }
        return result;
    }
};
```

**Drawbacks of this apprach**
- This doesn't work for the inputs like [5,9,18,54,108,540,90,180,360,720] whose answer should be [9,18,90,180,360,720] but it returns [5,90,180,360,720]
- Not efficient: O(n² * n) time in worst case — for each index, you’re scanning others and looping inside again.
- Doesn't backtrack or explore all subset combinations.

**More Effective apprach is to use dynamic programming**

Have a Nice Day 😊
