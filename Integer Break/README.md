# Integer Break

## Problem
Given a positive integer n, break it into the sum of AT LEAST two positive integers and maximize the product of those integers. Return the maximum product you can get.

In other words, break the sum with at least TWO integers that add up to the sum but you want to get the highest integers as possible in order to get a high total by multiplying them together. 

## Example 
```bash 
INPUT: 2
OUTPUT: 1

EXPLANATION: 
the max sum of 2 is 1 + 1, THEREFORE 1 x 1 = 1 so the output is 1 
```

## Example 2 
````
INPUT: 10
OUTPUT: 36

EXPLANATION:
since 10 can add up to 3+3+4 = 10 THEREFORE 3x3x4 = 36
````
NOTE: You may assume that n is not less than 2 and not larger than 58


## Solution 
If dp[i] is the max production value for breaking the number i, therefore dp[1+j] can also be 
multiplied (i.e. i * j)

  j+i corresponds to the optimal solution for maxi], we have two cases:
                (1) i is the sum of two numbers, i.e. dp[i+j] =i-j is one number, and so max[i]=j*(i-j)
                (2) i is the sum of at least three numbers, i.e. dp[i+j]=i-j is a sum of at least 2 numbers,
   and so the product of the numbers in this sum for S is maxArr[i-j]
                (=maximum product after breaking up i-j into a sum of at least two integers):
                max[i] = j*max[i-j]

````java
public int integerBreak(int n) {
    int[] dp = new int[n+1];
 
    for(int i=1; i<n; i++){
        for(int j=1; j<i+1; j++){
            if(i+j<=n){
                dp[i+j]=Math.max(Math.max(dp[i],i)*Math.max(dp[j],j), dp[i+j]);
            }
        }
    }
 
    return dp[n];
}
````





