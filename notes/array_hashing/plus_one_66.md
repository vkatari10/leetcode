# Plus One 

Given an array of integers, add one to this number

```Python

class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:


        for i in range(len(digits) - 1, -1, -1): # go from end -> back

            if digits[i] + 1 != 10: # if we can just add one to the number and 
            # have no carry then just return it 
                digits[i] += 1
                return digits

            digits[i] =  0 # else make this digit zero 

            if i == 0: # if we get to the first item in the list then we just add 1 + 
            # the remaining values in the list 
                '''
                Think about [9, 9] we can just add one to both indicies, and then once
                we reach the end we end up with [1] + [0, 0]. This is why this solution 
                works as is...
                '''
                return [1] + digits
```
Time: O(N) Since we need to traverse the entire array<br>
Space: O(1)<br>

Notes: This is not like leetcode 2, since we just need to add one to the number and we are not adding two numbers together
