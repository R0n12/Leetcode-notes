# #79 Word Search

## Description
Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

## Example
```java
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

## Constraints
- `board` and `word` consists only of lowercase and uppercase English letters.
- `1 <= board.length <= 200`
- `1 <= board[i].length <= 200`
- `1 <= word.length <= 10^3 `
  
---

## Logic

> ### __Backtracking__ 
> A methodology where we mark the current path of exploration, if the path does not lead to a solution, we then revert the change and try another path.

For this problem, we can try different direction of a grid, record each result and see if it matches a substring of the word, if not, revert and try another direction, if it matches, go deeper. basically a DFS procedure with a optional __revert__ behavior.

---

## Algorithms
1. Iterate through each grid
2. Call `backtrack()` function
    1. check the base case, if we already matched the required word
    2. check if the current letter is valid in the word or the grid is out of cell
    3. if the current condition is valid, we explore further, in possible four directions
    4. revert the grid back to original state

![Alt text](https://leetcode.com/problems/word-search/Figures/79/79_example.png)

---
## Code

```Java
 class Solution {
    private char[][]board;
    private int ROWS;
    private int COLS;
    
    public boolean exist(char[][] board, String word) {
        this.board = board;
        this.ROWS = board.length;
        this.COLS = board[0].length;
        for(int row = 0;row<ROWS;row++){
            for(int column = 0; column<COLS;column++){
                if(backtrack(row,column,0,word)){
                    return true;
                }
            }
        }
        return false;
    }
    
    private boolean backtrack(int rowpos, int columnpos, int index, String word){
        //check if the base case
        // if index is over word, it must return true
        if(index > word.length()-1){
            return true;
        }
        // if out of bound or not correct letter, return false
        if(rowpos <0 || rowpos==this.ROWS||columnpos<0||columnpos==this.COLS||this.board[rowpos][columnpos]!=word.charAt(index)){
            return false;
        }
        
        this.board[rowpos][columnpos] = '*';
        boolean result = false;
        int[] rowoff = {0,1,0,-1};
        int[] coloff = {1,0,-1,0};
        
        //explore four directions
        for(int d = 0; d < 4; d++){
             result = backtrack(rowpos+rowoff[d],columnpos + coloff[d], index+1,word);
            // switch(d){
            //     case 0:
            //         result = backtrack(rowpos-1,columnpos,index+1,word);
            //         break;
            //     case 1:
            //         result = backtrack(rowpos,columnpos+1,index+1,word);
            //         break;
            //     case 2:
            //         result = backtrack(rowpos+1,columnpos,index+1,word);
            //         break;
            //     case 3:
            //         result = backtrack(rowpos,columnpos-1,index+1,word);
            //         break;
            //     default:
            //         break;   
            // }
            
            if(result){
                break;
            }
        }
        this.board[rowpos][columnpos] = word.charAt(index);
        return result;
    }   
}
```

> 1. Use row offset array and column offset array to enable quicker operation in DFS search in four directions.
> 2. Can use switch, however, manage variable reference carefully.
> 3. mark visited and revert back -> __backtracking__

---

## Runtime

### $\mathcal{O}(N*4^L)$

>### $L$ : total length of the word
>### $N$ : total number of cells on the grid
>__Worst Case__: search all the four directions, each level of visiting nodes are $4$, n level then entails $4^n$ times of operation, for each cell, then $N*4^L$ times.


