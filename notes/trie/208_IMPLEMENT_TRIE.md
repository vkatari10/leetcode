# Implement Trie

See Leetcode Desc

```Python
class TrieNode:
    def __init__(self):
        '''
        The self.children is going to store other TrieNodes
        for every char in the word 

        is_end_of_word = True -> used during insert to mark 
        in the depth of the children that we have reached the 
        end of the word
        '''
        self.children = {}         
        self.is_end_of_word = False

class Trie:

    def __init__(self):
        self.root = TrieNode()
   

    '''
    For all 3 methods they are nearly identical the only difference is how
    we need to return 

    For insert this is what is happening

    1. start with the object root 
    2. For every char in that word
    3. Create a new TrieNode if the char is not here, else borrow an existing one
    4. Do this to the end of the word, then set the end node end of word to True


    Example:
            TrieNode (root)
            ├── 'c' → TrieNode
            └── 'a' → TrieNode
                ├── 't' → TrieNode (is_end=True)
                └── 'r' → TrieNode (is_end=True)

    '''
    def insert(self, word: str) -> None:
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.is_end_of_word = True # mark this node as the end of the word
  
    def search(self, word: str) -> bool:
        node = self.root
        for char in word:
            if char not in node.children: # if the char isn't there 
                return False
            node = node.children[char]
        return node.is_end_of_word # return if we got to the end

    def startsWith(self, prefix: str) -> bool:
        node = self.root
        for char in prefix:
            if char not in node.children:# stop searching
                return False
            node = node.children[char]
        return True # just return true beacuse we may not reach the end

# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```
Time: O(N) Since we need to store every char in every word for every method<br>
Space: O(N) Sice we store every word (is actually more specific but for the most part the space is just linear)<br>

Notes: This is like a tree but instead of nodes its just dicts, memorize this structure because idk where else it shows up except for problems like this
