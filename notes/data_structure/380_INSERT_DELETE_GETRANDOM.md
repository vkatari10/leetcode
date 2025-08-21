# Insert Delete GetRandom O(1)

```Python
import random
from collections import defaultdict

class RandomizedSet:

    def __init__(self):
        self.vals_idx = {}
        self.vals = []

    def insert(self, val: int) -> bool: 
        if val in self.vals_idx:
            return False

        self.vals_idx[val] = len(self.vals)
        self.vals.append(val)
        return True

    def remove(self, val: int) -> bool:
        if val not in self.vals_idx:
            retun False


        """
        Genius part we just delete O(1) from hash map and
        then move the wanting to delete index to the last 
        index in the list and just pop off so its O(1)
        """

        index = self.vals_idx[val]
        self.vals_idx[self.vals[-1]] = index # move the last added value to the index of the thing we are deleting

        del self.vals_idx[val] # remove the original val from the hash

        self.vals[index] = self.vals[-1] # move last to the deleting index now
        self.values.pop() # "delete" the last item (dupe of the thing we just moved)
        # we erased the deletion value implcitly by overwriting its value in the array         

        return True
        

    def getRandom(self) -> int:
        return self.vals[random.randint(0, len(self.vals) - 1)]

        
        


# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```
Time: O(1) per operation since its just hash maps and appending<br>
Space: O(N) since we need an array and hash map to store all values<br>

Notes: This is kinda easy to implement but like you need to know which data structures to use, i.e. not a set to implement it properly
