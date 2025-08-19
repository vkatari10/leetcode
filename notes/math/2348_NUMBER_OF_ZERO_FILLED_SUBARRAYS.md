# Number of Zero Filled Subarrays



```Python
class Solution:
    def zeroFilledSubarray(self, nums: List[int]) -> int:
        res = 0
        streak = 0

        """
        Instead of building the solution top down we can instead just 
        build the sum up

        Essentially everytime we see a zero we can update the streak we have
        which counts the number of consec zeros in the array and then add
        those streaks onto the array so we can mimic the 1 + 2 + 3 structure. 

        If we dont see a zero reset the streak back to zero and then return res
        """
        for num in nums:
            if num == 0:
                streak += 1
                res += streak
            else:
                streak = 0

        return res
```
Time: O(N)<br>
Space: O(1)<br>

Notes: This is how we track consecutive numbers in an array
