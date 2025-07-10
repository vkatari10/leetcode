# Design Add and Search Words Data Structure

See leetcode problem.

```Python
class TrieNode: # same as regular Trie Structure 
    def __init__(self):
        self.trie = {}
        self.is_end_of_word = False

class WordDictionary:
    
    def __init__(self):
        self.root = TrieNode()

    def addWord(self, word: str) -> None: # same as regular Trie insert
        node = self.root
        for char in word:
            if char not in node.trie:
                node.trie[char] = TrieNode()
            node = node.trie[char]
        node.is_end_of_word = True
                
    def search(self, word: str) -> bool:
        def dfs(node, i):
            if i == len(word): # if the wild card took us to the end
                return node.is_end_of_word
            char = word[i] # now check this char 
            if char == ".":
                '''
                Since the "." can be anything we just check every branch
                possible at this point 
                '''
                return any(dfs(child, i + 1) for child in node.trie.values())
            if char not in node.trie:
                return False # same logic as add
            '''
            This the same idea as the other recursive statement above but since
            we know that this char exists we do not need to branch and we can 
            just return the char at this trie. 
            '''
            return dfs(node.trie[char], i + 1)
        return dfs(self.root, 0) # dont forget to call 
        


# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```
Time: O(26^N) since we can have at most 26 branches N times<br>
Space: O(N) since we end up storing each word char by char<br>

Notes: This is very similar to the implement Trie DS except for the fact that we need to account for wild cards, which makes this problem harder since we need to use Trie DFS.
