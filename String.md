## Leetcode -3713

```java
class Solution {
    public static boolean checkBalance(int []arr)
    {
         int common=0;
        for(int i=0;i<26;i++){
        if(arr[i]==0)continue;
        if(common==0)
        {
            common=arr[i];
        }
        else if(common!=arr[i])
        {
            return false;
        }
    }
      return true;
    }
    public int longestBalanced(String s) {
        int max=0;
        for(int i=0;i<s.length();i++)
        {
            int[]arr=new int[26];
           for(int j=i;j<s.length();j++)
           {
              char ch=s.charAt(j);
              arr[ch-'a']++;
              if(checkBalance(arr))
              {
                max=Math.max(j-i+1,max);
              }
           }
        }
        return max;
    }
}
```
