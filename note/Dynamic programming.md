## Dynamic programming

1. [673. Number of Longest Increasing Subsequence](https://leetcode.com/problems/number-of-longest-increasing-subsequence/)

2. [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

   Note that `k` could be negative, which needs offset for **memoize**. 

   This can also be solved by using **Prefix Sum** along with **HashMap**

   ```java
   class Solution {
       public int subarraySum(int[] nums, int k) {
           int ans = 0;
           for(int i = 0; i < nums.length; i++){
               ans += dp(nums, k, i);
           }
           return ans;
       }
       // number of CS that end at index
       public int dp(int[] nums, int k, int index){
           if(index == 0) return nums[index] == k ? 1 : 0;
           int res = 0;
           if(nums[index]==k) res +=1;
           return res + dp(nums, k - nums[index], index - 1);
       }
   }
   ```

   

3. [72. Edit Distance -- Hard](https://leetcode.com/problems/edit-distance/)

4. [10. Regular Expression Matching -- Hard](https://leetcode.com/problems/regular-expression-matching/) use DP for string match

### Do not know where to start or where to stop

1. [410. Split Array Largest Sum -- Hard](https://leetcode.com/problems/split-array-largest-sum/)
2. [1335. Minimum Difficulty of a Job Schedule -- Hard](https://leetcode.com/problems/minimum-difficulty-of-a-job-schedule/)

job scheduling series



[1000. Minimum Cost to Merge Stones -- Hard](https://leetcode.com/problems/minimum-cost-to-merge-stones/) 

```java
class Solution {
    int k;
    int[] preSum;
    Integer[][][]memo;
    public int mergeStones(int[] stones, int k) {
        // the last step merge cost will always be sum(stones)
        // so problem becomes merge stones into k piles, then merge into one piles
        // we can divide the problem "merge into k piles" into two sub problems
        // merge one side in to k - 1 piles, while another side into 1 pile
        
        // also we can see stones  as (k - 1), (k - 1), ... (k - 1), 1
        // so  x*(k - 1) + 1 = len, there will be a solution only when (len - 1) % (k - 1) = 0
        
        this.k = k;
        int m = stones.length;
        preSum = new int[stones.length];
        preSum[0] = stones[0];
        memo = new Integer[m][m][k + 1];
        for(int i = 1; i < stones.length; i++){
            preSum[i] = stones[i] + preSum[i - 1];
        }
        int ans = dp(stones, 0, stones.length - 1, 1);
        return ans == Integer.MAX_VALUE ? -1 : ans;
    }
    // return min cost to form target number of piles by using from ith to jth stone
    private int dp(int[] stones, int i, int j, int target){
        // base case
        if(j - i + 1 < target) return Integer.MAX_VALUE;
        if(i == j) return target == 1 ? 0 : Integer.MAX_VALUE;
        if(memo[i][j][target] != null) return memo[i][j][target];
        int minCost = Integer.MAX_VALUE;
        if(target == 1){
            int temp = dp(stones, i, j, k);
            if(temp != Integer.MAX_VALUE){// can be merged into k piles
                minCost = temp + preSum[j] - (i - 1 >= 0 ? preSum[i - 1] : 0 );
            }else{
                minCost = Integer.MAX_VALUE;
            }
            return memo[i][j][target] = minCost;
        }
        // we need to partition the array to two part, one part form target - 1 piles
        // another form 1 piles, m here is the end of the left part
        for(int m = i; m < j; m++){
            int left = dp(stones, i, m, target - 1);
            int right = dp(stones, m + 1, j, 1);
            if(left != Integer.MAX_VALUE && right != Integer.MAX_VALUE){
                minCost = Math.min(left + right, minCost);
            }
        }
        return memo[i][j][target] = minCost;
    }
```

[1937. Maximum Number of Points with Cost -- Medium ](https://leetcode.com/problems/maximum-number-of-points-with-cost/)

![image-20210719162200792](images/image-20210719162200792.png)

