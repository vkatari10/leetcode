# Jump Game 

```Python
class Solution:
    def canJump(self, nums: List[int]) -> bool:

        """
        This solution will start at the end and look 
        at if the current position + index will be >=
        to the goal value which is just the last index
        in the array 

        pretty much if we are at index i and we can jump
        to the index of the goal then we can set goal 
        to this new i and keep moving down the array 
        and if goal gets to 0 then we must know that
        there is a valid path to the goal
        """
        
        goal = len(nums) - 1

        for i in range(len(nums) - 2, -1, -1):
            if i + nums[i] >= goal:
                goal = i

        return True if goal == 0 else False
```
Time: O(N)<br>
Space: O(1)<br>

Notes: This is faster than trying to do DP, which is also valid, but pretty much this is a clever greedy trick where we check if the index and the value at said index is larger than the index of the goal at this current point
