## Ship Packages Within Days

## Problem Statement

A conveyor belt has packages that must be shipped from one port to another within days days.

The i-th package on the conveyor belt has a weight of weights[i]. Each day, we load the ship with packages on the conveyor belt (in the order given by weights). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within days days.

## Example 1:

### Input:

weights = [1,2,3,4,5,6,7,8,9,10], days = 5

Output:

15

### Explanation:
A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:

1st day: 1, 2, 3, 4, 5

2nd day: 6, 7

3rd day: 8

4th day: 9

5th day: 10

Example 2:

Input:

weights = [3,2,2,4,1,4], days = 3

Output:

6


## Constraints:

1 <= days <= weights.length <= 5 * 10^4

1 <= weights[i] <= 500

## Solution Approach

This problem can be solved using Binary Search on the minimum ship capacity:

The lower bound of ship capacity is the maximum weight in weights (since the ship must at least carry the heaviest package).

The upper bound is the sum of all weights (if the ship carries everything in one day).

We perform a binary search between these bounds and check if the mid-value is a feasible ship capacity by simulating the loading process.

If the mid-value works, we try a smaller value to find the minimum capacity. Otherwise, we increase the capacity.

Implementation
''' c++
class Solution {
public:
    int lows(vector<int> & weights)
    {
        int anss = 0;
        for(int i = 0; i<weights.size(); i++)
        {
            if (anss<= weights[i])
            anss = weights[i];
        }
        return anss;
    }
    int requireddays(vector<int> v, int capacity)
    {
        int day =1;
        int load = 0;
        for(int i: v)
        {
            if(load+i>capacity)
            {
                load = i;
                day++;
            }
            else
            {
                load = load +i;
            }
        }
        return day;
    }
    int sumof(vector<int>& arr)
    {
        int total = 0;
        for(int i =0; i<arr.size();i++)
        {
            total+= arr[i];
        }
        return total;
    }
    int shipWithinDays(vector<int>& weights, int days) {
        int low = lows(weights);
        int high = sumof(weights);
        while(low<= high)
        {
            int mid = low + (high-low)/2;
            int daysreq = requireddays(weights, mid);
            if(daysreq <= days)
            {
                high = mid-1;
            }
            else 
            {
                low = mid+1;
            }
        }
        return low;
    }
};
'''

# Example usage
weights = [1,2,3,4,5,6,7,8,9,10]
days = 5
print(shipWithinDays(weights, days))  # Output: 15

## Complexity Analysis

Binary Search runs in O(log(sum(weights) - max(weights)))

Feasibility Check runs in O(N), where N is the length of weights

Overall Complexity: O(N log(sum(weights) - max(weights)))
