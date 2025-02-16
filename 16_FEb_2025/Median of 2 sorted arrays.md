# Median of Two Sorted Arrays - LeetCode Solution

## Problem Description
The problem "Median of Two Sorted Arrays" asks to find the median of two sorted arrays, `nums1` and `nums2`, of sizes `m` and `n` respectively. The median is the middle element of a sorted array. If the array has an even number of elements, the median is the average of the two middle elements.

You need to return the median of the two sorted arrays. This solution uses a simple approach where both arrays are combined, sorted, and the median is found.

## Problem Link
- [Median of Two Sorted Arrays - LeetCode](https://leetcode.com/problems/median-of-two-sorted-arrays/)

## Approach

### Steps:

1. **Merge the Arrays**: 
   - Combine the two sorted arrays into one. This is done by inserting all elements from `nums2` into `nums1`.
   - The combined array is now unsorted and will need to be sorted.

2. **Sort the Combined Array**: 
   - Sort the merged array in ascending order to ensure that the elements are arranged from smallest to largest. This sorting step is necessary to find the correct median.

3. **Calculate the Median**:
   - After sorting, calculate the median based on the length of the combined array:
     - If the number of elements (`n`) is odd, the median is the element at index `n/2`.
     - If the number of elements is even, the median is the average of the elements at indices `(n-1)/2` and `n/2`.

4. **Return the Median**:
   - Return the computed median.

### Time Complexity:
- Sorting the combined array takes O((m + n) log(m + n)) time, where `m` and `n` are the lengths of `nums1` and `nums2`. 
- The overall time complexity is dominated by the sorting step.

### Space Complexity:
- The space complexity is O(m + n) because we are storing the combined array.

## Code Implementation

```cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        nums1.insert(nums1.end(), nums2.begin(), nums2.end());
        sort(nums1.begin(), nums1.end());
        int n = nums1.size();
        if(n%2==1)
        {
            int mid = n/2;
            double ans = nums1[mid];
            return ans;
        }
        else
        {
            int mid = (n-1)/2;
            //cout<<mid;
            //cout<<nums1[mid+1]+ nums1[mid];
            double ans = (nums1[mid] + nums1[mid+1])/2.0;
            return ans;
        }
        return 0;
    }
};
```
