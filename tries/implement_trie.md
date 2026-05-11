# Implement Trie (Prefix Tree)

**Link:** https://leetcode.com/problems/implement-trie-prefix-tree/

## Approach

Each `TrieNode` holds a hashmap of children (character → node) and an `endOfWord` flag. The root is an empty node.

- **insert:** Walk the trie character by character, creating nodes as needed. Mark the final node as end of word.
- **search:** Walk the trie character by character, returning `False` on any missing child. Return whether the final node is marked end of word.
- **startsWith:** Same as search but return `True` at the end regardless of the `endOfWord` flag — we only care that the prefix exists.

## Code

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.endOfWord = False

class Trie:

    def __init__(self):
        self.root = TrieNode()

    def insert(self, word: str) -> None:
        cur = self.root

        for c in word:
            if c not in cur.children:
                cur.children[c] = TrieNode()
            cur = cur.children[c]
        cur.endOfWord = True

    def search(self, word: str) -> bool:
        cur = self.root

        for c in word:
            if c not in cur.children:
                return False
            cur = cur.children[c]
        
        return cur.endOfWord

    def startsWith(self, prefix: str) -> bool:
        cur = self.root

        for c in prefix:
            if c not in cur.children:
                return False
            cur = cur.children[c]
        
        return True
```

## Complexity

Time: O(n) per operation — where n is the length of the word or prefix  
Space: O(n · m) — n words of average length m stored in the trie
