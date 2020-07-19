# #208 Implement Trie (Prefix Tree) 

## Please check the problem description [here](https://leetcode.com/problems/implement-trie-prefix-tree/).

```Java
class TrieNode {

    // R links to node children
    private TrieNode[] links;

    private final int R = 26;

    private boolean isEnd;

    public TrieNode() {
        links = new TrieNode[R];
    }

    public boolean containsKey(char ch) {
        return links[ch -'a'] != null;
    }
    public TrieNode get(char ch) {
        return links[ch -'a'];
    }
    public void put(char ch, TrieNode node) {
        links[ch -'a'] = node;
    }
    public void setEnd() {
        isEnd = true;
    }
    public boolean isEnd() {
        return isEnd;
    }
}
```
* **Logic**
  * Use `TrieNode` to represent each link as a maximum of 26 alphabet  
  ![alt text](Week%20of%207.13%20Images/20801.png)
  * Use a boolean `isEnd` to indicate whether current node is a prefix or an endpoint
  * `containsKey(char ch)` -> just check if the position of that `ch` is null. null -> no associated string following; not null -> exist a string that has the `char ch`
  * `get(char ch)` -> get the correct position in the alphabet list, return that node.
  * `put(char ch, TrieNode node)` -> insert a new node with designated character
* **Syntax**
  * `links[ch-'a']`-> character are calculated as their ASCII values to find the right position 

```Java
class Trie {
    private TrieNode root;
    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {
            char currentChar = word.charAt(i);
            if (!node.containsKey(currentChar)) {
                node.put(currentChar, new TrieNode());
            }
            node = node.get(currentChar);
        }
        node.setEnd();
    }
    
    private TrieNode searchPrefix(String word) {
        TrieNode node = root;
        for (int i = 0; i < word.length(); i++) {
           char curLetter = word.charAt(i);
           if (node.containsKey(curLetter)) {
               node = node.get(curLetter);
           } else {
               return null;
           }
        }
        return node;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
       TrieNode node = searchPrefix(word);
       return node != null && node.isEnd();
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode node = searchPrefix(prefix);
        return node != null;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```
* **Logic**
  * `insert(String word)` -> insert all the character into the links;  
   after inserting one character, remember to reassign the `TrieNode` to subsequent position -> `node = node.get(currentChar)`;  
   remember to set end -> `node.setEnd()`
  * `Search` -> search prefix one char at a time and reassign the node downward;    
    if doesn't contain then return null;  
    Make sure to check if the last node is the end and is not a null node
  * `startsWith` -> just use the search prefix method except for checking the end criteria.
* **Runtime**
  * `insert`: $\mathcal{O}(m)$, m: key length
  * `search`: $\mathcal{O}(m)$
  * `startWith`: $\mathcal{O}(m)$
* **Space**
  * `insert`: $\mathcal{O}(m)$, m: key length
  * `search`: $\mathcal{O}(1)$
  * `startWith`: $\mathcal{O}(1)$

