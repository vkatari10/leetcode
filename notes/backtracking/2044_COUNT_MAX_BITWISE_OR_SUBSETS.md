# Count Nmumber of Maximum Bitwise Or Subsets


```Python
class Solution:
    def countMaxOrSubsets(self, nums):
        max_or = 0
        for n in nums:
            max_or |= n # this will always find the max OR since its monotonic
            # we can keep ORing one and still end up with the max

        
        # based on the problem constraints we can do backtracking
        def dfs(i, curr_or):
            if i == len(nums):
                '''
                So with any backtracking problem we have a condition when 
                the index equals the length of nums to return the final ans
                '''
                return 1 if curr_or == max_or else 0

            '''
            So with any backtracking we just include and exclude this current
            number 

            Since we are including the number we just or the current number
            on the include and then we dont on the exclude

            But both calls will move on to the next index
            '''
            include = dfs(i + 1, curr_or | nums[i])
            exclude = dfs(i + 1, curr_or)
            return include + exclude

        return dfs(0, 0)
```
Time: O(2^N) Since this is backtracking and exploring every possiblility<br>
Space: O(N) if we count the stack frame, but technically O(1) since its all recursive<br>

Notes: This is just classisical backtracking again you can see how similar it is to 78 or 80. The only difference is since we know the max target we can precompute it ahead of time and then on the include call we can just bitwise OR the currnet number with the curr or instead of adding to it like we would in other problems due to the nature of this problem. We are also just returning a scalar in this problem so we can just return a final value at the end of the function.
