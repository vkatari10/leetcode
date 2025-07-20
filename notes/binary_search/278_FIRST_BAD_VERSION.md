# First Bad Version 


```Python
# The isBadVersion API is already defined for you.
# def isBadVersion(version: int) -> bool:

class Solution:
    def firstBadVersion(self, n: int) -> int:
        '''
        There is no reason to make an array since we can just imply it 
        using using the given input from 1 to n 
        '''
        left, right = 1, n
        ans = n

        while left <= right: # classic binary search condition 

            '''
            We can just calc the mid point value here 
            '''
            mid = (left + right) // 2

            if isBadVersion(mid): # we can check this mid version now 
                right = mid - 1 # if this version is good we can move right down to mid
                # this is because we now every version past right is also bad 
                ans = mid
            else: # else we can just move left up since we know every previous version is good
                left = mid + 1

        return ans
```
Time: O(logN) Since we are performing binary search here<br>
Space: O(1) Since we are not creating anything here except `left` and `right`<br>

Notes: We don't make an array here since we know the first and ending bounds because the problem gives us those contraints meaning we can keep this O(1) space.
