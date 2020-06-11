# #42 Trapping Rain Water

## Please check the problem description [here](https://leetcode.com/problems/trapping-rain-water/).

## First Impressions

>1. try to iterate through the array to find the left bound and the right bound and make it  $\mathcal{O}(n)$.
>2. However, it was hard to track and keep increment the value since there are conditions that not all the max right are fulfilled.

## Brute Force
```Java
    class Solution {
    public int trap(int[] height) {
        int ans = 0;
        for(int i = 0; i< height.length;i++){
            int left_max = 0;
            int right_max = 0;
            for(int a = i; a >= 0; a--){
                left_max = Math.max(left_max, height[a]);
            }
            for(int b = i; b<height.length;b++){
                right_max = Math.max(right_max, height[b]);
            }
            ans += (Math.min(left_max, right_max)-height[i]);
        }
        return ans;
    }
}
```
Loop through the array, instead of finding right bound and left bound for the entire array, search both bounds for each block, and add the difference between them to the total area.  
right bound: `left_max=Math.max(left_max,height[j])`  
left bound: `right_max=Math.max(right_max,height[j])`  
total: `ans += Math.min(left_max, right_max)-height[current]`

>### Runtime: $\mathcal{O}(n^2)$, since looping through all the index to find bounds for each element in the array.
>### Space: $\mathcal{O}(1)$, no extra space.

## Dynamic Programming

```Java
    class Solution {
    public int trap(int[] height) {
        if(height.length == 0){
            return 0;
        }
        int ans = 0;
        int size = height.length;
        int[] left_max = new int[size];
        int[] right_max = new int[size];
        left_max[0] = height[0];
        for(int i = 1; i<size;i++){
            left_max[i] = Math.max(height[i],left_max[i-1]);
        }
        right_max[size-1] = height[size-1];
        for(int i = size-2;i>=0;i--){
            right_max[i] = Math.max(height[i],right_max[i+1]);
        }
        
        for(int i = 1; i< size-1;i++){
            ans += Math.min(left_max[i], right_max[i]) - height[i];
        }
        
        return ans;
    }
}
```

Store heights from left and from right until a certain new max point.  
Loop through the `height` array and add the max difference on the given current index using `left_max` and `right_max`

![alt text](Week%20of%206.8%20Images/#42WaterDP.png)

__Calculating areas using repeated shaded area approach__

>### Runtime: $\mathcal{O}(n)$, no more inside loops
>### Space: $\mathcal{O}(n)$, extra space for `left_max` and `right_max`.

## Using Stacks

```Java
    class Solution {
        public int trap(int[] height) {
            int current_index = 0;
            Stack<Integer> st = new Stack<Integer>();
            int ans = 0;
            /*loop thru all the index*/
            while(current_index<height.length){
                /*when the new top height need to be updated*/
                while(!st.isEmpty()&&height[current_index]>height[st.peek()]){
                    // pop out the current top
                    int top_index = st.pop();
                    if(st.isEmpty()){
                        break;
                    }
                    int dist = current_index - st.peek() - 1;// calculate horizontal distance
                    int bounded_height = Math.min(height[current_index], height[st.peek()]) - height[top_index];// calculate bounded height
                    ans += dist * bounded_height;// area calculation
                }
                st.push(current_index++);// update new top height
            }
            return ans;
        }
    }
```
Using Stack to keep track of the index of each height.

if the current height is bigger than current stack top, calculate previous bounded trapped rain area.

replace the current top with updated new top height.

>### Runtime: $\mathcal{O}(n)$, require looping through entire array only once
>### Space: $\mathcal{O}(n)$, stack can take up array space when encountering a flat or continuous stair structure











