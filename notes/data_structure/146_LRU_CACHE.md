# Lru Cache

```Python
class Node:
    def __init__(self, key, val):
        self.key = key
        self.val = val
        self.prev = None
        self.next = None

class LRUCache:
    """
    We use a doubly linked list with a hash map to track all nodes 
    that are in the list and then we can evict the first item in the 
    linked list 

    init -- makes a list with two dummy nodes
    one latest and one oldest 

    get -- if the key is in the cache then we 
    remove the node from the linked list 
    and put it back in the end (latest)
    then we return the node.val from the cache
    else return -1 if the key was not found 

    remove -- generic remove node from list

    insert -- puts at node at the end of the linked
    list to mark this node as the latest used key

    put -- if they key already exists we will 
    delete and override it, by storing a new 
    node in the cache and putting it at the end 
    of the list 

    if the length of the cache is too long then we just delete
    the oldest (first value in the linked list)
    """
    def __init__(self, capacity: int):
        self.cap = capacity
        self.cache = {}

        self.oldest = Node(0, 0)
        self.latest = Node(0, 0) # dummy nodes at beg of list
        self.oldest.next = self.latest
        self.latest.prev = self.oldest
        

    def get(self, key: int) -> int:
        if key in self.cache:
            self.remove(self.cache[key])
            self.insert(self.cache[key]) # put this key at the latest used (end of the list)
            return self.cache[key].val
        return -1

    def remove(self, node):
        # deletes a given node from the list
        prev, next = node.prev, node.next
        prev.next = next
        next.prev = prev

    def insert(self, node):
        # insert a node at the end of the list
        prev, next = self.latest.prev, self.latest
        prev.next = next.prev = node
        node.next, node.prev = next, prev
        

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            self.remove(self.cache[key])
        self.cache[key] = Node(key, value)
        self.insert(self.cache[key])

        if len(self.cache) > self.cap:
            # delete oldest if cap too large
            lru = self.oldest.next
            self.remove(lru)
            del self.cache[lru.key]


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```
Time: O(1) for all operations since we are reading from a hashmap and just doing linked list operations without having to search for nodes<br>
Space: O(cap) depending on how much cap is given at instantiaion<br>

Notes: This combines two structures where we track nodes in O(1) with a hash map and then we can just delete and move nodes around O(1) by using dummy nodes on a doubly linked list
