# #212 Word Search II 

## Please check the problem description [here](https://leetcode.com/problems/word-search-ii/).

## Using Trie concepts, refer to [#208](https://leetcode.com/problems/implement-trie-prefix-tree/).

## First Impressions

```Java
    class TrieNode{
    final private int R = 26;
    private TrieNode[] links;
    private boolean isEnd;
    
    public TrieNode(){
        links = new TrieNode[R];
    }
    
    public TrieNode get(char ch){
        return links[ch-'a'];
    }
    
    public boolean ContainsKey(char ch){
        return links[ch-'a'] != null;
    }
    
    public void put(char ch, TrieNode node){
        links[ch-'a'] = node;
    }
    
    public void setEnd(){
        isEnd = true;
    }
    
    public boolean isEnd(){
        return isEnd;
    }
}

class Trie {
    
    private TrieNode root;

    /** Initialize your data structure here. */
    public Trie() {
        root = new TrieNode();
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode node = root;
        for(int i = 0; i<word.length();i++){
            char currentChar = word.charAt(i);
            if(!node.ContainsKey(currentChar)){
                node.put(currentChar, new TrieNode());
            }
            node = node.get(currentChar);
        }
        node.setEnd();
    }
    
    public TrieNode searchPrefix(String word){
        TrieNode node = root;
        for(int i = 0; i < word.length(); i++){
            char currentChar = word.charAt(i);
            if(node.ContainsKey(currentChar)){
                node = node.get(currentChar);
            }else{
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


class Solution {
    char[][] _board = null;
    ArrayList<String> _result = new ArrayList<String>();
    String _cur = "";
    public List<String> findWords(char[][] board, String[] words) {
        //construct a new trie
        Trie tree = new Trie();
        for(String word:words){
            tree.insert(word);
        }
        
        //loop thru the board
        this._board = board;
        for(int row = 0; row < board.length; row ++){
            for(int col = 0; col < board[row].length; col ++){
                //conduct backtracking search
                backtracking(row, col, tree);
            }
        }
        return this._result;
    }
    
    private void backtracking(int row, int col, Trie tree){
        
        Character currentChar = this._board[row][col];
        String temp = this._cur + Character.toString(currentChar);
        
        //check if there is any match
        if(tree.search(temp)){
            this._result.add(temp);
            this._cur = "";   
        }
        
        // mark as visited
        this._board[row][col] = '#';
        
        int[] rowOffset = {-1, 0, 1, 0};
        int[] colOffset = {0,1,0,-1};
        for(int i = 0; i< 4; i++){
            int newRow = row + rowOffset[i];
            int newCol = col + colOffset[i];
            if (newRow < 0 || newRow >= this._board.length || newCol < 0|| newCol >= this._board[0].length) {
                continue;
            }else{
                this._cur += Character.toString(this._board[newRow][newCol]);
                backtracking(newRow, newCol, tree);
            }
        }
        this._board[row][col] = currentChar;
    }
}
```
* **Error**: Time Limit Exceeded
  * $M \times N$ to construct the `Trie`
  * constucting the word from empty each time a word is searched.

## Solution
```Java
    class TrieNode {
  HashMap<Character, TrieNode> children = new HashMap<Character, TrieNode>();
  String word = null;
  public TrieNode() {}
}

class Solution {
  char[][] _board = null;
  ArrayList<String> _result = new ArrayList<String>();

  public List<String> findWords(char[][] board, String[] words) {

    // Step 1). Construct the Trie
    TrieNode root = new TrieNode();
    for (String word : words) {
      TrieNode node = root;

      for (Character letter : word.toCharArray()) {
        if (node.children.containsKey(letter)) {
          node = node.children.get(letter);
        } else {
          TrieNode newNode = new TrieNode();
          node.children.put(letter, newNode);
          node = newNode;
        }
      }
      node.word = word;  // store words in Trie
    }

    this._board = board;
    // Step 2). Backtracking starting for each cell in the board
    for (int row = 0; row < board.length; ++row) {
      for (int col = 0; col < board[row].length; ++col) {
        if (root.children.containsKey(board[row][col])) {
          backtracking(row, col, root);
        }
      }
    }

    return this._result;
  }
  
  private void backtracking(int row, int col, TrieNode parent) {
    Character letter = this._board[row][col];
    TrieNode currNode = parent.children.get(letter);

    // check if there is any match
    if (currNode.word != null) {
      this._result.add(currNode.word);
      // delete the end word to reduce duplicity
      currNode.word = null;
    }

    // mark the current letter before the EXPLORATION
    this._board[row][col] = '#';

    // explore neighbor cells in around-clock directions: up, right, down, left
    int[] rowOffset = {-1, 0, 1, 0};
    int[] colOffset = {0, 1, 0, -1};
    for (int i = 0; i < 4; ++i) {
      int newRow = row + rowOffset[i];
      int newCol = col + colOffset[i];
      if (newRow < 0 || newRow >= this._board.length || newCol < 0
          || newCol >= this._board[0].length) {
        continue;
      }
      if (currNode.children.containsKey(this._board[newRow][newCol])) {
        backtracking(newRow, newCol, currNode);
      }
    }

    // End of EXPLORATION, restore the original letter in the board.
    this._board[row][col] = letter;

    // Optimization: incrementally remove the leaf nodes
    if (currNode.children.isEmpty()) {
      parent.children.remove(letter);
    }
  }
}

```
* **Logic**
  * Mapping each TrieNode to a Character as `HashMap` - as children of a `TrieNode`
  * ![alt text](Week%20of%207.20%20Images/21201.png)
  * Add a word to a `TrieNode` if it is the end
  * set the word to `null` to avoid duplicity search
* **Optimization**
  * pruning leaf nodes if explored
    * reducing Trie size by pruning, which will optimize search time
    * ```Java
      // Optimization: incrementally remove the leaf nodes
      if (currNode.children.isEmpty()) {
      parent.children.remove(letter);
      }
      ```
  * backtracking along with `TrieNode`
    * instead of resetting to root at each backtracking, traverse the `Trie` along with backtracking
  * pruning searched words from `Trie`
    * ```Java
      // check if there is any match
       if (currNode.word != null) {
      this._result.add(currNode.word);
      // delete the end word to reduce duplicity
      currNode.word = null;
      }
      ```
* **Runtime**: $\mathcal{O}(M \cdot (4 \cdot 3^{L-1}))$
  * M: number of cell
  * 4: four direction initially to choose
  * 3: three direction to explore except the direction that we come from
  * L: length of the word
  * with pruning, the search time will be greatly reduced, since the `Trie` structure will reduce
* **Space**: $\mathcal{O}(N)$
  * N: total number of words in the dict

