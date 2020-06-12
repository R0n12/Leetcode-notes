# #71 Simplify Path

## Please check the problem description [here](https://leetcode.com/problems/simplify-path/).

## First Impressions
> 1. split the input path using "/" as delimiter
> 2. using stack, no clue

## Using Stack
```Java
    class Solution {
    public String simplifyPath(String path) {
        // initialize stack for implementation
        Stack<String> st = new Stack<String>();
        // split input string using '/' as delimiter
        String[] inputArr = path.split("/");
        // process inputArr thru iteration
        for(int i = 0; i< inputArr.length; i++){
            // if the string == "..", move up one directory, pop last element in stack if stack is not empty
            if(inputArr[i].equals("..")){
                if(!st.isEmpty()) st.pop();
            }else{
                // if the string is not empty and != ".", push the element
                if(inputArr[i].length()!=0 && !inputArr[i].equals(".")){
                    st.push(inputArr[i]);
                }
            }
        }
        
        // use StringBuilder class to concatenate all the strings
        StringBuilder result = new StringBuilder();
        for(String dir: st){
            result.append("/");
            result.append(dir);
        }
        
        return result.length() > 0 ? result.toString():"/";
        
        
    }
}
```
![alt text](Week%20of%206.8%20Images/71_Stack.png)

The above picture showed a general structure of a designated path. 

>* __All the given inputs are VALID paths__

By splitting the input path using "/", we can have the array of all directory name.
We only need to perform mulitple checks to decide which directory to push into the stack.

>* __".."__: this means that the path should be pop back one dir, this is where STACK came into place
>* __""__: because of the split method, consecutive "/" will be parsed to empty strings, if encountered, just skip and continue
>* __"."__: stay in the current directory, just skip and continue
>* __others__: push the valid dir name to the stack

Use `StringBuilder` class with `append()` to concatenate the strings together without constructing another store space.

Always check if stack is empty before popping.

Always check if the result is null or empty.

>### Runtime: $\mathcal{O}(n)$, splitting the string, and iterate thru the array: $2*n$
>### Space: $\mathcal{O}(n)$, Stack and array.