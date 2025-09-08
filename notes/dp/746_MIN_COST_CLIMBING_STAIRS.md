# Min Cost Climbing Stairs

```Python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        n = len(cost)
        dp = [0] * (n)

        # since we can start at 0 or 1 we take the best choice at dp[0]
        dp[0] = min(cost[0], cost[1])

        for i in range(1, n):
            """
            Now we need to add the cost at this point to dp[i]
            which is just cost[i] and now we can add onto the min 
            of what was the cost at dp[i-1] and [i-2] since those 
            are the choices we could have taken at each step 
            """
            dp[i] = cost[i] + min(dp[i - 1], dp[i - 2])
        
        # now we return the min of -1, -2 since we could jump up 2
        # from -2 to reach the end as the problem states
        return min(dp[-1], dp[-2])
```
Time: O(N) Since we need to iterate over the entire array once<br>
Space: O(N) Since we have an array the size of n, note this can also be solved with an O(1) space solution<br>

Notes: This is a 1d DP problem where we have a choice at every step we can either take the last or -2 cost from each point in the array which aligns with the problem statement
