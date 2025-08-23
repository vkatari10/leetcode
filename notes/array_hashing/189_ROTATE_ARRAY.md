# Rotate array 

```Python
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """

        """
        We will find the pivot index by doing k % n this tells us where
        we need to start rotating the array 
        """
        n = len(nums)
        k %= n

        def reverse(start, end):
            """
            This is just doing an in place swap nothing complicated
            """
            while start < end:
                nums[start], nums[end] = nums[end], nums[start]
                start += 1
                end -= 1

        """
        Example: nums = [1,2,3,4,5,6,7], k = 3

        k %= len(nums) == 3

        1. reverse the entire array 

        [7, 6, 5, 4, 3, 2, 1]

        2. reverse up to k - 1

        [5, 6, 7, 4, 3, 2, 1]

        2. reverse from k to the end 

        [5, 6, 7, 1, 2, 3, 4]
        """
        reverse(0, n - 1)
        reverse(0, k - 1)
        reverse(k, n - 1)
```
Time: O(N)<br>
Space: O(1)<br>

Notes: Instead of using extra memory we can use this trick that rotates it by reversing the entire hting at once and then going back afterwards and then reversing onto itself again.
