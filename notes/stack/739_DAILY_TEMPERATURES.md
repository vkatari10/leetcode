# Daily Temperatures

Given an array of temperatures find the next day in the list (as a number of how many days) until there is another day that has a higher temperature

```Python
    class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        
        stack = [] # stores indicies 
        ans = [0] * len(temperatures) # set all answers to be 0 at the beg since 
        # all days are unresolved


        for i in range(len(temperatures)):
            while stack and temperatures[i] > temperatures[stack[-1]]:
                '''
                Pretty much if the stack has something and then we know that 
                temperature at this index is larger than the last temperature
                in the stack then we enter this loop

                This is because we know at this point that the index at this point
                is larger so we can pop those off the stack and then put that index
                of the answer array as the distance we are at now against the index
                of the array 
                '''
                index = stack.pop()
                ans[index] = i - index
            stack.append(i) # append the index onto the main stack since we dont
            # know when the next warmest day is for this day 

        return ans
```
Time: O(N) Since we need to check every day<br>
Space: O(N) Since we need to possibly store every index on the stack<br>

Notes: This stack pattern can be used in a lot of similar problems that deal with the next greatest element (which this problem pretty much is)
