# Find Pairs with a certain sum

Make a data structure that can efficiently find pairs when given a total and the ability to update any number with a certain value, where the input is arrays of integers.

```Python

from collections import Counter

class FindSumPairs:

    def __init__(self, nums1: List[int], nums2: List[int]):
        '''
        Need to track both input arrays from the start

        We will also precompute the hashmap for the second
        array as well upfront so we dont need to create it later
        '''
        self.n2 = nums2
        self.n1 = nums1
        self.freq = Counter(nums2)
        

    def add(self, index: int, val: int) -> None:
        '''
        So all we do is increment nums2[index] += val

        However since nums2 is being tracked with the freq
        map at the beginning of the array we need to account
        for changes of each number since we store as index:number

        Reduce that old numbesr count by one to show that it 
        may not exist in the list anymore and needs to be 
        accounted for
        
        '''
        old = self.n2[index]
        self.freq[old] -= 1
        self.n2[index] += val
        self.freq[self.n2[index]] += 1
        
    def count(self, tot: int) -> int:
        # just counter where the number from n1 
        # minus the wanted total == the number 
        '''
        from n1 and return the number of times that this 
        happens
        '''
        count = 0
        for num in self.n1:
            count += self.freq[tot - num]
        return count



# Your FindSumPairs object will be instantiated and called as such:
# obj = FindSumPairs(nums1, nums2)
# obj.add(index,val)
# param_2 = obj.count(tot)
```
Time O(n^2): Beacuse of the hashmap that we need to maintain<br>
Space: O(N): Storing all the arrays from the beg + hashmap<br>

Notes: You could make a more simple version of it but fails on test cases, but this is the most efficnent (kind of) that gets you under TLE.
