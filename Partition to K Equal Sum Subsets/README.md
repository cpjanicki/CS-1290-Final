# Partition to K Equal Sum Subsets

## Problem
Given an array of integers nums and a positive integer k ,find whether it's possible to divide this array into k non-empty subsets whose sums are all equal.

NOTE:
1 <= k <= nums.length <= 16
0 < nums[i] < 10000

## Example 
```bash 
INPUT: nums = [4,3,2,3,5,2,1],   k = 4
OUTPUT: True

Why is it true?
Because you can divide it into 4 subsets
[5]
[1,4]
[2,3]
[3,2]

THEY ALL ADD UP TO  5!!!!!!!
````

## Solution 
The best wasy to solve this problem is with DFS (Disjoint Forest Set)
We try to place each element to one of the bucket. 
Note the improvement in the for loop.


We investigate methods of exhaustive search and find target = sum(nums) / k in the same way

Our goal is to use nums in some order so that placing them into groups in that order will be valid. search(used, ...) and this depends on todo, the sum of the remaining unused elements, not crossing multiples of target within one number

The maximum value that can be chosen so as to not cross a multiple of target, is targ = (todo - 1) % target + 1. This is essentially todo % target, plus target if that would be zero.

Now for each unused number that doesn't cross, we'll search on that state, and we'll return true if any of those searches are true.

Notice that the state todo depends only on the state used, so when memoizing our search, we only need to make lookups by used.

THE SOLUTION THAT I POSTED IS A TOP-DOWN DP SOLUTION
@leetcode




````java
enum Result { TRUE, FALSE }

class Solution {
    boolean search(int used, int todo, Result[] memo, int[] nums, int target) {
        if (memo[used] == null) {
            memo[used] = Result.FALSE;
            int targ = (todo - 1) % target + 1;
            for (int i = 0; i < nums.length; i++) {
                if ((((used >> i) & 1) == 0) && nums[i] <= targ) {
                    if (search(used | (1<<i), todo - nums[i], memo, nums, target)) {
                        memo[used] = Result.TRUE;
                        break;
                    }
                }
            }
        }
        return memo[used] == Result.TRUE;
    }
    public boolean canPartitionKSubsets(int[] nums, int k) {
        int sum = Arrays.stream(nums).sum();
        if (sum % k > 0) return false;

        Result[] memo = new Result[1 << nums.length];
        memo[(1 << nums.length) - 1] = Result.TRUE;
        return search(0, sum, memo, nums, sum / k);
    }
}

````








