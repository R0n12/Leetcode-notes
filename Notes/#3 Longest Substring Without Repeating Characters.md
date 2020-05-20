# #3 Longest Substring Without Repeating Characters

## Please check the problem description [here](https://leetcode.com/problems/longest-substring-without-repeating-characters/).

## First Try: Brute Force

```Java
    class Solution {
    public int lengthOfLongestSubstring(String s) {
        //convert string to char array
        char[] cry = s.toCharArray();
        //create hashset to enable unique character search
        Set<Character> temp = new HashSet<>();

        int maxlength = 0;
        //遍历每个character
        for(int i = 0; i<s.length();i++){
            int index = i;
            int length = 0;
            
            //往后查询最长substring
            while(index<s.length()){
                if(!temp.contains(cry[index])){
                    temp.add(cry[index]);
                    length++;
                    index++;
                }else{
                    break;
                }
            }
            
            if(length > maxlength){
                maxlength = length; 
            }
            temp.clear();
        }
        return maxlength;
    }
}
```

通过遍历每个character，继续往后遍历，运用HashSet存储唯一字符，同时增加长度，更新长度。

>### Runtime: $\mathcal{O}(n^3)$, 遍历character第一个循环$\mathcal{O}(n)$, 往后查询$\mathcal{O}(n)$, HashSet中查重,worst case是遍历长度为string length的HashSet, 所以$\mathcal{O}(n)$。  
>### Space: 需要最差长度为string length的空间去保存字符$\mathcal{O}(n)$

---

## Sliding Window __滑动窗口算法__

```Java
    class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        //set to store characters
        Set<Character> set = new HashSet<>();
        //set length, starting index, ending index
        int ans = 0,i=0,j=0;
        while(i<n && j<n){

            // if the set doesn't contain current character
            if(!set.contains(s.charAt(j))){
                set.add(s.charAt(j++));// first add char at j index, then j ++
                ans = Math.max(ans,j-i);
            // if duplicate character
            }else{
                // remove character at the starting point. move point one position forward.
                set.remove(s.charAt(i++));
            }
        }
        return ans;
    }
}
```
需要从头开始遍历每一个character, 但是只要后面有一个连续字符重复，通过j++往后移ending index, 就可以去掉这个starting character,因为这个substring已经不符合标准，去除的同时需要记录长度。同时将starting index往后移一个character。
>### Runtime: $\mathcal{O}(n)$, 最差情况，每个字符都要被i和j访问一次，2n
>### Space: 需要最差长度为string length的空间去保存字符$\mathcal{O}(n)$
---
## Sliding Window optimized __优化滑动窗口算法__

```Java
    public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        // use hash map to addistionally decrease search time
        Map<Character, Integer> map = new HashMap<>(); // current index of character
        // try to extend the range [i, j]
        for (int j = 0, i = 0; j < n; j++) {
            if (map.containsKey(s.charAt(j))) {
                i = Math.max(map.get(s.charAt(j)), i);
            }
            ans = Math.max(ans, j - i + 1);
            map.put(s.charAt(j), j + 1);
        }
        return ans;
    }
}
```

运用hashmap来缩短查重时间，通过查重后，如果有重复，可以直接跳过重复substring，增加starting index到最后重复位置，缩短时间

### Runtime: $\mathcal{O}(n)$
### Space: hashmap->n, charset->m, $\mathcal{O}(min(m,n))$


