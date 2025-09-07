# House Robber 


```Python
class Solution:
    def rob(self, nums: List[int]) -> int:
        n = len(nums)

        if n == 1:
            return nums[0]

        dp = [0] * n # dp table

        dp[0] = nums[0] 

        """
        We want to do this because of how the dp 
        table is going to be set up

        We want to contain either nums[0] (take the first house)
        or nums[1] take the second house, but if we take the second house
        then we cannot rob the first one so we must make a binary choice here

        This is also because the loop starts from 2 so this is the first index
        that the loop will see to decide if we take the third or second house
        """
        dp[1] = max(nums[0], nums[1]) 

        for i in range(2, n): # since we init the first 2 indicies
            """
            Here we make the choice to mark dp[i] as either the max

            of the last value in the dp table or the value of this index
            in nums and the value in the index - 2

            Whichever is bigger is the max profit. 
            """
            dp[i] = max(dp[i - 1], nums[i] + dp[i - 2])


        # this will be guaranteed to have the highest value
        # since its a accumulation of all previous values in the table
        return dp[-1]

```
Time: O(N) since we iterate over the array once<br>
Space: O(N) for DP array, although this problem could use O(1) when optimized<br>

Notes: This is a classic dp problem where we are faced with two choices at every index to build up the entire dp array
