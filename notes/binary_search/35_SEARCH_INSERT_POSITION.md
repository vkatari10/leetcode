# Search Insert Position 


```Python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        '''
        There are two cases
        1. target is present 
        2. target is NOT present

        1. Simple case we just return the index of where the num is

        2. Case where the number is not present

        In this case we just need to return left 
        because once left crosses above right then we end up in a place
        where left provides the insert index of the target number 

        Example: 

        Given nums = [1, 3, 5, 6]; target = 2

        [1, 3, 5, 6]
        L  M      R

        since mid is greater than target bring right = mid - 1, now mid is 0 as well

        [1, 3, 5, 6]
        L
        M 
        R

        Now mid is less than target so we bring up left 

        [1, 3, 5, 6]
        M   L
        R

        Now this causes the loop to end, but we return left here because

        target == 2
        where would 2 go? At index 1 
        this is the index of where left is pointing

        this also works for highest value nums because left becomes + 1 and the end anyways
        and the loop exists preventing bound errors

        '''

        left = 0
        right = len(nums) - 1
        mid = 0

        while left <= right:

            mid = (left + right) // 2

            if nums[mid] > target:
                right = mid - 1
            elif nums[mid] < target:
                left = mid + 1
            else:
                return mid

        return left
```
Time: O(logN) since we are using binary search<br>
Space: O(1) Since we are just using two pointers<br>

Notes: The reason why is explained above but pretty much we just return left after its been modified to be + 1 and the loops exits
