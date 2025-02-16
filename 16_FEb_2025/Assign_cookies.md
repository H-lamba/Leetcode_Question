# Assign Cookies - LeetCode Solution

## Problem Description
The problem "Assign Cookies" is a classic greedy algorithm problem from [LeetCode](https://leetcode.com/problems/assign-cookies/description/). The task is to assign cookies to children such that the number of children who receive cookies is maximized. Each child has a greed factor, and each cookie has a size. A child can only be satisfied if their greed factor is less than or equal to the size of the cookie they receive. The goal is to maximize the number of children that are satisfied.

## Problem Link
- [Assign Cookies - LeetCode](https://leetcode.com/problems/assign-cookies/description/)

## Approach

### Greedy Algorithm
The greedy approach aims to always choose the best option at each step with the hope that these local optimum choices lead to the global optimum solution. In this case, we aim to satisfy as many children as possible.

### Steps:
1. **Sort the greed array**: First, sort the greed factors of the children in increasing order.
2. **Sort the cookie array**: Sort the sizes of the cookies in increasing order as well.
3. **Greedy assignment**: Start by iterating over the cookies. For each cookie, check if it can satisfy the current child's greed (i.e., the cookie size is greater than or equal to the child's greed factor). If it does, assign the cookie to that child and move on to the next child and next cookie.

The goal is to maximize the number of children who can be satisfied.

### Time Complexity:
- Sorting both arrays takes O(n log n) time, where `n` is the number of children (or cookies). 
- The greedy selection process takes O(n), so the overall time complexity is O(n log n).

### Space Complexity:
- The space complexity is O(1) for the greedy approach since we are not using any extra data structures other than the sorted arrays.

## Code Implementation

```c++
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(),g.end());
        sort(s.begin(),s.end());
        int l = 0;
        int r= 0;
        while(l<g.size() && r<s.size())
        {
            if(g[l]<=s[r])
            l++;
            r++;
        }
        return l;
    }
};
```
